# Save key-value data

# Save key-value data
* If you have a relatively small collection of key-values that you'd like to save, you should use the SharedPreferences APIs.
* A SharedPreferences object points to a file containing key-value pairs and provides simple methods to read and write them.
* Each SharedPreferences file is managed by the framework and can be private or shared.

## Get a handle to shared perferences
* You can create a new shared preference file or access an existing one by calling getPreferences() method.

```kotlin
val sharedPref = activity?.getPreferences(Context.MODE_PRIVATE)
```

## Write to shared preferences
* To write to a shared preferences file, create a SharedPreferences.Editor by calling edit() on your SharedPreferences.
    * Pass the keys and values you want to write with methods such as putInt() and putString(). Then call apply() or commit() to save the changes.

```kotlin
with (sharedPref.edit()) {
    putInt(getString(R.string.saved_high_score_key), newHighScore)
    apply()
}
```

# Read from shared perferences
* To retrieve values from a shared preferences file, call methods such as getInt() and getString(), providing the key for the value you want, and optionally a default value to return if the key isn't present.

```kotlin
val defaultValue = resources.getInteger(R.integer.saved_high_score_default_key)
val highScore = sharedPref.getInt(getString(R.string.saved_high_score_key), defaultValue)
```
