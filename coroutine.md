# Coroutine

## Implementation

This implementation explores a new transformation approach.

### Preliminaries

#### Scala Macros

1. Declare *macro definitions*
 
    * Take ASTs as input arguments  

    * Return transformed ASTs

2. Invoke such *macro definitions* from user programs

3. Compose and Decompose ASTs inside the *macro definition*

4. Inspect the types of the expressions passed to the macro and reason about symbol identify

### Runtime Model 

The coroutines are **stackful**, nested coroutines calls are supported - the entire coroutine call stack needs to be restored.

* When `yield`ing,

    * the coroutine instance must store the **state** of the local variables

* When `resum`ing

    * the **state** must be retrieved into the local variables

#### Call stacks

* Use *arrays* to represent coroutine call stacks

* Divide a call stack into a sequence of coroutin frames

* Store each frame with 

    * *pointer* to the coroutine object (coroutine block)

    * *the position* in the coroutine where the last yield happened

    * *local variables* and *return values*

* Initialize stack size to **4** entries

#### Coroutine instance class

* Provide the Instance class

    ```scala
    class Instance {
      var _live = true                  // if the instance is live (non-terminated)
      var _call = false                 // if a nested call is in progress
      @exposed
      var _value: Y = null              // what the last yield value was
      @exposed
      var _result: R = null             // the result value if the instance terminated
      @exposed
      var _exception: Exception = null  // the exception that was thrown if any
      /* Call stack arrays */
      def resume()
    }
    ```

* Create a new instance by `start` method

#### Coroutine class

* Generate a new anonymous subclass of Coroutine class

    ```scala
    clss Coroutine[Y, R] {
      def _enter(i: Instance[Y, R]): Unit
    }
    class Coroutine1[T0, Y, R] extends Coroutine[Y, R] {
      def _call(i: Instance[Y, R], a0: T0): Unit
    }
    /* One class for each arity */
    ```

#### Trampolining

### Transformation


# References

[1]. [Theory and Practice of Coroutines with Snapshots](https://2018.ecoop.org/details/ecoop-2018-papers/14/Theory-and-Practice-of-Coroutines-with-Snapshots)
