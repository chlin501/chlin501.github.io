
# Type Class

## Steps

1. Trait 

    ```
    trait Show[T] {
        def show(msg: T): String
    }
    ```

2. Instance

    ```
    object Show {
        implicit val intShow = new Show[Int] {
            ovrerride def show(value: Int): String = s"int: $value"
        }
    }
    ```

3. Creation

    ```
    object Show {
        def apply[T](implicit sh: Show[T]): Show[T] = sh

        implicit val ...
    }
    ```

4. Business Function

    ```    
    object Show {
        def apply...
        def show[A: Show](a: A) = Show[A].show(a)
        implicit val ...
    }
    ```

## Code

* Sample

    ```
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
