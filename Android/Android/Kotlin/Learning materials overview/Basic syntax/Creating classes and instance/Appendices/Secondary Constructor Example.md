# Secondary Constructor Example
## Code
```Kotlin
class Person(name:String){
  val name:String
  init{
    this.name = name
  }
  constructor(name:String, company:String)
    :this(name + "@" + company)
  constructor(name:String, age:Int, company:String)
    :this(name + "." + age.toString(), company)
}

fun main(){
  val person1 = Person("Aditya","IFuture")
  println(person1.name)

  val person2 = Person("Aditya", 24, "IFuture")
  println(person2.name)
}
``` 
## Result
```
Aditya@IFuture
Aditya.24@IFuture
```

