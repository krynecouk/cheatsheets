## Expression vs Statements
> **expression** has a value.
> **statement** doesn't have its own value.
> In Kotlin, most control structures, except for the loops (`for`, `do`, and `do/while`) are expressions.

```kotlin 
fun max(a: Int, b: Int): Int = if (a > b) a else b
```

## `val` x `var`
- `val`(ue) ~ `final` in Java (Immutable)
- `var`(iable) ~ el diable (Mutable)

## Strint templates
```kotlin
fun main(args: Array<String>) {
	println("Hello, ${if (args.size > 0) args[0] else "someone"}!")
}
```

## Class Properties
```kotlin
class Person(
	val name: String,	// read-only property; generates getter
	var isMarried: Boolean	// writeable property; generates getter and setter 
)
```

```kotlin
>>> val person = Person("Bob", true)
>>> println(person.name)
Bob
>>> println(person.isMarried)
true
```

## Custom Accessors
```kotlin
class Rectangle(val height: Int, val width: Int) {
	val isSquare: Boolean
	get() = height == weight
```

## `enum class`
```kotlin
enum class Color(val r: Int, val g: Int, val b: Int) {
	RED(255, 0, 0);
}
```

## `when`
```kotlin
fun getWarmth(color: Color) = when(color) {
	RED, ORANGE, YELLOW -> "warm"
	GREEN -> "neutral"
}
	
```kotlin
fun mixOptimized(c1: Color, c2: Color) =
	when {
		(c1 == RED && c2 == YELLOW) ||
		(c1 == YELLOW && c2 == RED) -> ORANGE
		(c1 == YELLOW && c2 == BLUE) ||
		(c1 == BLUE && c2 == YELLOW) -> GREEN
	else -> throw Exception("Dirty color")
}
```

## Smart Cast
```kotlin
if (x is String) x.toUpperCase()
```

## `for` `in` 
```kotlin
>>> for (i in 100 downTo 1 step 2) {
	print(fizzBuzz(i))
}
```

```kotlin
for ((letter, binary) in binaryReps) {
	println("$letter = $binary")
}
```

```kotlin
fun isLetter(c: Char) = c in 'a'..'z' || c in 'A'..'Z'
fun isNotDigit(c: Char) = c !in '0'..'9'
```

## Exceptions
> No checked exceptions.
> `try-catch` and `throw` are expressions.
```kotlin
fun readNumber(reader: BufferedReader) {
    val number = try {
        Integer.parseInt(reader.readLine())
    } catch (e: NumberFormatException) {
        null
    }
    println(number)
}
```

## Named arguments
```kotlin
joinToString(collection, separator = " ", prefix = " ", postfix = ".")
```

## Default parameter values
```kotlin
fun <T> joinToString(
        collection: Collection<T>,
        separator: String = ", ",
        prefix: String = "",
        postfix: String = ""
): String {}
```
> No overloading in Kotlin.

## Extension functions
```kotlin
fun String.lastChar(): Char = this.get(this.length - 1)
```
-> 
```kotlin
fun String.lastChar(): Char = get(length - 1)
```

## Extension functions and overriding
> Same as static method overriding in Java - depends on *declared* type, not implemented.
```kotlin
fun View.showOff() = println("I'm a view!")
fun Button.showOff() = println("I'm a button!")
>>> val view: View = Button()
>>> view.showOff()
I'm a view!
```

## Extension properties
```kotlin
var StringBuilder.lastChar: Char
    get() = get(length - 1)
    set(value) {
        this.setCharAt(length - 1, value)
    }
```

## `vararg` and spread 
```kotlin
fun listOf<T>(vararg values: T): List<T> { ... }
```

```kotlin
fun main(args: Array<String>) {
	val list = listOf("args: ", *args)
	println(list)
}
```

## `infix` functions
```kotlin
infix fun Any.to(other: Any) = Pair(this, other)

val map = mapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
```

## destructing variables
```kotlin
val (number, name) = 1 to "one"
```

## `interface`
```kotlin
interface Clickable {
	fun click()
	fun showOff() = println("I'm clickable!")
}
```
> Like ordinary class but **without a state**.

## `open class` and `open fun`
```kotlin
open class RichButton : Clickable {...}
```
```kolin
open fun stopAnimating()
```
> In Kotlin, every class is `public final` by default. In order to be able to extend class, you have to mark  `open` class  and every function or property.

## `internal class`
```kotlin 
internal class Foo {...}
```
> Visible only in the module.

## `inner class`
```kotlin
class Outer {
	inner class Inner {...}
}
```
> In Kotlin, every nested class is `static` by default. In order to contain reference to the `Outer` class, you have to mark it `inner`. 

## `sealed class`
```kotlin
sealed class Expr {
	class Num(val value: Int) : Expr()
	class Sum(val left: Expr, val right: Expr) : Expr()
}
```
> All subclasses must be nested.

## Constructor
### Primary Constructor
> Declared outside of the class body.

```kotlin
class User(val nickname: String)
```
```kotlin
class TwitterUser(nickname: String) : User(nickname) { ... }
```
```kotlin
class Secretive private constructor() {}
```

### Secondary Constructor
> Declared in the class body.

```kotlin
class MyButton : View {
	constructor(ctx: Context) : super(ctx) {...}
}
```

## Interface properties
```kotlin
interface User {
	val nickname: String
}
```
> Classes implementing the `User` interface need to provide a way to obtain the value of nickname.

```kotlin
class PrivateUser(override val nickname: String) : User
```

```kotlin
class SubscribingUser(val email: String) : User {
    override val nickname: String
        get() = email.substringBefore('@') )
}
```
```kotlin
class FacebookUser(val accountId: Int) : User {
    override val nickname = getFacebookName(accountId)
}
```

## Backing field
```kotlin
class User(val name: String) {
	var address: String = "unspecified"
		set(value: String) {
			println("""$field" -> "$value".""")
			field = value
		}
}
```

## `==` and `===`
- `==` value comparison (`equals`)
- `===` reference comparison 



## Sources
[1]: [Kotlin in Action](https://www.amazon.com/Kotlin-Action-Dmitry-Jemerov/dp/1617293296/ref=cm_cr_arp_d_product_top?ie=UTF8)
