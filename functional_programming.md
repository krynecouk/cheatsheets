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


Sources
-------
[1]: [Mostly Adequate Guide to Functional Programming]e(https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)
