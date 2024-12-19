* == interface /
  * enforce a policy | alter configs requests
  * use cases
    * require that the topic's replication factor (`min.insync.replicas`) & / OR retention settings remain | allowable range
* 👀if `alter.config.policy.class.name` is defined -> Kafka -- will create, via the default constructor, an -- instance of the specified class 👀 
  * -> broker configs -- are passed to -- its `configure()`
  * | broker shutdown, -> invoked the `close()`-> if it's necessary -> resources can be released