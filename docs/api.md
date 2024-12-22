* Kafka core APIs
  * ==
    * <a href="#producerapi">Producer</a> 
    * <a href="#consumerapi">Consumer</a>
    * <a href="#streamsapi">Streams</a>
    * <a href="#connectapi">Connect</a>
    * <a href="#adminapi">Admin</a>

<h3 class="anchor-heading"><a id="producerapi" class="anchor-link"></a><a href="#producerapi">2.1 Producer API</a></h3>

* allows
  * publishing streams of data | Kafka cluster's topics
* uses 
  * applications can send -- streams of data to -- Kafka cluster's topics
* _Example:_ `KafkaProducer`
* requirements
  * add 
    ```
    <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-clients</artifactId>
      <version>{{fullDotVersion}}</version>
    </dependency>
    ```
    
<h3 class="anchor-heading"><a id="consumerapi" class="anchor-link"></a><a href="#consumerapi">2.2 Consumer API</a></h3>

* allows
  * subscribing -- streams of data from -- Kafka cluster's topics
    * -> can read from them
* uses
  * applications can read -- streams of data from -- Kafka cluster's topics
* _Example:_ `KafkaConsumer`
* requirements
  * add 
    ```
    <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-clients</artifactId>
      <version>{{fullDotVersion}}</version>
    </dependency>
    ```

<h3 class="anchor-heading"><a id="streamsapi" class="anchor-link"></a><a href="#streamsapi">2.3 Streams API</a></h3>

* allows
  * streams of data from input topics -- are transformed to -- output topics
    * == input streams -- are transformed to -- output streams 
* uses
  * stream processing applications and microservices
* == higher-level functions 
  * allows
    * processing event streams
    * transformations
    * stateful operations 
      * _Example:_ aggregations and joins, windowing, processing based on event-time, ...
* _Example:_ `KafkaStreams`
* requirements
  * add 
    ```
    <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-streams</artifactId>
      <version>{{fullDotVersion}}</version>
    </dependency>
    ```
  * if you use Scala
    * add
      ```
      <dependency>
        <groupId>org.apache.kafka</groupId>
        <artifactId>kafka-streams-scala</artifactId>
        <version>{{fullDotVersion}}</version>
      </dependency>
      ```
    * see [Kafka Streams DSL for Scala](streams/developer-guide/dsl-api.md)
* see [Kafka Streams documentation](streams)

<h3 class="anchor-heading"><a id="connectapi" class="anchor-link"></a><a href="#connectapi">2.4 Connect API</a></h3>

* allows
  * implementing connectors / continually
    * pull from SOME source system or application -- into -- Kafka
    * push from Kafka -- into -- SOME sink system or application
* uses
  * build and run reusable data
  * import/export connectors / consume (read) or produce (write) streams of events -- from & to -- external systems and applications
    * == integrate with Kafka
* _Example:_ connector -- to a -- relational database / capture EVERY change | set of tables
* ways to use
  * directly
  * indirectly -- via -- pre-built connectors / shared by the Kafka Community
* see [Kafka Connect](connect.md)

<h3 class="anchor-heading"><a id="adminapi" class="anchor-link"></a><a href="#adminapi">2.5 Admin API</a></h3>

* allows
  * about topics, brokers, other Kafka objects
    * managing
    * inspecting 
* requirements
  * add 
    ```
    <dependency>
      <groupId>org.apache.kafka</groupId>
      <artifactId>kafka-clients</artifactId>
      <version>{{fullDotVersion}}</version>
    </dependency>
    ```
* see `KafkaAdminClient`