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



## Sources
[1]: [Kotlin in Action](https://www.amazon.com/Kotlin-Action-Dmitry-Jemerov/dp/1617293296/ref=cm_cr_arp_d_product_top?ie=UTF8)
