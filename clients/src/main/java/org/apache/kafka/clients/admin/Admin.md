* == administrative client for Kafka /
  * about topics, brokers, configurations and ACLs
    * manage
    * inspect

* `Admin create(){}`
  * `Admin` instances returned -- are -- thread safe

* operations / exposed by Admin -> follow the pattern
  * `Admin` instances -- should be created via --
    * `Admin.create(Properties)`
    * `Admin.create(Map)`
  * 2 overloaded methods / EACH operation
    * one / uses a default set of options
    * another one / last parameter == explicit options object
  * operation method's first parameter == Collection of items | perform the operation on
    * recommendations
      * MULTIPLE requests / batch into 1! call's efficiency >> MULTIPLE calls | SAME method's efficiency
  * operation methods execute asynchronously
  * EACH `xxx` operation method -> returns an `XxxResult` class /
    * ' methods expose `KafkaFuture` -- for accessing the -- result(s) of the operation
  * `all()`
    * get the overall success/failure of the batch
  * `values()`
    * -- access to -- request batch's items
  * if you want synchronous behaviour -> use `KafkaFuture.get()`

* _Example:_ create a new topic -- via -- an Admin client instance 
  ```
    Properties props = new Properties();
    props.put(AdminClientConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
   
    try (Admin admin = Admin.create(props)) {
      String topicName = "my-topic";
      int partitions = 12;
      short replicationFactor = 3;
      // Create a compacted topic
      CreateTopicsResult result = admin.createTopics(Collections.singleton(
        new NewTopic(topicName, partitions, replicationFactor)
          .configs(Collections.singletonMap(TopicConfig.CLEANUP_POLICY_CONFIG, TopicConfig.CLEANUP_POLICY_COMPACT))));
   
      // Call values() to get the result for a specific topic
      KafkaFuture<Void> future = result.values().get(topicName);
   
      // Call get() to block until the topic creation is complete or has failed
      // if creation failed the ExecutionException wraps the underlying cause.
      future.get();
    }
    }
  ```

* <h3>Bootstrap and balancing</h3>
  * `bootstrap.servers`
    * see `CommonClientConfig`
    * if you pass -- via -- `Admin.create(Properties)` -> used for discovering the brokers | cluster
      * -> client -- will then connect to as -- needed

 * TODO: 
 * Different operations necessitate requests being sent to different nodes in the cluster. For example
 * {@link #createTopics(Collection)} communicates with the controller, but {@link #describeTopics(Collection)}
 * can talk to any broker. When the recipient does not matter the instance will try to use the broker with the
 * fewest outstanding requests.
 * 
 * The client will transparently retry certain errors which are usually transient.
 * For example if the request for {@code createTopics()} get sent to a node which was not the controller
 * the metadata would be refreshed and the request re-sent to the controller.


 * <h3>Broker Compatibility</h3>
 * <p>
 * The minimum broker version required is 0.10.0.0. Methods with stricter requirements will specify the minimum broker
 * version required.
 * <p>
 * This client was introduced in 0.11.0.0 and the API is still evolving. We will try to evolve the API in a compatible
 * manner, but we reserve the right to make breaking changes in minor releases, if necessary. We will update the
 * {@code InterfaceStability} annotation and this notice once the API is considered stable.