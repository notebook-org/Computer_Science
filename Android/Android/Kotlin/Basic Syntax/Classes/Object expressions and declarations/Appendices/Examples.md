# Examples
## Creating anonymous objects from scratch
```kotlin
val helloWorld = object {
    val hello = "Hello"
    val world = "World"
    // object expressions extend Any, so `override` is required on `toString()`
    override fun toString() = "$hello $world"
}
```
## Inheriting anonymous objects from supertypes
```kotlin
window.addMouseListener(object : MouseAdapter() {
  override fun mouseClicked(e: MouseEvent) { /*...*/ }

  override fun mouseEntered(e: MouseEvent) { /*...*/ }
})
```
