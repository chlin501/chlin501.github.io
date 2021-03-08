# Definition

A context bound describes an implicit value. It is used to declare that for some type A, there is an implicit value of type B[A] available. See [1][2].

# Code

As the Logging example below, for the type Slf4jLogger, there is an implicit value of type Logging[Slf4j] available.

* Without Context Bounds 

    ```scala
    trait Logging[T] {
        ...
    }
    object Logging {

        def apply[T](implicit instance: Logging[T]) = instance

        implicit val slf4j = new Logging[Slf4jLogger] {
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

* With Context Bounds[3]

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

[2]. [Scala 2.8 Arrays](https://www.scala-lang.org/old/sites/default/files/sids/cunei/Thu, 2009-10-01, 13:54/arrays.pdf)

[3]. [With Context Bounds](https://github.com/chlin501/logging/blob/master/logging/src/main/scala/logging/Logging.scala#L21)
