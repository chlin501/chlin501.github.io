# Functional Programming in Scala

## Monoids

### What is a monoid?

  * Some type A

  * An associative binary operation where op(op(x, y), z) = op(x, op(y, z))

  * A value zero that x == op(x, zero) and x == op(zero, x) for any x: A

  * trait

    ```scala
    trait Monoid[A] {
        def zero: A
        def op(a1: A, a2: A): A
    }
    ```

### Functors

  * trait

    ```scala
    trait Functor[F[_]] {
        def map[A, B](fa: F[A])(f: A => B): F[B]
    } 
    ```

  * map over a structure x with the identify function should itself be an identify

# References

  [1]. [Functional Programming in Scala](https://www.manning.com/books/functional-programming-in-scala)
