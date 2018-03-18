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
  "This is second line" +
  "This is third line" //OK but not nice
  
val rawString = """
  Hello
  This is second line.
  This is third line.
"""
```
String interpolation and invoke function in string interpolation
```
val years = 10
println("A decade is $year years.")

val name = "Mary"
println("The name length is ${name.length} long.") //length is a String property (the only one).
```
# 11 Loop and Ranges
Note - Kotlin allows to have `fun main(args Array<String>)` in each file in the package but not two in the same file.
`..` is an operator overloaded for rangeTo() function

Reverse loop can use `..` or `downTo`

```
for (a in 100 downTo 1 step 5) {
  println(a)
}
val capitals= listOf("London", "Paris", "Rome", "Madrid")
for (capital in capitals) {
  p
```
`Unit` equivalent to other languages `void`
`when` equivalent to Java `case`
When using `if` and `when` as an expression, expression must be exhaustive. i.e. it probably need `else` statement.

# 14-16 functions
By default return type is `Unit` object, equivalent to `void`. For not return at all use return type `Nothing`, which is a `class`.
### I. Default parameters
### II. Named parameter
not recommend function with 4-5 parameters
### III varied argument numbers
pass in undefined number of parameters not known before hands.
`*` spread operators is used to pass vararg arguments to another function.
# 17 Classes
class can have property declared just like variables. Much like Immutable properties.
Kotlin has no concept of field in Kotlin.
No `new` keyword in Kotlin.

If you don't want to initialize the properties, we can move it to constructor. That means we want to do initialization when creating the class.

```
class Customer(var id: Integer, var name: String) {
}
```
without `var`, `id` and `name` are just parameters passed to constructor. with `var`, `id` and `name` are now properties (`customer.id` is available.)

'init' block cannot be used to defined new properties.
```
class Customer (val id: String, name: String) {
    init {
        val upperName = name.toUpperCase()
    }
}

fun main(args: Array<String>) {
	val customer = Customer("1", "Monthol")
    println(customer.upperName) //unresolved reference upperName
}
```
### Custom getter and setter
If we want to define custom getters and setters, we need to define a property in the class body instead of the class declaration header.
```
class Customer (val id: Int, var name: String, var yearOfBirth: Int) {
    val age: Int
        get() = Calendar.getInstance().get(Calendar.YEAR) - yearOfBirth
}

val customer = Customer(1, "Monthol", 1978)
```
When we provide custom setter. Kotlin does not auto setting the value. We need to set the property by accessing the backing field with `field`

```
class Customer (val id: Int, var name: String, var yearOfBirth: Int) {
    val age: Int
        get() = Calendar.getInstance().get(Calendar.YEAR) - yearOfBirth
    val socialSecurityNumber: String
        set(value) {
            if (!value.startWith("SN")) {
                throw IllegalArgumentException ("Value not started with SN")
            }
            field = value
        }
}
```

val customer = Customer(1, "Monthol", 1978)
### The getter versus property default value (from Moskala et. Wojda)
Property value with customer getter is calculated each time property is accessed.
```
class Fruit(var weight: Double) {
           val heavy             // 1
           get() = weight > 20
}
       //usage
       var fruit = Fruit(7.0)
       println(fruit.heavy) //prints: false
       fruit.weight = 30.5
       println(fruit.heavy) //prints: true

```
Property value with default parameter is calculated once and does not changed.
```
class Fruit(var weight: Double) {
           val isHeavy = weight > 20
       }
       var fruit = Fruit(7.0)
       println(fruit.isHeavy) // Prints: false
       fruit.weight = 30.5
       println(fruit.isHeavy) // Prints: false
```
Declaring properties is not allowed for secondary constructors. So declare it in the class body, and we can initialize it in the secondary constructor body.

When a primary constructor is defined, every secondary constructor must call the primary constructor implicitly (via another secondary constructor) or explicitly.
```
class Customer (val id: String, var name: String) {
    init {      //init block is part of primary constructor?
        name = name.toUpperCase()
    }
    
    constructor (id: String) : this(id, "") {   // no property defining allow here (no `val` or `var`) at the secondary constructor
    
    }
```

`@JvmOverload` annotation informs the compiler to generate in additional JVM bytecode constructor overload for every parameter with a default value.

## 19 Visibility Modifiers
There are 4 visibility modifiers in Kotlin
public (default)
private (top level/class) visible within the same file(top level) or within class(class)
internal (top level/class) visible in the same module (Gradle module, Maven module, IntelliJ module,...)
protected (class only) visible within class and its subclasses

## 23 Type Casting
Smart-casting is the ability of the compiler to check that it is a certain type and smart-cast to it

```
open class Persion {
}

class Employee : Person() {
    fun vacationDays(days: Int) {
        if (days < 60) {
	    println("You need more vacation.")
	}
    }

class Contractor : Person() {
}

fun hasVacations(obj: Person) {
    if (obj is Employee) {
        obj.vacationDays(20) \\obj is smart-casted to Employee, it is now highlighted in green and auto-complete available for vacationDays()
    }
}

fun main(args: Array<String>) {
} 
```
There is no implicit cast in Kotlin.
```
var input: Any = 10

fun main(args: Array<String>) {
    val str = input as String
    println(str.length) // Class cast exception.
}
```
So safe cast it with `as?`
```
```
var input: Any = 10

fun main(args: Array<String>) {
    val str = input as? String
    println(str.length) // Class cast exception.
}
```

In intelliJ
#### Flatten or expand package folder trees
click setting on top of project plane.
#### Navigating to Recent File
View | Recent Files or press Ctrl+E
#### Override functions in java class
place cursor at class name and press `ctrl`+`Ent`
#### Comment out text
`cmd`+`/`
