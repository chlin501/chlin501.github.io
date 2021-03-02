# Kleisli

  "Kleisli enables composition of functions that return a monadic value ... without having functions take an Option or Either as a parameter"[1]

# Examples 

  * Construct
 
      ```
      import cats.data.Kleisli 
      val f1 = (int: Int) => Option((int + 1).toDouble)
      val fn = Kleisli[Option, Int, Double](f1)
      val f2 = (double: Double) => Option(double.toString + "_double")
      val fn2 = Kleisli(function2)
      ```

  * Compose

      ```
      // define FlatMap[Option] instance operations See. [4], [5]

      fn1 andThen fn2
      ```

# References

  [1]. [Kleisli](https://typelevel.org/cats/datatypes/kleisli.html)

  [2]. [Step.scala @ Apache Hama git repo](https://git-wip-us.apache.org/repos/asf?p=hama.git;a=blob;f=bsp/src/main/scala/org/apache/hama/bsp/Step.scala;h=7b256d7b0735a87497453381196717605499a9c1;hb=0a24dc62593a84f0ad1243c789c406f2fb8b3265)

  [3]. [Step.scala @ Github](https://github.com/chlin501/bsp/blob/master/bsp/src/main/scala/org/apache/hama/bsp/Step.scala) 

  [4]/ [FlatpMap[...] @ Apache Hama git repo](https://git-wip-us.apache.org/repos/asf?p=hama.git;a=blob;f=bsp/src/main/scala/org/apache/hama/bsp/package.scala;h=e1ee84670b2826840d180cd21d66f8b7424c1e1c;hb=0a24dc62593a84f0ad1243c789c406f2fb8b3265)

  [5]. [FlatMap[...] @Github](https://github.com/chlin501/bsp/blob/master/bsp/src/main/scala/org/apache/hama/bsp/package.scala)
