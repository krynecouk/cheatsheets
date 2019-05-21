Named Types
-----------
```js
// charAt :: (Number, String) -> String
const charAt = (pos, word) => word.charAt(pos);
charAt(9, 'mississippi'); //=> 'p'
```

Lists of Values
---------------
```js
// addToAll :: (Number, [Number]) -> [Number]
const addToAll = (val, nbrs) => nbrs.map(nbr => nbr + val);
addToAll(10, [2, 3, 5, 7]); //=> [12, 13, 15, 17]
```

Functions
---------
```js
// applyCalculation :: ((Number -> Number), [Number]) -> [Number]
const applyCalculation = (calc, nbrs) => nbrs.map(nbr => calc(nbr));
applyCalculation(n => 3 * n + 1, [1, 2, 3, 4]); //=> [4, 7, 10, 13]
```

Currying
--------
```js
// calculateTax :: Number -> Number -> Number
const calculateTax = R.curry((rate,  base) =>
    Math.round(100 * base + base * rate) / 100);
```

Type Variables
--------------
```js
// map :: (a -> b) -> [a] -> [b]
```

Parameterized Types
-------------------
```js
// makeBox :: Number -> Number -> Number -> [a] -> Box a
const makeBox = curry((height, width, depth, items) => /* ... */);
```
> There does not have to be just a single type parameter. We might have a `Dictionary` type that is parameterized over both the type of the keys and the type of the values it uses. This could be written `Dictionary k v`.

Source
------
[1]: [Ramda type signatures](https://github.com/ramda/ramda/wiki/Type-Signatures)
