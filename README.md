# learn-kotlin
Learning Kotlin
Install Kotlin compiler
1. Download from Kotlin website.
2. Brew in Mac
```
brew install kotlin
which koltinc
```
`kotlinc` will launch REPL (Read Eval Print Loop)
`:quit` to quit the REPL

#6 Koltin Application Structure
use `vi` or other text editor, save as `Main.kt`
```
fun main(args: Array<String>) {
    println("Hello World.")
}
```
`fun main(args: Array<String>)` is entry point of Kotlin application.
To compile a kotlin file into bytecode use command
```
kotlinc Main.kt
```
`MainKt.class` will be created at the same current directory.

If no package is specified. Default package will be used. But otherwise:-
```
package com.monthol.learnkotlin
fun main(args: Array<String>) {
    println("Hello World.")
}
```
Now use the same command to compile packaged application:
```
kotlinc Main.kt
```
Folders will be created as per the package structure.
###I. Now to run the compiled class file, we also need Kotlin runtime.
We can specified runtime folder directly
```
java -cp .:/user/local/Cellar/kotlin/1.0.3/libexec/lib/kotlin-runtime.jar com.monthol.learnkotlin.MainKt
```
`.:` is required to include the current directory, so then the folder `com.monthol.learnkotlin` cna be fouund.
###II. Instead of specified the runtime directory, we can include by
```
kotlinc Main.kt -include-runtime -d hello.jar
```
So we created a jar file, which is archive of all class files in the project.
Now run jar-version of `java`
```
java -jar hello.jar
```
###III. Use `kotlin` with `class` file or `jar` file.
```
kotlin hello.jar
```
#10Types
Literal constants for number type:-
```
var myLong = 10L
var myFloat = 10F
var myHex = 0x0F
var myBinary = 0xb01
```
There is no implicit conversion in Kotlin, use helper function.
```
val myInt = 10
val myLongAgain = myInt //This will not compile.
val myToLong = myInt.toLong() //OK.
```
String in Kotlin
```
val rawString = "Hello" +
>>"This is second line" +
>>"This is third line" //OK but not nice
  
val rawString = """
  Hello
>>This is second line.
>>This is third line.
"""
