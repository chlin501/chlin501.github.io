# Scala3 Examples

## Extension


```scala
trait Functor[F[_]] {
  extension [A, B](data: F[A])
    def map(f: A => B): F[B]
}

object App {

  def main(args: Array[String]): Unit = {

     val listF = new Functor[List] {
         extension [A, B](data: List[A])
             override def map(f: A => B): List[B] = data.map(f)
     }

     val data = List(1, 2, 3) 
     println(listF.map(data)(_+1))

  }
}

```
