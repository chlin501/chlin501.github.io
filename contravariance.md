# Contravariance

  There are many examples, and explanation on the internet, but [1] serves as a better example for me.

## An example

  * Define base stuff

      ```
      trait Animal
      case class Dog(name: String) extends Animal
      ```

  * Define relations

      ```
      //in order to have a vet for my dog i.e. def vetForDog: Vet[Dog] = ???
  
      // define
      trait Vet[-T] { // trait Vet[-T <: Animal] 
        def heal(animal: T): Boolean
      }
      def vetForDog: Vet[Dog] = new Vet[Animal] {
        override def heal(animal: Animal): Boolean = {
          println(s"healing $animal ...")
          true
        }
      }
      ```

  * Execute the code

      ```
      // execution
      val myDog = Dog("lucky")
      val aVet = vetForDog()
      aVet.heal(myDog)

      // printed in console
      // healing Dog(lucky) ...
      // res6: Boolean = true
      ```

   * In this example, a `vet` who can heal `animal` (general) can also heal `dog` (specific type). 

# Another example

  * Define fruit stuff  

      ```
      trait Fruit extends Product with Serializable 
      case object Apple extends Fruit 
      case object Banana extends Fruit 
      ```

  * Create Banana basket

      ```
      val bananaBasket = List(Banana)
      // bananaBasket: List[Banana.type] = List(Banana)
      ```

  * Create Apple basket

      ```
      val appleBasket = List(Apple) 
      // appleBasket: List[Apple.type] = List(Apple)
      ```

  * Form a fruit basket

      ```
      bananaBasket ++ appleBasket // List.++ is defined as final def ++[B >: A](...): List[B]. See [2]
      // res18: List[Fruit] = List(Banana, Apple)
      ```

# References

  [1]. [Contravariance](https://www.youtube.com/watch?v=b1ftkK1zhxI&t=10m30s)

  [2]. [Making MyList Covariant](https://www.james-willett.com/scala-generics/#making-mylist-covariant)
