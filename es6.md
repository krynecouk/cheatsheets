Block-Scoped Declarations
-------------------------
```js
var a = 2;

{
	let a = 3;
	console.log( a );		// 3
}

console.log( a );			// 2
```

Block-Scoped Functions
----------------------
```js
{
	foo();				// works!

	function foo() {
		// ..
	}
}

foo();					// ReferenceError
```


`let` + `for`
-------------
```js
var funcs = [];

for (let i = 0; i < 5; i++) {
	funcs.push( function(){
		console.log( i );
	} );
}

funcs[3]();				// 3
```

`const`
-------
```js
{
	const a = 2;
	console.log( a );		// 2

	a = 3;				// TypeError!
}
```

`spread` (expand array) operator
--------------------------------
```js 

n foo(x,y,z) {
	console.log( x, y, z );
}

foo( ...[1,2,3] );			// 1 2 3
```

or

```js
var a = [2,3,4];
var b = [ 1, ...a, 5 ];

console.log( b );			// [1,2,3,4,5]
```

`rest` (gather array) operator
------------------------------
```js
function foo(...args) {
	console.log( args );
}

foo( 1, 2, 3, 4, 5);			// [1,2,3,4,5]
```

Default Parameter Values
-------------------------
```js
function foo(x = 11, y = 31) {
	console.log( x + y );
}
```

Default Parameter Expressions
-----------------------------
```js
function foo(x = y + 3, z = bar( x )) {
	console.log( x, z );
}
```

Destructing
-----------
```js
function foo() {
	return [1,2,3];
}

function bar() {
	return {
		x: 4,
		y: 5,
		z: 6
	};
}
```

```js
var [ a, b, c ] = foo();
var { x: bam, y: baz, z: bap } = bar();

console.log( a, b, c );			// 1 2 3
console.log( bam, baz, bap );		// 4 5 6
console.log( x, y, z );			// ReferenceError
```

```js
var a, b, c, x, y, z;

[a,b,c] = foo();
( { x, y, z } = bar() );

console.log( a, b, c );			// 1 2 3
console.log( x, y, z );			// 4 5 6
```

```js
var [,,c,d] = foo();
var { w, z } = bar();

console.log( c, z );			// 3 6
console.log( d, w );			// undefined undefined
```

**TIP:** Think of it as a `<source>:<target>` pattern

Nested Destructing
------------------

```js
var App = {
	model: {
		User: function(){ .. }
	}
};

var { model: { User } } = App;		// instead of var user = App.model.User
```

Parameters Destructing
----------------------
```js
function foo( { x, y } ) {
	console.log( x, y );
}

foo( { y: 1, x: 2 } );			// 2 1
foo( { y: 42 } );			// undefined 42
foo( {} );				// undefined undefined
```

Computed Property Names
-----------------------
```js
var prefix = "user_";

var o = {
	baz: function(..){ .. }
};

o[ prefix + "foo" ] = function(..){ .. };
```

Template Literals
-----------------
```js
var name = 'Johnny'
var hello = 
`Hello
${name}!`

console.log( name ); // Hello Johnny!

Tagged Template Literals
------------------------
```js
function foo(strings, ...values) {
	console.log( strings );
	console.log( values );
}

var desc = "awesome";

foo`Everything is ${desc}!`;
// [ "Everything is ", "!"]
// [ "awesome" ]
```
**TIP:**: Think of it as foo(`Everything is ${desc}!`) before interpolation.

Arrow Functions
---------------
```js
var foo = (x,y) => x + y;
```

`for..of` Loops
---------------
```js
var a = ["a","b","c","d","e"];

for (var idx in a) {
	console.log( idx );
}
// 0 1 2 3 4

for (var val of a) {
	console.log( val );
}
// "a" "b" "c" "d" "e"
```
**TIP:** `for..in` loops keys, `for..of` loops values.

Symbol
------
```js
var sym = Symbol( "some optional description" );

typeof sym;			// "symbol"
```

## Import
> Used to import bindings which are exported by another module. Can be member or default.

-- default import		: imports `export default` from module 
(e.g. `import React from 'react'`)
-- member import 		: imports `export` from module 
(e.g. `import { Component } from 'react'`)

### Import all module
```js
import * as myModule from '/modules/my-module.js';
```

### Import a single export
```js
import {myExport} from '/modules/my-module.js';
```

### Import multiple exports 
```js
import {foo, bar} from '/modules/my-module.js';
```

### Import export with alias
```js
import {foo as f} from 'my-module'; // my-module is a dependency name
```

## `import` vs `require`
- `import` is a ES2015 modules system
- `require` is a CommonJS modules system

```js
val React = require('react');
```

## `this`
> Value of `this` depends on how function is called (runtime binding).

> `bind` method can change the `this` value (only once!).

> arrow functions has `this` always same where was created (no matter by who is called).

> More info [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

## Solving `this` problem
### `bind`
```js
class Foo {
        constructor() {
                this.fun = this.fun.bind(this);
        }
}
```

### arrow fun
```js
class Foo {
        foo = () => console.log(this);
}
```

### arrow fun in `JSX`
```js
<form onSubmit={() => console.log(this)}>
```

## `async`/`await`
> `async`/`await` is a new way to write asynchronous code. Previous alternatives for asynchronous code are callbacks and promises.

> `async`/`await` is actually just syntax sugar built on top of promises.

```js
const makeRequest = () =>
  getJSON()
    .then(data => {
      console.log(data)
      return "done"
    })

makeRequest()
```
=> 
```js
const makeRequest = async () => {
  console.log(await getJSON())
  return "done"
}

makeRequest()
```

> `await` waits for async method. Must be used insinde of `async` method.

## Appendix
### ES6 config and destroy pattern
```js
const FooConfig = {
        foo: {
                a: 'a',
                b: 'b'
        }
}

const {a, b} = FooConfig[input];
```

### Spread with new element
```js
const newArr = [...oldArr, newElement];
```

Sources
------
[1]: [You Dont't Know JS: ES6 & Beyond](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md)
[2]: [esfiddle](https://esfiddle.net)
[3]: [Async/Await tutorial](https://dev.to/gafi/7-reasons-to-always-use-async-await-over-plain-promises-tutorial-4ej9)
