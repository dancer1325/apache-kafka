* TODO:
* However, the {@link KafkaFuture KafkaFutures} returned from request methods are executed
 * by a single thread so it is important that any code which executes on that thread when they complete
 * (using {@link KafkaFuture#thenApply(KafkaFuture.BaseFunction)}, for example) doesn't block
 * for too long. 
 *  * If necessary, processing of results should be passed to another thread.