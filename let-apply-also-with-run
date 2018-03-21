## let
#### definition
```kotlin
/**
* Calls the specified function [block] with `this` value as its argument and returns its result.
*/

public inline fun <T, R> T.let(block: (T) -> R): R = block(this)
```
   * called object passed in via argument
   * return type is whatever the lambda returns

#### typical usages

   * convert from one type to another
   * handling Nullability

// using 'let' to convert from one type to another

val answerToUniverse = strBuilder.let {

    it.append("Douglas Adams was right after all")

    it.append("Life, the Universe and Everything")

    42

}

// using 'let' to only print when str is not null

str?.let { print(it) }

Receiver vs. return value:

|                                  | Returns block result | Returns receiver |
|----------------------------------|----------------------|------------------|
| **Receiver available as `it`**   | `let`                | `also`           |
| **Receiver available as `this`** | `run`                | `apply`          |

How to read the table:

```kotlin
val returnValue = "Receiver".let {
    println("$it is the receiver")
    "Block result"
}
println(returnValue)
```
credits [arekolek](https://gist.github.com/arekolek/91bec2e6ba98446f39d60a7ea2c52f71#file-kotlinfunctions-md)
