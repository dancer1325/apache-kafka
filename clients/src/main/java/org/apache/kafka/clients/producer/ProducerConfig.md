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