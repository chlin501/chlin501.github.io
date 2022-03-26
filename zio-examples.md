# ZIO Examples

  * [Arrow](https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/arrow/App.scala)

  * [Queue](https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/queue/App.scala)

      * Create queue

          ```scala
          val queue = Queue.bounded[Int](requestedCapacity = ...)
          ```

      * Share queue

          * Producer
 
              ```scala
              for {
                _ <- queue.offer(data)
              } yield ()
              ```    

          * Consumer

              ```scala
              for {
                data <- queue.take 
              } yield data
              ```
      * Note

          * UIO[Queue[T]] is equivalent to makeQueue, which creates a new queue each time when doing `for { q <- queue /* queue = UIO[Queue[T]] */ ... }`

  * [Resource](https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/resource/App.scala)

  * [Stream](https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/stream/App.scala)

      * [Stream with queue](https://github.com/chlin501/zio-stream-example/blob/main/src/main/scala/examples/App.scala)

  * [Task Status](https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/task/App.scala)


