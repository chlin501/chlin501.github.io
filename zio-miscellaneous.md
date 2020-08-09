# Miscellaneous

  * `*>` is a binary operator that ignores the output of left hand side

      ```scala
      val result = ZIO.succeed(1) *> ZIO.succeed(2) *> ZIO.succeed(3)
      val runtime = Runetime.default
      runtime.unsafeRune(result) // result = 3
      ```

  * `type State[S, E, A] = ZIO[Has[Ref[S]], E, A]`
