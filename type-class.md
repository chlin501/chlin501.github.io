
# Type Class

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
