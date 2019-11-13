## Boolean

`let isDone: boolean = false;`

## Number

```ts
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

## String

```ts
let fullName: string = `Bob Bobbington`;
```

## Array
`let list: number[] = [1, 2, 3];`

## Tuple

> Array with fixed number of elements and types.

```ts
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK

type Drink = [string, boolean, number];
const pepsi: Drink = ['brown', true, 40];
```

## Enum

```ts
enum Color {Red, Green, Blue}
let c: Color = Color.Green;

enum Color {Red = 1, Green, Blue}
let colorName: string = Color[2];

console.log(colorName); // Displays 'Green' as its value is 2 above
```

## Any

```ts
let notSure: any = 4;
notSure.ifItExists(); // okay, ifItExists might exist at runtime
notSure.toFixed(); // okay, toFixed exists (but the compiler doesn't check)

let prettySure: Object = 4;
prettySure.toFixed(); // Error: Property 'toFixed' doesn't exist on type 'Object'.
```

## Void

> Oposite of `any`.

```ts
function warnUser(): void {
    console.log("This is my warning message");
}
```

## Null and Undefined

```ts
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```

## Never

> Return type for a function expression or an arrow function expression that always throws an exception or one that never returns.

```ts
function error(message: string): never {
    throw new Error(message);
}
```

## Object

```ts
declare function create(o: object | null): void;

create({ prop: 0 }); // OK
create(null); // OK

create(42); // Error
create("string"); // Error
create(false); // Error
create(undefined); // Error
```

## Function

```ts
const add = (a: number, b: number) : number => a + b;
```

## Interface

```ts
interface Vehicle {
    name: string;
    year: number;
    broken: boolean;
    summary(): string;
}

const civic: Vehicle = {
   name: 'civic', // OK
   year: 2000, // OK
   broken: 'not', // ERROR
   summary: () => 'its ko'
}
```

## Class

- public (default)
- private (only in class)
- protected (only in class and child)

```ts
class Car extends Vehicle {}

// this
class Foo {
   color: string;

   constructor(color: string) {
      this.color = color;
   }
}

// same as that
class Foo {
   constructor(public color: string) { }
}
```

## Optional Properties

```ts
interface SquareConfig {
    color?: string;
    width?: number;
}
```

## Casting

```ts
let strLength: number = (<string>someValue).length;
let strLength: number = (someValue as string).length;
```

## Flexible Types

```ts
let numberAboveZero: boolean | number = false;
```


## Destructuring

```ts
const { age } : { age: number } = profile;
```

## Implicit check

> No need to specify `implements`.

```ts
interface Mappable {
    location: {
        lat: number;
        lng: number;
    }
}

const foo = (mappable: Mappable) => {...}

foo({location: { lat: 20, lng: 30 }}); // OK
```

## Abstract class

```ts
abstract class Foo {
    abstract bar(): string;
}
```

## Static

```ts
class Foo {
    static foo(): void;
}
```

## Generic class

```ts
class Foo<T> {
   constructor(public collection: T[]) {}
   get(index: number) : T { 
      return this.collection[index];
   }
}

const arr = new Foo(['a', 'b', 'c']); // OK - type inference
```

## Generic functions

```ts
const foo = <T>(bar: T) => { 
    console.log(bar);
}
```

## Decorators

```ts
function f() {
    console.log("f(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("f(): called");
    }
}

function g() {
    console.log("g(): evaluated");
    return function (target, propertyKey: string, descriptor: PropertyDescriptor) {
        console.log("g(): called");
    }
}

class C {
    @f()
    @g()
    method() {}
}

new C().method();

// f(): evaluated
// g(): evaluated
// g(): called
// f(): called
```

## Intersection Types

```ts
type Person = Person & Serializable & Loggable;
```

## Discriminated Unions

```ts
type Shape = Square | Rectangle | Circle;
```

## Conditional Types

```ts
T extends U ? X : Y
```

## Type predicates

> It will cast `pet` (if it is possible) to the `Fish`.

```ts
function isFish(pet: Fish | Bird): pet is Fish {
    return (pet as Fish).swim !== undefined;
}
```

## `in` operator

```ts
function move(pet: Fish | Bird) {
    if ("swim" in pet) {
        return pet.swim();
    }
    return pet.fly();
}
```

## Type Alias

> Similar to interfaces, but can name primitives, unions, tuples, and any other types that you’d otherwise have to write by hand.

```ts
type LinkedList<T> = T & { next: LinkedList<T> };
```

## String literal types

> String literal types allow you to specify the exact value a string must have.

```ts
type Easing = "ease-in" | "ease-out" | "ease-in-out";
```

## Numeric Literal Types

```ts
function rollDice(): 1 | 2 | 3 | 4 | 5 | 6 {
    // ...
}
```

## Readonly props and types

```ts
interface PersonReadonly {
    readonly name: string;
    readonly age: number;
}
```

## `keyOf`

```ts
interface Todo {
  id: number;
  text: string;
  due: Date;
}

type TodoKeys = keyof Todo; // "id" | "text" | "due"

function prop<T, K extends keyof T>(obj: T, key: K) {
  return obj[key];
}

const todo = {
  id: 1,
  text: "Buy milk",
  due: new Date(2016, 11, 31)
};

const id = prop(todo, "id");     // number
const text = prop(todo, "text"); // string
const due = prop(todo, "due");   // Date
```

## Index type

```ts
interface User {
    events: { [key: string]: Callback[] } = {}
}
```

> `User` has `events`. `events` is object with string keys and values of `Callback`.

## Optional chaining

> Immediately stop execution some expressions encounters `null` or `undefined`.

```ts
// Before
let x = (foo === null || foo === undefined) ?
    undefined :
    foo.bar.baz();

// Now
let x = foo?.bar.baz();
```

```ts
// Before
if (foo && foo.bar && foo.bar.baz) {
    // ...
}

// After-ish
if (foo?.bar?.baz) {
    // ...
}
```

```ts
// Before 
if (log != null) {
	log(`Request started at ${new Date().toISOString()}`);
}

// Now
log?.(`Request finished at at ${new Date().toISOString()}`);
```

## Nullish Coalescing

```ts
let x = foo ?? bar();
```

> Call `bar()` when foo is `null` or `undefined`.

## Assertions functions

> Throws an error if assert function is `false`.

```ts
function multiply(x, y) {
    assert(typeof x === "number");
    assert(typeof y === "number");

    return x * y;
}
```

## Sources
[1]: [Typescript Docs](http://www.typescriptlang.org/docs/home.html)
[2]: [Typescript Playground](http://www.typescriptlang.org/play/)
