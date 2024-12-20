* Kafka core APIs
  * ==
    * <a href="#producerapi">Producer</a> 
    * <a href="#consumerapi">Consumer</a>
    * <a href="#streamsapi">Streams</a>
    * <a href="#connectapi">Connect</a>
    * <a href="#adminapi">Admin</a>

<h3 class="anchor-heading"><a id="producerapi" class="anchor-link"></a><a href="#producerapi">2.1 Producer API</a></h3>

* TODO:
* allows applications to send streams of data to topics in the Kafka cluster.
      The Producer API allows applications to send streams of data to topics in the Kafka cluster.
      <p>
      Examples showing how to use the producer are given in the
      <a href="/{{version}}/javadoc/index.html?org/apache/kafka/clients/producer/KafkaProducer.html" title="Kafka {{dotVersion}} Javadoc">javadocs</a>.
      <p>
      To use the producer, you can use the following maven dependency:

      <pre class="line-numbers"><code class="language-xml">&lt;dependency&gt;
      &lt;groupId&gt;org.apache.kafka&lt;/groupId&gt;
      &lt;artifactId&gt;kafka-clients&lt;/artifactId&gt;
      &lt;version&gt;{{fullDotVersion}}&lt;/version&gt;
&lt;/dependency&gt;</code></pre>

<h3 class="anchor-heading"><a id="consumerapi" class="anchor-link"></a><a href="#consumerapi">2.2 Consumer API</a></h3>

*  allows applications to read streams of data from topics in the Kafka cluster.
	The Consumer API allows applications to read streams of data from topics in the Kafka cluster.
	<p>
	Examples showing how to use the consumer are given in the
	<a href="/{{version}}/javadoc/index.html?org/apache/kafka/clients/consumer/KafkaConsumer.html" title="Kafka {{dotVersion}} Javadoc">javadocs</a>.
	<p>
	To use the consumer, you can use the following maven dependency:
	<pre class="line-numbers"><code class="language-xml">&lt;dependency&gt;
	&lt;groupId&gt;org.apache.kafka&lt;/groupId&gt;
	&lt;artifactId&gt;kafka-clients&lt;/artifactId&gt;
	&lt;version&gt;{{fullDotVersion}}&lt;/version&gt;
&lt;/dependency&gt;</code></pre>

<h3 class="anchor-heading"><a id="streamsapi" class="anchor-link"></a><a href="#streamsapi">2.3 Streams API</a></h3>

*  allows transforming streams of data from input topics to output topics.
	The <a href="/{{version}}/documentation/streams">Streams</a> API allows transforming streams of data from input topics to output topics.
	<p>
	Examples showing how to use this library are given in the
	<a href="/{{version}}/javadoc/index.html?org/apache/kafka/streams/KafkaStreams.html" title="Kafka {{dotVersion}} Javadoc">javadocs</a>.
	<p>
	Additional documentation on using the Streams API is available <a href="/{{version}}/documentation/streams">here</a>.
	<p>
	To use Kafka Streams you can use the following maven dependency:

	<pre class="line-numbers"><code class="language-xml">&lt;dependency&gt;
	&lt;groupId&gt;org.apache.kafka&lt;/groupId&gt;
	&lt;artifactId&gt;kafka-streams&lt;/artifactId&gt;
	&lt;version&gt;{{fullDotVersion}}&lt;/version&gt;
&lt;/dependency&gt;</code></pre>

	<p>
	When using Scala you may optionally include the <code>kafka-streams-scala</code> library.  Additional documentation on using the Kafka Streams DSL for Scala is available <a href="/{{version}}/documentation/streams/developer-guide/dsl-api.html#scala-dsl">in the developer guide</a>.
	<p>
	To use Kafka Streams DSL for Scala {{scalaVersion}} you can use the following maven dependency:

	<pre class="line-numbers"><code class="language-xml">&lt;dependency&gt;
	&lt;groupId&gt;org.apache.kafka&lt;/groupId&gt;
	&lt;artifactId&gt;kafka-streams-scala_{{scalaVersion}}&lt;/artifactId&gt;
	&lt;version&gt;{{fullDotVersion}}&lt;/version&gt;
&lt;/dependency&gt;</code></pre>

<h3 class="anchor-heading"><a id="connectapi" class="anchor-link"></a><a href="#connectapi">2.4 Connect API</a></h3>

*  API allows implementing connectors that continually pull from some source system or application into Kafka or push from Kafka into some sink system or application.
	The Connect API allows implementing connectors that continually pull from some source data system into Kafka or push from Kafka into some sink data system.
	<p>
	Many users of Connect won't need to use this API directly, though, they can use pre-built connectors without needing to write any code. Additional information on using Connect is available <a href="/documentation.html#connect">here</a>.
	<p>
	Those who want to implement custom connectors can see the <a href="/{{version}}/javadoc/index.html?org/apache/kafka/connect" title="Kafka {{dotVersion}} Javadoc">javadoc</a>.
	<p>

<h3 class="anchor-heading"><a id="adminapi" class="anchor-link"></a><a href="#adminapi">2.5 Admin API</a></h3>

*  allows managing and inspecting topics, brokers, and other Kafka objects.
	The Admin API supports managing and inspecting topics, brokers, acls, and other Kafka objects.
	<p>
	To use the Admin API, add the following Maven dependency:
	<pre class="line-numbers"><code class="language-xml">&lt;dependency&gt;
	&lt;groupId&gt;org.apache.kafka&lt;/groupId&gt;
	&lt;artifactId&gt;kafka-clients&lt;/artifactId&gt;
	&lt;version&gt;{{fullDotVersion}}&lt;/version&gt;
&lt;/dependency&gt;</code></pre>
	For more information about the Admin APIs, see the <a href="/{{version}}/javadoc/index.html?org/apache/kafka/clients/admin/Admin.html" title="Kafka {{dotVersion}} Javadoc">javadoc</a>.
	<p>
