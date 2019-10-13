## Reading Object Properties
### `R.prop`

`s → {s: a} → a | Undefined`

```js
R.prop('x', {x: 100}); //=> 100
R.prop('x', {}); //=> undefined
R.compose(R.inc, R.prop('x'))({ x: 3 }) //=> 4
```

### `R.propEq`

`String → a → Object → Boolean`

```js
const kids = [abby, fred, rusty, alois];
const hasBrownHair = R.propEq('hair', 'brown');
R.filter(hasBrownHair, kids); //=> [fred, rusty]
```

### `R.path`

`[Idx] → {a} → a | Undefined`

> Retrieve the value at a given path.

```js
R.path(['a', 'b'], {a: {b: 2}}); //=> 2
R.path(['a', 'b'], {c: {b: 2}}); //=> undefined
```

### `R.pathEq`

`[Idx] → a → {a} → Boolean`

```js
const users = [ user1, user2, user3 ];
const isFamous = R.pathEq(['address', 'zipCode'], 90210);
R.filter(isFamous, users); //=> [ user1 ]
```

### `R.pick`

`[k] → {k: v} → {k: v}`

> Returns a partial copy of an object containing only the keys specified.

```js
R.pick(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1, d: 4}
R.pick(['a', 'e', 'f'], {a: 1, b: 2, c: 3, d: 4}); //=> {a: 1}
```

### `R.pickBy`

`((v, k) → Boolean) → {k: v} → {k: v}`

```js
const isUpperCase = (val, key) => key.toUpperCase() === key;
R.pickBy(isUpperCase, {a: 1, b: 2, A: 3, B: 4}); //=> {A: 3, B: 4}
```

### `R.keys`

`{k: v} → [k]`

### `R.values`

`{k: v} → [v]`

## Manipulating Object Properties

### `R.assoc`

`String → a → {k: v} → {k: v}`

> Creates shallow copy of an object with an additional attribute. 

```js
R.assoc('c', 3, {a: 1, b: 2}); //=> {a: 1, b: 2, c: 3}
```

### `R.dissoc`

`String →  {k: v} → {k: v}`

> Returns a new object that does not contain a prop property.

```js
R.dissoc('b', {a: 1, b: 2, c: 3}); //=> {a: 1, c: 3}
```

### `R.assocPath`

`[Idx] → a → {a} → {a}`

> Creates shallow copy of an object with an additional attribute on specified path.

```js
R.assocPath(['a', 'b', 'c'], 42, {a: {b: {c: 0}}}); //=> {a: {b: {c: 42}}}

// Any missing or non-object keys in path will be overridden
R.assocPath(['a', 'b', 'c'], 42, {a: 5}); //=> {a: {b: {c: 42}}}
```

### `R.dissocPath`

`[Idx] → {k: v} → {k: v}`

```js
R.dissocPath(['a', 'b', 'c'], {a: {b: {c: 42}}}); //=> {a: {b: {}}}
```

### `R.omit`

`[k] → {k: v} → {k: v}`

> Removes several properties at once.

```js
R.omit(['a', 'd'], {a: 1, b: 2, c: 3, d: 4}); //=> {b: 2, c: 3}
```

## Transorming Object Properties

### `R.evolve`

`{k: (v → v)} → {k: v} → {k: v}`

```js
const tomato = {firstName: '  Tomato ', data: {elapsed: 100, remaining: 1400}, id:123};
const transformations = {
  firstName: R.trim,
  lastName: R.trim, // Will not get invoked.
  data: {elapsed: R.add(1), remaining: R.add(-1)}
};
R.evolve(transformations, tomato); //=> {firstName: 'Tomato', data: {elapsed: 101, remaining: 1399}, id:123}
```

## Sources
[1]:[Ramda](https://ramdajs.com/docs/)
[2]:[Thinking in Ramda](http://randycoulman.com/blog/categories/thinking-in-ramda/)
[3]:[Ramda REPL](https://ramdajs.com/repl/)
[4]:[Why Ramda](https://fr.umio.us/why-ramda/)

