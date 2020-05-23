# ZIO Task Status

  * Monitor task

      ```scala
      def monitor(supervisee: Fiber.Runtime[Throwable, Unit]) = for {
        status <- supervisee.status
        _ <- console.putStrLn(s"Supervisee's status ${supervisee.toString}")
      } yield ()
      ```

  * Main body

      ```scala
      val sched = Schedule.recurs(20) && Schedule.spaced(1 seconds)
      for {
        s <- supervisee() // ZIO Task { ... } operation
        m <- monitor(s).repeat(sched).fork
        _ <- s.join
        _ <- m.join
      } yield()
      ```

# Code

  * https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/task/App1.scala
