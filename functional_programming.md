Function
--------
> A function is a special relationship between values: Each of its input values gives back exactly one output value.

```js
const toLowerCase = {
  A: 'a',
  B: 'b',
  C: 'c',
  D: 'd',
  E: 'e',
  F: 'f',
};
toLowerCase['C']; 							// 'c'
```

First Class Functions
---------------------
```js
// NOTOK
const split = (delimiter, what) => what.split(delimiter);
const words = str => split(' ', str);
console.log(words('foo bar'));						// ["foo", "bar"]
// OK
const split = (delimiter) => (what) => what.split(delimiter);
const words = split(' ');
console.log(words('foo bar'));						// ["foo", "bar"]
```

Currying
--------
```js
const match = s => what => what.match(s);
const matchR = match(/r/g);

console.log(matchR('tru'))    						// ["r"]
```
> Currying does exactly this: each single argument returns a new function expecting the remaining arguments.

Composing
---------
> Composition feels like function husbandry. You, breeder of functions, select two with traits you'd like to combine and mash them together to spawn a brand new one.

```js
const compose = (f, g) => x => f(g(x));					// double function compositions (not associative - right to left)
```

```js
const compose = (...fns) => x => fns.reduceRight((y, f) => f(y), x);	// multiple function compositions (not associative - right to left)
```

```js
const pipe = (...fns) => x => fns.reduce((y, f) => f(y), x); 		// multiple function compositions (not associative - left to right)
```

```js
const compose = (...fns) => (...args) => fns.reduceRight((res, fn) => [fn.call(null, ...res)], args)[0];	// multiple function compositions (associative)
```

```js
// example
const toUpperCase = x => x.toUpperCase();
const exclaim = x => `${x}!`;
const shout = compose(exclaim, toUpperCase);

shout('send in the clowns'); // "SEND IN THE CLOWNS!"
```

Sources
-------
[1]: [Mostly Adequate Guide to Functional Programming]e(https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)
[2]: [Curry and Function Composition](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)
