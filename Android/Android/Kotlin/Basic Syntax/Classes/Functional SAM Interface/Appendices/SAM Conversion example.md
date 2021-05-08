# SAM conversion example
```kotlin
fun interface Animal{
  fun MakeSound()
}

fun TakeForWalk(animal:Animal){
  println("Taking for walk")
  animal.MakeSound()
  println("Bringing back for walk")
}

fun main(){
  TakeForWalk{ println("bark bark!") }
}
```
