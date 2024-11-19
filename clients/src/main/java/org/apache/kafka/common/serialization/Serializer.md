* := interface /
  * 👀objects -- are converted into -- bytes 👀
* class / implements this interface
  * expectations
    * have a constructor / NO parameter
* see `org.apache.kafka.common.ClusterResourceListener`
* `default void configure(Map<String, ?> configs, boolean isKey);`
  * allows
    * configuring this class
* `byte[] serialize(String topic, T data);`
  * `data` -- is converted into -- `byte[]`
* `default byte[] serialize(String topic, Headers headers, T data) {}`
  * `data` -- is converted into -- `byte[]`