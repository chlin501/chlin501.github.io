# ZIO Actors

# Findings

  * Actor class itself doesn't maintain status

  * State is maintained by `Stateful` trait

      ```
      trait Stateful[R, S, ...] {
        def receive(state: State, ...) 
        override def makeActor(...)(initial: S) {
           def process(message: ..., state: Ref[State]) = for {
             ...
             ... <- receive(message, state)
             ...
           } yield ()


           for {
             state <- Ref.make(initial)
             ...
             ... <- ... process(message, state) ... // This defines how to process the queue. And run within a task forever by pulling data from queue. See [2]
           } yield new Actor(...)
        }
      }
      trait AbstractActor[R, S, ...] {
        def makeActor(..)(initial: S) = // where S denotes State. See [1]
      }
      ```

# References

  [1]. [AbstractStateful initial State](https://github.com/zio/zio-actors/blob/master/actors/src/main/scala/zio/actors/Actor.scala#L73) 

  [2]. [Stateful trait process()](https://github.com/zio/zio-actors/blob/master/actors/src/main/scala/zio/actors/Actor.scala#L60)
