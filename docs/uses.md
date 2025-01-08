<!--
 Licensed to the Apache Software Foundation (ASF) under one or more
 contributor license agreements.  See the NOTICE file distributed with
 this work for additional information regarding copyright ownership.
 The ASF licenses this file to You under the Apache License, Version 2.0
 (the "License"); you may not use this file except in compliance with
 the License.  You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and
 limitations under the License.
-->

* goal
  * POPULAR use cases for Apache Kafka

* see [this blog post](/docs/blogs/theLog.md)

<h4 class="anchor-heading"><a id="uses_messaging" class="anchor-link"></a><a href="#uses_messaging"></a></h4>
# Messaging

* 👀== -- replacement for a -- traditional message broker 👀
  * message brokers uses
    * decouple processing -- from -- data producers,
    * buffer unprocessed messages
  * _Example of TRADITIONAL message systems:_ [ActiveMQ](https://activemq.apache.org), [RabbitMQ](https://www.rabbitmq.com) 

* vs MOST messaging systems
  * BETTER throughput,
  * built-in 
    * partitioning,
    * replication,
    * fault-tolerance

<h4 class="anchor-heading"><a id="uses_website" class="anchor-link"></a><a href="#uses_website"></a></h4>

# Website Activity Tracking

* TODO:
The original use case for Kafka was to be able to rebuild a user activity tracking pipeline as a set of real-time publish-subscribe feeds.
This means site activity (page views, searches, or other actions users may take) is published to central topics with one topic per activity type.
These feeds are available for subscription for a range of use cases including real-time processing, real-time monitoring, and loading into Hadoop or
offline data warehousing systems for offline processing and reporting.
<p>
Activity tracking is often very high volume as many activity messages are generated for each user page view.

<h4 class="anchor-heading"><a id="uses_metrics" class="anchor-link"></a><a href="#uses_metrics"></a></h4>
# Metrics

Kafka is often used for operational monitoring data.
This involves aggregating statistics from distributed applications to produce centralized feeds of operational data.

<h4 class="anchor-heading"><a id="uses_logs" class="anchor-link"></a><a href="#uses_logs"></a></h4>
# Log Aggregation

Many people use Kafka as a replacement for a log aggregation solution.
Log aggregation typically collects physical log files off servers and puts them in a central place (a file server or HDFS perhaps) for processing.
Kafka abstracts away the details of files and gives a cleaner abstraction of log or event data as a stream of messages.
This allows for lower-latency processing and easier support for multiple data sources and distributed data consumption.

In comparison to log-centric systems like Scribe or Flume, Kafka offers equally good performance, stronger durability guarantees due to replication,
and much lower end-to-end latency.

<h4 class="anchor-heading"><a id="uses_streamprocessing" class="anchor-link"></a><a href="#uses_streamprocessing"></a></h4>
# Stream Processing

Many users of Kafka process data in processing pipelines consisting of multiple stages, where raw input data is consumed from Kafka topics and then
aggregated, enriched, or otherwise transformed into new topics for further consumption or follow-up processing.
For example, a processing pipeline for recommending news articles might crawl article content from RSS feeds and publish it to an "articles" topic;
further processing might normalize or deduplicate this content and publish the cleansed article content to a new topic;
a final processing stage might attempt to recommend this content to users.
Such processing pipelines create graphs of real-time data flows based on the individual topics.
Starting in 0.10.0.0, a light-weight but powerful stream processing library called <a href="/documentation/streams">Kafka Streams</a>
is available in Apache Kafka to perform such data processing as described above.
Apart from Kafka Streams, alternative open source stream processing tools include <a href="https://storm.apache.org/">Apache Storm</a> and
<a href="https://samza.apache.org/">Apache Samza</a>.

<h4 class="anchor-heading"><a id="uses_eventsourcing" class="anchor-link"></a><a href="#uses_eventsourcing"></a></h4>
# Event Sourcing

<a href="https://martinfowler.com/eaaDev/EventSourcing.html">Event sourcing</a> is a style of application design where state changes are logged as a
time-ordered sequence of records. Kafka's support for very large stored log data makes it an excellent backend for an application built in this style.

<h4 class="anchor-heading"><a id="uses_commitlog" class="anchor-link"></a><a href="#uses_commitlog"></a></h4>
# Commit Log

Kafka can serve as a kind of external commit-log for a distributed system. The log helps replicate data between nodes and acts as a re-syncing
mechanism for failed nodes to restore their data.
The <a href="/documentation.html#compaction">log compaction</a> feature in Kafka helps support this usage.
In this usage Kafka is similar to <a href="https://bookkeeper.apache.org/">Apache BookKeeper</a> project.
