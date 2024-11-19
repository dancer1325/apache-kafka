* := interface /
  * 👀bytes -- are converted into -- objects 👀
* class / implements this interface
  * expectations
    * have a constructor / NO parameter
* see `org.apache.kafka.common.ClusterResourceListener`
* `default void configure(Map<String, ?> configs, boolean isKey);`
  * configure this class
* `T deserialize(String topic, byte[] data);`
  * `byte[]`'s record value -- is deserialized into a --
    * value or
    * object
* `default T deserialize(String topic, Headers headers, byte[] data) {}`
  * `byte[]`'s record value -- is deserialized into a --
    * value or
    * object
* `default T deserialize(String topic, Headers headers, ByteBuffer data) {}`
  * `ByteBuffer`'s record value -- is deserialized into a --
    * value or
    * object