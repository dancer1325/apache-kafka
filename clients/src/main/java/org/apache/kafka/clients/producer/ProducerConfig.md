* == configuration -- for -- Kafka Producer

* TODO:
* `acks`
  * 👀:= # of acknowledgments / producer requires the leader to have received | BEFORE considering a request complete 👀
    * == controls the durability of records / are sent
    * ALLOWED values
      * `acks=0`
        * == producer -- will NOT wait for -- ANY acknowledgment from the server
        * 👀record -- will be IMMEDIATELY added to the -- socket buffer & considered sent 👀 ->
          * ⚠️ NO guarantee that the server has received the record ⚠️
            * == client will NOT generally know of any failures
          * ⚠️`retries` will NOT take effect ⚠️
            * Reason: 🧠 client NOT aware of ANY failure 🧠
        * -> offset given back / EACH record = -1
      * `acks=1`
        * == leader will write the record | its local log / respond WITHOUT awaiting FULL acknowledgement from ALL followers
          * if leader fails -> DONE | [IMMEDIATELY after acknowledging the record, BEFORE followers have replicated it]
            * -> record will be lost
      * `acks=all`
        * 👀== leader -- will wait for the -- FULL set of in-sync replicas to acknowledge the record 👀
          * -> if >=1 in-sync replica remains alive -> record will NOT be lost
        * strongest available guarantee
        * == `acks=-1`
  * idempotence
    * if you enable idempotence -> requires `acks=all`
    * if idempotence is NOT explicitly enabled & `acks!=all` -> idempotence is disabled
* TODO:
* `retries`
  * see [CommonClientConfigs](../CommonClientConfigs.md)
  * if >0 & SOME record / sent failed -- with a -- potentially transient error -> client will resend
    * 's behavior == record resent by the client | receiving the error 's behavior
  * 👀if timeout exceeded `DELIVERY_TIMEOUT_MS_CONFIG` ALTHOUGH # of retries NOT exhausted -> NO more attempts to retry == produce requests will be failed 👀
    * common use cases
      * unset `retries` & configure `DELIVERY_TIMEOUT_MS_CONFIG`
  * idempotence
    * if you enable idempotence -> requires `retries>0`
    * if idempotence is NOT explicitly enabled & `retries<=0` -> idempotence is disabled
  * if you enable it & `enable.idempotence=false` & `MAX_IN_FLIGHT_REQUESTS_PER_CONNECTION>1` -> potentially change the ordering of records
    * Reason: 🧠if 2 batches -- are sent to a -- 1! partition & first fails & retried / second succeeds -> second batch's records MAY appear first 🧠
* TODO: