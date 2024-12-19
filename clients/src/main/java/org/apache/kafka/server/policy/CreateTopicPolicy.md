* == interface /
  * enforce a policy | create topics requests
  * use cases
    * require that the topic's replication factor (`min.insync.replicas`) & / OR retention settings are | allowable range
* 👀if `create.topic.policy.class.name` is defined -> Kafka -- will create, via the default constructor, an -- instance of the specified class 👀 
  * -> broker configs -- are passed to -- its `configure()`
  * | broker shutdown, -> invoked the `close()`-> if it's necessary -> resources can be released
* TODO:
* `void validate(RequestMetadata requestMetadata) throws PolicyViolationException;`
  * validate the request parameters
    * if the create topics request parameters | ⚠️ provided topic ⚠️, do NOT satisfy this policy -> throws a `PolicyViolationException` / suitable error
      * == validations are / specific-topic
