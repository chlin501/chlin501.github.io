# ZIO Managed

## Steps

  1. Create resource

      ```scala
      resource <- ZManaged.make(acquire)(release)
      // acquire is a statement denoting what to do when obtaining resource e.g. queue.offer(_)
      // release is a function denoting after acquire operation, what to do next. For instance,
      // release = (successOrNot: Boolean) => 
      //             if(successOrNot) ZIO.unit 
      //             else ZIO...{ failure operations in dealing failure placing value in queue }
      ```

  2. Assemble program  

      ```scala
      program = resource(1) *> resource(2) *> resource(3)
      ```

  3. Retrieve result

      ```scala
      values  <- program.use_(ZIO.unit) *> queue.take 
      ```

# References

  [1]. https://github.com/chlin501/zio-examples/blob/master/src/main/scala/examples/resource/App.scala

  [2]. [ZManagedSpec](https://github.com/zio/zio/pull/1565/files#diff-d083a4b5d798e95bac8ee0be3c99b085R18)
