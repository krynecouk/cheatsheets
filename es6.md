Block-Scoped Declarations
-------------------------
```js
var a = 2;

{
	let a = 3;
	console.log( a );	// 3
}

console.log( a );		// 2
```

Sources
------
[1]: [You Dont't Know JS: ES6 & Beyond](https://github.com/getify/You-Dont-Know-JS/blob/master/es6%20%26%20beyond/ch2.md)
[2]: [esfiddle](https://esfiddle.net)
