# Briefing

Given and Using are contextual abstraction[1].

# Given

Givens are a way to ensure that the compiler helps us to fill in the needed contextual information without us explicitly passing it[2].

## Usage

### Single Canonical Value

    * In **object Logging**,
   
        * define

            ```scala
            // See [3]
            given consoLogger: Logging[String] = new Logging[String] {

                def info(f: => String): String = { println(f); f }
  
                def debug(f: => String): String = { println(f); f }

                def warn(f: => String): String = { println(f); f }

                def error(f: => String): String = { println(f); f }

            }
            ```

        * provide

            ```scala
            def apply[T: Logging]: Logging[T] = summon[Logging[T]]
            // or
            def apply[T: A](using ev: A[T]): ev.type = ev
            ```

    * In the **main** method,

        ```scala
        val log = Logging[String]
        log.info("Hello World!")
        ```

### Multiple Instances

* Create **Low Priority** trait. 

    ```scala
    trait LowPriority {
        given consoleLogger: Logging[String] = new Logging[String] { // low priority instance
           ...
        }
    }
    ```

* Inherit LowPriority trait

    ```scala
    // Please refer to implicit prioritization[4]
    // Generally when having the same type, the one in the sub class has a higher priority.
    object Logging extends LowPriority {
          // slf4jLogger is a higher priority instance, compared to the consoleLogger
          given slf4jLogger (using log: Slf4jLogger): Logging[String] = new Logging[String] ...

          // other types instances if any
          ...
    }
    ```

# Using

The contextual information such as Configuration[2], whose frequency to be changed is not very high, can be supplied with the keyword using, that can be picked up by compiler, instead of explicitly providing in each method call.

# References

[1]. [Given Instances and Using Clauses](https://docs.scala-lang.org/scala3/book/ca-given-using-clauses.html)

[2]. [An Introduction to Givens in Scala 3](https://blog.knoldus.com/an-introduction-to-givens-in-scala-3/)

[3]. [The Given Instance](https://github.com/chlin501/logging-scala3/blob/main/src/main/scala/logging/Logging.scala#L13)

[4]. [Is there a way to control which implicit conversion will be the default used?](https://stackoverflow.com/questions/1886953/is-there-a-way-to-control-which-implicit-conversion-will-be-the-default-used/1887678#1887678)

[5]. https://github.com/chlin501/logging-scala3/blob/main/src/main/scala/logging/Logging.scala#L27
