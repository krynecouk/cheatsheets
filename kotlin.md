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

## `data class`
```kotlin
data class Client(val name: String, val postalCode: Int)
```
> Automatically generates `equals`, `hashcode` and `toString` methods.

## Delegation `by`
``` kotlin
class DelegatingCollection<T>(innerList: Collection<T> = ArrayList<T>()) : Collection<T> by innerList {}
```
> Decorator pattern without boilerplate.

## `object`
```kotlin
object Payroll {
    val allEmployees = arrayListOf<Person>()
    fun calculateSalary() {
        for (person in allEmployees) {
            ...
        }
    }
}
```
> Singleton object.

## `companion object`
```kotlin
class User private constructor(val nickname: String) {
    companion object {
        fun newSubscribingUser(email: String) =
                User(email.substringBefore('@'))

        fun newFacebookUser(accountId: Int) =
                User(getFacebookName(accountId))
    }
}
```
> Top level `fun` are recommended. But top-level functions can’t access private members of a class. Thus, if you need to write a function that can be called without having a class instance but needs access to the internals of a class, you can write it as a member of an object declaration inside that class.

## `companion object` extension
```kotlin
class Person(val firstName: String, val lastName: String) { companion object {} }
fun Person.Companion.fromJSON(json: String): Person {}
val p = Person.fromJSON(json)
```

## anonymous `object`
```kotlin
window.addMouseListener(
        object : MouseAdapter() {
            override fun mouseClicked(e: MouseEvent) {}
        }
}
``` 

## lambdas
```kotlin
people.maxBy( {p: Person -> p.age } )
people.maxBy { p: Person -> p.age }
people.maxBy { p -> p.age }
```

> Kotlin allows to access non-final variables and modify them in a lambda (`captured` variable).

## Member references
```kotlin
val getAge = Person::age
```

```kotlin
fun salute() = println("Salute!")
>>> run(::salute)
```

## Lazy collection operations: sequences
```kotlin
people.map(Person::name).filter { it.startsWith("A") }
```
> Eager collection -> creates intermediate collections after `map` and `filter` because every element is `mapped` and `filtered`.

```kotlin
people.asSequence()
	.map(Person::name)
	.filter { it.startsWith("A") }
	.toList()
```
> Lazy sequence -> creates only output collection because each element one by one is first `mapped` then `filtered`.  Preferable when large collections.

## Lambdas with receivers: “with” and “apply”
### `with`
```kotlin
fun alphabet() = with(StringBuilder()) {
	for (letter in 'A'..'Z') {
		append(letter)
	}
	append("\nNow I know the alphabet!")
	toString()
}
```
> `with` is basically a `fun(T, lambda)`.

### `apply`
```kotlin
fun alphabet() = StringBuilder().apply {
    for (letter in 'A'..'Z') {
        append(letter)
    }
    append("\nNow I know the alphabet!")
}.toString()
```
> Basically the same as `with` but with return type of `receiver` (builder).

## Kotlin type system
### Nullable type
```kotlin
fun strLenSafe(s: String?): Int = if (s != null) s.length else 0
```
> Type or `null`

### Safe call operator: `?.`
```kotlin
if (s != null) s.toUpperCase() else null
```
=>
```kotlin
s?.toUpperCase()
```
### Elvis oprator `?:`
```kotlin
val t: String = s ?: ""
```

```kotlin
val t: String = s ?: throw IllegalArgumentException("Empty String")
```

### Safe cast `as?`
```kotlin
val otherPerson = o as? Person ?: return false
```

### Not-null assertions `!!`
```kotlin
val sNotNull: String = s!!
```

### `let`
```kotlin
if (email != null) sendEmailTo(email)
```
=>
```kotlin
email?.let { email -> sendEmailTo(email) }
```

### Late-initialized properties `lateinit`
```kotlin
private var myService: MyService? = null
```
=> 
```kotlin
private lateinit var myService: MyService
```

### Nullable extensions
```kotlin
fun String?.isNullOrBlank(): Boolean = this == null || this.isBlank()
```

### Nullability of type parameters
```kotlin
fun <T> printHashCode(t: T) {
	println(t?.hashCode())
}
```

> By default, all type parameters of functions and classes in Kotlin are nullable.

## Primitive types
- Integer types: `Byte`, `Short`, `Int`, `Long`
- Floating-point number types: `Float`, `Double`
- Character type: `Char`
- Boolean type: `Boolean`
- void: `Unit`
- <no return type>: `Nothing`

## Collections & Arrays
- `kotlin.collections.Collection`: read-only collections (`size`, `iterator()`, `contains()`)
- `kotlin.collections.Mutable-Collection`: mutable collections (`add()`, `remove()`, `clear()`)
- `kotlin.collections.Immutable-Collection`: not yet implemented
- `Array<T>`: array of `T` wrappers, in order to use array of primitives, use specific impl e.g. `IntArray`

## Sources
[1]: [Kotlin in Action](https://www.amazon.com/Kotlin-Action-Dmitry-Jemerov/dp/1617293296/ref=cm_cr_arp_d_product_top?ie=UTF8)
