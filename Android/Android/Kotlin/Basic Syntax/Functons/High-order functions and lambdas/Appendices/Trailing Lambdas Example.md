# Trailing lambdas example
```kotlin
perate(a:Int, op:(Int)->Int):Int{
  return op(a)
}

fun main(){
  val a = operate(5){x:Int -> x*x}
  println(a)
}
```
