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

A design pattern that allows for a generic type to apply a function inside without changing the structure of the generic type[2]. 

A type class that abstracts over type constructors that can be map‘ed over[3]. 

* `map` fucntion

    ```scala
    trait Functor[F[_]] {
        def map[A, B](fa: F[A])(f: A => B): F[B]
    } 
    ```

* Laws

    * Composition: `fa.map(f).map(g) = fa.map(f.andThen(g))`

    * Identity: `fa.map(x => x) = fa`

# References

  [1]. [Functional Programming in Scala](https://www.manning.com/books/functional-programming-in-scala)

  [2]. [Functor (functional programming)](https://en.wikipedia.org/wiki/Functor_(functional_programming))

  [3]. [Functor](https://typelevel.org/cats/typeclasses/functor.html)
