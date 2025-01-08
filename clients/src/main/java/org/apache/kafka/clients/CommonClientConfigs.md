* `bootstrap.servers`
  * == list of host/port pairs
    * `host1:port1,host2:port2,...`
      * syntax
    * 👀order does NOT matter 👀
    * recommendations
      * include >1 server -- to ensure -- resilience
        * Reason: 🧠if any servers are down 🧠
        * NORMALLY, 2 or 3 is fine
    * ⚠️NOT need to contain the entire set of brokers ⚠️ 
      * Reason: 🧠Kafka clients automatic and efficiently manage and update connections -- to the -- cluster 🧠 
  * uses
    * establish the initial connection -- to the -- Kafka cluster
    * by clients, to bootstrap & discover the full set of Kafka brokers

* TODO: