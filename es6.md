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

Sources
------
[1]: [You Dont't Know JS: ES6 & Beyond](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md)
[2]: [esfiddle](https://esfiddle.net)
