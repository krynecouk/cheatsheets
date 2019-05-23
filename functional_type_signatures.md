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

Type Aliases
------------
```js
// toUrl :: User Name u => Url -> u -> Url
//     Name = String
//     Url = String
const toUrl = curry((base, user) => base + user.name.toLowerCase().replace(/\W/g, '-'));
toUrl('http://example.com/users/', {name: 'Fred Flintstone', age: 24});
//=> 'http://example.com/users/fred-flintstone'
```
> If we had a parameterized type `User String`, where the `String` was meant to represent a name, and we wanted to be more specific about the type of `String` that is represented when generating a URL, we could create a type alias `User Name u`.

Type Constraints
----------------
```js
// maximum :: Ord a => [a] -> a
const maximum = vals => reduce(
  (curr, next) => next > curr ? next : curr, head(vals), 
  tail(vals)
)
maximum([3, 1, 4, 1]); //=> 4
```
> `Ord a ⇒ [a] → a` says that maximum takes a collection of elements of some type, but that type must adhere to `Ord`.

Multiple Signatures
-------------------
```js
// getIndex :: a -> [a] -> Number
//          :: String -> String -> Number
const getIndex = curry((needle, haystack) => haystack.indexOf(needle));
getIndex('ba', 'foobar'); //=> 3
```

Simple Objects
--------------
```js
// keys :: {k: v} -> [k]
keys({a: 86, b: 75, c: 309}); //=> ['a', 'b', 'c']
```
> Or just `Object`.

Records
--------
```js
// display :: {name: String, age: Number} -> (String -> Number -> String) -> String
const display = curry((person, formatter) => 
                      formatter(person.name, person.age));
const formatter = (name, age) => name + ', who is ' + age + ' years old.';
display({name: 'Fred', age: 25, occupation: 'crane operator'}, formatter);
//=>  "Fred, who is 25 years old."
```

Example
-------
```js
Lens s a = Functor f => (a -> f a) -> s -> f s
```
> This tells us that the type `Lens` is parameterized by two generic variables, `s`, and `a`. We know that there is a constraint on the type of the `f` variable used in a `Lens`: it must be a `Functor`. With that in mind, we see that a `Lens` is a curried function of two parameters, the first being a function from a value of the generic type a to one of the parameterized type `f a`, and the second being a value of generic type `s`. The result is a value of the parameterized type `f s`. But what does it do? We don't know. We can't know. Our type signatures tell us a great deal about a function, but they don't answer questions about what a function actually does. We can assume that somewhere the map method of `f a` must be called, since that is the only function defined by the type `Functor`, but we don't know how or why that map is called. Still, we know that a `Lens` is a function as described, and we can use that to guide our understanding of over.

```js
const headLens = R.lensIndex(0);
R.over(headLens, R.toUpper, ['foo', 'bar', 'baz']); //=> ['FOO', 'bar', 'baz']
```
> Returns the result of "setting" the portion of the given data structure focused by the given lens to the result of applying the given function to the focused value.

```js
const headLens = R.lensIndex(0);

R.view(headLens, ['a', 'b', 'c']);            //=> 'a'
R.set(headLens, 'x', ['a', 'b', 'c']);        //=> ['x', 'b', 'c']
R.over(headLens, R.toUpper, ['a', 'b', 'c']); //=> ['A', 'b', 'c']
```
> Returns a lens whose focus is the specified index.

Sources
-------
[1]: [Ramda type signatures](https://github.com/ramda/ramda/wiki/Type-Signatures)
[2]: [Fantasy Land](https://github.com/fantasyland/fantasy-land/) 
[3]: [Static Land](https://github.com/rpominov/static-land)
