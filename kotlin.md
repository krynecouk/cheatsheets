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

## Sources
[1]: [Kotlin in Action](https://www.amazon.com/Kotlin-Action-Dmitry-Jemerov/dp/1617293296/ref=cm_cr_arp_d_product_top?ie=UTF8)
