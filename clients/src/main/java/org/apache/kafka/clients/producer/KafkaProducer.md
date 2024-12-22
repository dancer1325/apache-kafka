* 👀== Kafka client / 
  * publishes records | Kafka cluster 👀
  * characteristics
    * 💡thread safe 💡
  * recommendations
    * 👀share 1! producer instance | ACROSS threads 👀
      * fast > MULTIPLE producer instances
  * ⚠️if producer closure fails -> these resources will leak  ⚠️
  * can communicate with brokers / v0.10.0+ 
    * if you communicate with brokers / v0.10.0- -> may NOT support certain client features

* _Example:_ producer / sends records of sequential numbers (key/value pairs) as strings
  ```
  Properties props = new Properties();
  props.put("bootstrap.servers", "localhost:9092");
  props.put("linger.ms", 1);  // 1 millisecond of latency | our request / wait for more records to arrive, if we did NOT fill up the buffer
  props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
  props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");
  
  Producer<String, String> producer = new KafkaProducer<>(props);
  for (int i = 0; i < 100; i++)
    producer.send(new ProducerRecord<String, String>("my-topic", Integer.toString(i), Integer.toString(i)));
  producer.close();
  ```

* 👀== pool of buffer space + background I/O thread 👀 
  * pool of buffer space
    * holds records / NOT yet transmitted to the server
  * background I/O thread /
    * PREVIOUS records
      * turn into requests
      * transmit them -- to the -- cluster

* `send(ProducerRecord){}`
  * asynchronous method
    * how does it work?
      * if you invoke it -> 
        * record is added | buffer of pending record
          * Reason: 🧠producer batch together individual records for efficiency 🧠
        * immediately returns
 
* `acks`
  * see [ProducerConfig](ProducerConfig.md)
  * by default, `acks=all`

* `retries`
 * see [ProducerConfig](ProducerConfig.md)
 * by default, `retries=Integer.MAX_VALUE`
 * recommendations
   * rather than set `retries`, set `delivery.timeout.ms`

* `batch.size`
  * see [ProducerConfig](ProducerConfig.md)
  * == size of producer's buffers of unsent records / EACH partition
  * ⚠️as larger -> requires more memory ⚠️

* `linger.ms`
  * see [ProducerConfig](ProducerConfig.md)
  * by default `=0` -> == IMMEDIATELY send out a record (ALTHOUGH < `batch.size`)
    * if records / arrive close together in time, ALTHOUGH `linger.ms=0` -> will generally batch together ()
  * == Nagle's algorithm | TCP
  * recommendations
    * set `>0`

* `buffer.memory`
  * see [ProducerConfig](ProducerConfig.md)

* `key.serializer`
  * see [ProducerConfig](ProducerConfig.md)

* `value.serializer`
  * see [ProducerConfig](ProducerConfig.md)

* | Kafka 0.11,
  * additional modes
    * idempotent producer
      * 💡 strengthens Kafka's delivery semantics: >= 1 -- to -> 1! delivery 💡
        * -> producer retries -- will NO longer introduce -- duplicates 
    * transactional producer
      * allows
        * application can send messages -- ,atomically (== ALL or NOTHING), to -- MULTIPLE partitions (& topics)

* | Kafka 3.0,
  * `enable.idempotence`
    * by default, `true`
    * if it's `true` -> `retries=Integer.MAX_VALUE` & `acks=all`
      * NO need to modify idempotent producer

* idempotent producer
  * requirements, to take advantage 1! delivery,
    * ⚠️avoid re-sends | application level ⚠️
      * Reason: 🧠 idempotent works | 🧠 
        * Network-level retries
        * Internal producer retries
        * Broker failures
      * -> recommendations
        * unset `retries`
          * == use the default one, `Integer.MAX_VALUE`
        * if `send(ProducerRecord)` returns an error ALTHOUGH infinite retries -> 
          * shut down the producer
          * check last produced message's contents are NOT duplicated
  * idempotence for messages sent / guaranteed | 1! session

* transactional producer & attendant APIs
  * requirements
    * set `transactional.id`
      * -> 👀AUTOMATICALLY enabled, idempotence + producer configs / idempotence depends on 👀
  * topics / included | transactions -- should be configured for -- durability
    * `replication.factor>3` &
    * `min.insync.replicas=2` | these topics
  * ⚠️if you want transactional guarantees E2E -> consumers MUST be configured to read ONLY committed messages ⚠️
  * 👀ALL messages invoked by `send()` between [`beginTransaction()`, `commitTransaction()`] -> will be part of 1! transaction 👀 
  * limitations
    * ⚠️ONLY 1 open transaction / producer ⚠️
  * if there are error states -> transactional producer uses exceptions
    * NOT required to specify
      * callbacks for `producer.send()` or
      * call `.get()` | returned Future 
  * transactional APIs
    * requirements
      * broker v0.11.0+
        * if you invoke an API / NOT available | running broker version -> you receive an `UnsupportedVersionException`

* `transactional.id`
  * see [ProducerConfig](ProducerConfig.md)
  * NEW transactional APIs
    * are blocking
    * | failure -> will throw exceptions
  * _Example:_ how to use new APIs
    * vs PREVIOUS Example -- HERE, ALL 100 messages -- are part of a -- 1! transaction 
      ```
        Properties props = new Properties();
        props.put("bootstrap.servers", "localhost:9092");
        props.put("transactional.id", "my-transactional-id");
        Producer<String, String> producer = new KafkaProducer<>(props, new StringSerializer(), new StringSerializer());
    
        producer.initTransactions();
    
        try {
            producer.beginTransaction();
            for (int i = 0; i < 100; i++)
                producer.send(new ProducerRecord<>("my-topic", Integer.toString(i), Integer.toString(i)));
            producer.commitTransaction();
        } catch (ProducerFencedException | OutOfOrderSequenceException | AuthorizationException e) {
            // We can't recover from these exceptions, so our only option is to close the producer and exit.
            producer.close();
        } catch (KafkaException e) {
            // For all other exceptions, just abort the transaction and try again.
            producer.abortTransaction();
        }
        producer.close();
      ```

* `void abortTransaction(){}`
  * aborts the ongoing transaction
    * 💡== if you invoke it -> unflushed produce messages -- will be -- aborted 💡
      * -> keeps the transactional guarantees
  * if ANY prior `send(ProducerRecord)` calls failed with a `ProducerFencedException` OR an instance of `AuthorizationException` -> throw an exception IMMEDIATELY
  * exceptions
    * if the transaction can NOT be aborted | BEFORE expiration of `max.block.ms` -> will raise `TimeoutException` 
      * != request did NOT reach the broker
      * == can NOT get the acknowledgement response | time
      * -> up to the application's logic, how to handle timeouts
    * if interrupted -> will raise `InterruptException`
  * | previous exceptions,
    * POSSIBLE actions to take
      * retry
      * close the producer 
    * NOT possible to attempt a different operation (_Example:_ `commitTransaction`)
      * Reason: 🧠 abort MAY ALREADY be in the progress of completing 🧠
  * recommendations
    * 👀if you catch `KafkaException` -> ALWAYS call `abortTransaction()` 👀 
