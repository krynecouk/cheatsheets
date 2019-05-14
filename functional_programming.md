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

Map's composition law
---------------------
```js
compose(map(f), map(g)) === map(compose(f, g));
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

Hindley-Milner
--------------
```js
// head :: [a] -> a
const head = xs => xs[0];

// filter :: (a -> Bool) -> [a] -> [a]
const filter = curry((f, xs) => xs.filter(f));

// reduce :: (b -> a -> b) -> b -> [a] -> b
const reduce = curry((f, x, xs) => xs.reduce(f, x));

```
> `a -> b` can be any type `a` to any type `b`, but `a -> a` means it has to be the same type. For example, `id` may be `String -> String` or `Number -> Number`, but not `String -> Bool`.

Narrowing the Possibility
-------------------------
> `parametricity` property states that a function will act on all types in a uniform manner.

Sources
-------
[1]: [Mostly Adequate Guide to Functional Programming]e(https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)
[2]: [Curry and Function Composition](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)
[3]: [ES Fiddle](https://esfiddle.net)
[4]: [So You Still Don't Understand Hindley-Milner](http://akgupta.ca/blog/2013/05/14/so-you-still-dont-understand-hindley-milner/)
[5]: [Hindley-Milner StackOverflow](https://stackoverflow.com/questions/12532552/what-part-of-hindley-milner-do-you-not-understand)
