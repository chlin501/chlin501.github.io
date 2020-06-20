# Code

* Without Context Bounds 

    ```scala
    trait Logging[T] {
        ...
    }
    object Logging {

        def apply[T](implicit instance: Logging[T]) = instance

        implicit val slf4j = new Logging[Slf4Logger] {
            ...
        }
    }
    object App {
        def main(args: Array[String]): Unit = {
            import Logging._  // compile error
            //[error] ... not enough arguments for method apply: (implicit s: Logging[T]): Logging[T] in object Logging. 
        }
    }
    ```

* With Context Bounds[2]

    ```scala
    trait Logging[T] {
        ...
    }
    object Logging {

        def apply[T: Logging]() = implicitly[Logging[T]]

        implicit val slf4j = new Logging[Slf4Logger] {
            ...
        }
    }
    object App {
        def main(args: Array[String]): Unit = {
            import Logging._  //  compile without a problem
            log.info("hello world!")
        }
    }
    ```

# References

[1]. [What are Scala context bounds?](https://docs.scala-lang.org/tutorials/FAQ/context-bounds.html)

[2]. [With Context Bounds](https://github.com/chlin501/logging/blob/master/logging/src/main/scala/logging/Logging.scala#L21)
