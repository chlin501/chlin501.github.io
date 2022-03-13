# Functional Programming

## Magma

A magma consists of a set equipped with a single binary operation that must be closed by definition. No other properties are imposed.[1]

  * A set *M*

  * An operation **•**

  * Closure axiom: a,b ∈ *M* ⇒ a•b ∈ *M*

## Semigroup

A semigroup is an algebraic structure consisting of a set together with an associative binary operation.[2] 

### Definition

  * A set *S*

  * A binary operation *•*

  * Associative property: ∀ a,b,c ∈ *S* where (a•b)•c = a•(b•c)

### Example

  ```scala
  trait Semigroup[A] {
    def combine(a: A, b: A): A
  }
  ```

## Monoid

A monoid is a set equipped with an associative binary operation and an identity element.[3] 

### Definition

  * A set *S* 

  * A binary operation: S × S → S

  * Two axioms

      * Associativity: ∀ a,b,c ∈ *S* where (a•b)•c = a•(b•c) 

      * Identity element: ∃ id ∈ *S*, ∀ e ∈ *S* where id•e = e and e•id = e

### Example

  ```scala
  trait Monoid[A] extends Semigroup[A] {
    def id: A
  }
  ```

## Functor

A functor allows for a generic type to apply a function inside without changing the structure of the generic type.[4] 

### Laws

  1. `map(id) = id`

  2. `map(f andThen g) = map(f) andThen map(g)`

### Example

  ```scala
  trait Functor[F[_]] {
    def map[A, B](fa: F[A])(f: A => B): F[B]
  } 
  ```

## Applicative

An intermediate structure[6] between functors and monads. It allows sequenced functorial computations, but doesn't allow using results from prior computations[6].

### Methods

  * `pure`: bring value(s) to applicative (like constructor)

  * `liftA2` or `<*>`: apply a function wrapped in a context to a value wrapped in a context[7]

### Laws


# References

  [1]. [Magma (algebra)](https://en.wikipedia.org/wiki/Magma_(algebra))

  [2]. [Semigroup](https://en.wikipedia.org/wiki/Semigroup)

  [3]. [Monoid](https://en.wikipedia.org/wiki/Monoid)

  [4]. [Functor (functional programming)](https://en.wikipedia.org/wiki/Functor_(functional_programming))

  [5]. [The functor laws](https://en.wikibooks.org/wiki/Haskell/The_Functor_class#The_functor_laws)

  [6]. [Applicative functor](https://en.wikipedia.org/wiki/Applicative_functor)

  [7]. [Applicatives](https://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html#applicatives)
