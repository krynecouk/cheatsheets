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
// double function composition (right to left)
const compose = (f, g) => x => f(g(x));					
```

```js
// multiple function compositions (right to left)
const compose = (...fns) => x => fns.reduceRight((y, f) => f(y), x);
```

```js
// multiple function compositions (left to right)
const pipe = (...fns) => x => fns.reduce((y, f) => f(y), x); 	
```

```js
// example
const toUpperCase = x => x.toUpperCase();
const exclaim = x => `${x}!`;
const shout = compose(exclaim, toUpperCase);

shout('send in the clowns'); // "SEND IN THE CLOWNS!"
```

Pointfree
---------
> Functions that never mention the data upon which they operate.

```js
// not pointfree because we mention the data: word
const snakeCase = word => word.toLowerCase().replace(/\s+/ig, '_');

// pointfree
const snakeCase = compose(replace(/\s+/ig, '_'), toLowerCase);
```

Category Theory
---------------
```yml
collection with the following components:
- A collection of objects 			# String, Boolean, Number, Object etc.
- A collection of morphisms			# standard every day pure functions
- A notion of composition on the morphisms 	# `compose`
- A distinguished morphism called identity	# `const id = x => x;`
```


Sources
-------
[1]: [Mostly Adequate Guide to Functional Programming]e(https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)
[2]: [Curry and Function Composition](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)
[3]: [ES Fiddle](https://esfiddle.net)
