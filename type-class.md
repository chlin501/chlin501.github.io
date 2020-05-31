
# Type Class

In addition to the explanation desribed on the internet[1]. Scala type class makes use of type parameter denoting what kind of type this class uses. For instance, a config type class may load from typesafe or hadoop configuration; therefore, a type class `Setting[typesafe.Config]` or `Setting[hadoop.Configuration]` can be used to explicitly point out what kind of type underpins this setting. Thus the type parameter in `MyTrait[T]` usually is a single type, instead of complicated expression such as `MyTrait[I => O], `MyTrait[A, B, C]`, and so on.

## Steps

1. Trait 

    ```scala
    trait Show[T] {
        def show(msg: T): String
    }
    ```

2. Instance

    ```scala
    object Show {
        implicit val intShow = new Show[Int] {
            ovrerride def show(value: Int): String = s"int: $value"
        }
    }
    ```

3. Creation

    ```scala
    object Show {
        def apply[T](implicit sh: Show[T]): Show[T] = sh

        implicit val ...
    }
    ```

4. Business Function

    ```scala
    object Show {
        def apply...
        def show[A: Show](a: A) = Show[A].show(a)
        implicit val ...
    }
    ```

## Code

* Sample

    ```scala
    trait Show[T] {
        def show(msg: T): String
    }
    object Show {
        def apply[T](implicit s: Show[T]) = s
        def show[A: Show](msg: A) = Show[A].show(msg)
        implicit val intShow = new Show[Int] {
            override def show(msg: Int) = s"msg: $msg"
        }
    }
    object App {
        def main(args: Array[String]): Unit = {
            import Show._
            println(show(3))
        }
    }
    ```

# References

  [1]. [Type class](https://en.wikipedia.org/wiki/Type_class) 
