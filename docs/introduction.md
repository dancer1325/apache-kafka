<h4 class="anchor-heading">
    <a class="anchor-link" id="intro_streaming" href="#intro_streaming"></a>
    <a href="#intro_streaming">What is event streaming?</a>
</h4>

* Event streaming
  * == digital human body's central nervous system
  * uses
    * | 'always-active' world
      * businesses are
        * software-defined
        * automated,
      * user of software is software
  * goal
    * capture data | real-time -- from -- event sources
      * _Example:_ databases, sensors, mobile devices, cloud services, and software applications | form of streams of events
      * how does it work?
        * event streams are stored
      * uses of data
        * manipulate,
        * processing,
        * react to the event streams | real-time & retrospectively
        * routing the event streams -- to -- different destination technologies

<h4 class="anchor-heading">
          <a class="anchor-link" id="intro_usage" href="#intro_usage"></a>
          <a href="#intro_usage">What can I use event streaming for?</a>
</h4>

* [WIDE use cases](https://kafka.apache.org/powered-by) | DIFFERENT industries & organizations
  * process payments & financial transactions | real-time
    * _Example:_ stock exchanges, banks, and insurances 
  * track and monitor cars, trucks, fleets, and shipments | real-time
    * _Example:_ logistics & automotive industry 
  * continuously capture & analyze sensor data from IoT devices or other equipment
    * _Example:_ factories and wind parks
  * collect and immediately react to customer interactions and orders
    * _Example:_ retail, hotel and travel industry and mobile applications
  * monitor patients | hospital care and predict changes in condition
  * connect, store, and make available data / produced by different divisions of a company
  * foundation for 
    * data platforms,
    * event-driven architectures,
    * microservices

<h4 class="anchor-heading">
                            <a class="anchor-link" id="intro_platform" href="#intro_platform"></a>
                            <a href="#intro_platform">Apache Kafka&reg; == event streaming platform</a>
</h4>

* Kafka
  * 👀== 3 key capabilities, about event streaming, 👀
    * <strong>publish</strong> (to write) & <strong>subscribe</strong> (to read) -- streams of events /
      * include continuous import/export of your data -- from -- OTHER systems
    * <strong>store</strong> streams of events
      * durably
      * reliably
    * <strong>process</strong> streams of events |
      * as they occur or
      * retrospectively
  * allows
    * implementing your use cases -- for -- event streaming E2E / 👀1! battle-tested solution 👀
  * can be deployed | 
    * bare-metal hardware,
    * virtual machines,
    * containers,
    * on-premises
    * cloud
  * about managing
    * self-managing
    * fully managed services / -- offered by a -- variety of vendors
  * provides it's functionality in a manner 
    * distributed,
    * highly scalable,
    * elastic,
    * fault-tolerant,
    * secure

<h4 class="anchor-heading">
                            <a class="anchor-link" id="intro_nutshell" href="#intro_nutshell"></a>
                            <a href="#intro_nutshell">How does Kafka work | nutshell?</a>
</h4>

* Kafka
  * 👀 servers + clients 👀
    * == distributed system
    * / communicate -- via a -- high-performance [TCP network protocol](protocol.md)
    * Servers
      * 👀== cluster of >=1 servers 👀/ 
        * can span multiple datacenters OR cloud regions
        * uses of these servers
          * 👀brokers == storage layer / made up of SOME of these previous servers 👀
          * run [Kafka Connect](connect.md) 
      * highly scalable & fault-tolerant
        * == if ANY of its servers fails -> other servers -- will take over -- their work
          * Reason: 🧠ensure continuous operations / NO data loss 🧠
    * Clients
      * allow you
        * write distributed applications & microservices / about streams of events
          * actions
            * read,
            * write,
            * process
          * via
            * in parallel,
            * at scale,
            * fault-tolerant
      * types
        * built-in
        * [community](https://cwiki.apache.org/confluence/display/KAFKA/Clients)

<h4 class="anchor-heading">
                            <a class="anchor-link" id="intro_concepts_and_terms" href="#intro_concepts_and_terms"></a>
                            <a href="#intro_concepts_and_terms">Main Concepts and Terminology</a>
</h4>
                          <p>
                            An <strong>event</strong> records the fact that "something happened" in the world or in your business. It is also called record or message in the documentation. When you read or write data to Kafka, you do this in the form of events. Conceptually, an event has a key, value, timestamp, and optional metadata headers. Here's an example event:
                          </p>
                          <ul>
                            <li>
                              Event key: "Alice"
                            </li>
                            <li>
                              Event value: "Made a payment of $200 to Bob"
                            </li>
                            <li>
                              Event timestamp: "Jun. 25, 2020 at 2:06 p.m."
                            </li>
                          </ul>
                          <p>
                            <strong>Producers</strong> are those client applications that publish (write) events to Kafka, and <strong>consumers</strong> are those that subscribe to (read and process) these events. In Kafka, producers and consumers are fully decoupled and agnostic of each other, which is a key design element to achieve the high scalability that Kafka is known for. For example, producers never need to wait for consumers. Kafka provides various <a href="/documentation/#semantics">guarantees</a> such as the ability to process events exactly-once.
                          </p>
                          <p>
                            Events are organized and durably stored in <strong>topics</strong>. Very simplified, a topic is similar to a folder in a filesystem, and the events are the files in that folder. An example topic name could be "payments". Topics in Kafka are always multi-producer and multi-subscriber: a topic can have zero, one, or many producers that write events to it, as well as zero, one, or many consumers that subscribe to these events. Events in a topic can be read as often as needed—unlike traditional messaging systems, events are not deleted after consumption. Instead, you define for how long Kafka should retain your events through a per-topic configuration setting, after which old events will be discarded. Kafka's performance is effectively constant with respect to data size, so storing data for a long time is perfectly fine.
                          </p>
                          <p>
                            Topics are <strong>partitioned</strong>, meaning a topic is spread over a number of "buckets" located on different Kafka brokers. This distributed placement of your data is very important for scalability because it allows client applications to both read and write the data from/to many brokers at the same time. When a new event is published to a topic, it is actually appended to one of the topic's partitions. Events with the same event key (e.g., a customer or vehicle ID) are written to the same partition, and Kafka <a href="/documentation/#semantics">guarantees</a> that any consumer of a given topic-partition will always read that partition's events in exactly the same order as they were written.
                          </p>
                          <figure class="figure">
                            <img src="/images/streams-and-tables-p1_p4.png" class="figure-image" />
                            <figcaption class="figure-caption">
                              Figure: This example topic has four partitions P1–P4. Two different producer clients are publishing,
                              independently from each other, new events to the topic by writing events over the network to the topic's
                              partitions. Events with the same key (denoted by their color in the figure) are written to the same
                              partition. Note that both producers can write to the same partition if appropriate.
                            </figcaption>
                          </figure>
                          <p>
                            To make your data fault-tolerant and highly-available, every topic can be <strong>replicated</strong>, even across geo-regions or datacenters, so that there are always multiple brokers that have a copy of the data just in case things go wrong, you want to do maintenance on the brokers, and so on. A common production setting is a replication factor of 3, i.e., there will always be three copies of your data. This replication is performed at the level of topic-partitions.
                          </p>
                          <p>
                            This primer should be sufficient for an introduction. The <a href="/documentation/#design">Design</a> section of the documentation explains Kafka's various concepts in full detail, if you are interested.
                          </p>

<h4 class="anchor-heading">
                            <a class="anchor-link" id="intro_apis" href="#intro_apis"></a>
                            <a href="#intro_apis">Kafka APIs</a>
</h4>
                          <p>
                            In addition to command line tooling for management and administration tasks, Kafka has five core APIs for Java and Scala:
                          </p>
                          <ul>
                            <li>
                              The <a href="/documentation.html#adminapi">Admin API</a> to manage and inspect topics, brokers, and other Kafka objects.
                            </li>
                            <li>
                              The <a href="/documentation.html#producerapi">Producer API</a> to publish (write) a stream of events to one or more Kafka topics.
                            </li>
                            <li>
                              The <a href="/documentation.html#consumerapi">Consumer API</a> to subscribe to (read) one or more topics and to process the stream of events produced to them.
                            </li>
                            <li>
                              The <a href="/documentation/streams">Kafka Streams API</a> to implement stream processing applications and microservices. It provides higher-level functions to process event streams, including transformations, stateful operations like aggregations and joins, windowing, processing based on event-time, and more. Input is read from one or more topics in order to generate output to one or more topics, effectively transforming the input streams to output streams.
                            </li>
                            <li>
                              The <a href="/documentation.html#connect">Kafka Connect API</a> to build and run reusable data import/export connectors that consume (read) or produce (write) streams of events from and to external systems and applications so they can integrate with Kafka. For example, a connector to a relational database like PostgreSQL might capture every change to a set of tables. However, in practice, you typically don't need to implement your own connectors because the Kafka community already provides hundreds of ready-to-use connectors.
                            </li>
                          </ul>

                          <!-- TODO: add new section once supporting page is written -->

<h4 class="anchor-heading">
                            <a class="anchor-link" id="intro_more" href="#intro_more"></a>
                            <a href="#intro_more">Where to go from here</a>
</h4>
                          <ul>
                            <li>
                              To get hands-on experience with Kafka, follow the <a href="/quickstart">Quickstart</a>.
                            </li>
                            <li>
                              To understand Kafka in more detail, read the <a href="/documentation/">Documentation</a>.
                              You also have your choice of <a href="/books-and-papers">Kafka books and academic papers</a>.
                            </li>
                            <li>
                              Browse through the <a href="/powered-by">Use Cases</a> to learn how other users in our world-wide community are getting value out of Kafka.
                            </li>
                            <li>
                              Join a <a href="/events">local Kafka meetup group</a> and
                              <a href="https://kafka-summit.org/past-events/">watch talks from Kafka Summit</a>, the main conference of the Kafka community.
                            </li>
                          </ul>

<div class="p-introduction"></div>
