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

Example
=======
```yml
The category Set has "objects," which are sets, and "morphisms" or "arrows," which are functions between the sets.  
It has a few other interesting properties, notably:
- If there's a function 𝑓 from some set 𝐴 to some set 𝐵, and there's also a function 𝑔:𝐵→𝐶, then there's a function 𝑔∘𝑓:𝐴→𝐶.
- Composition is associative: for functions 𝑓:𝐴→𝐵, 𝑔:𝐵→𝐶, and ℎ:𝐶→𝐷, we have that ℎ∘(𝑔∘𝑓)=(ℎ∘𝑔)∘𝑓.
- For every set 𝐵, there's a special function 1𝐵:𝐵→𝐵, which is the identity for function composition; that is, 1𝐵∘𝑓=𝑓 and 𝑔∘1𝐵=𝑔.
```

Functor
-------
> A Functor is a type that implements map and obeys some laws (simply an interface with a contract ~ Mappable)

> Functor is a map between categories.

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
``` js
// head :: [a] -> a
```
> `a` says it cannot be a specific type, which means it can be any type, which leaves us with a function that must work uniformly for every conceivable type.

Free Theorem
------------
```js
// head :: [a] -> a
compose(f, head) === compose(head, map(f));

// filter :: (a -> Bool) -> [a] -> [a]
compose(map(f), filter(compose(p, f))) === compose(filter(p), map(f));
```


Theory
------
ads

Appendix A: Examples
--------------------
Functor
=======

```js
class Container {
  constructor(x) {
    this.$value = x;
  }

  static of(x) {
    return new Container(x);
  }
}
```

```js
// (a -> b) -> Container a -> Container b
Container.prototype.map = function (f) {
  return Container.of(f(this.$value));
};
```

```js
Container.of(2).map(two => two + 2); 
// Container(4)

Container.of('flamethrowers').map(s => s.toUpperCase()); 
// Container('FLAMETHROWERS')

Container.of('bombs').map(append(' away')).map(prop('length')); 
// Container(10)
```

Maybe 
=====
```js
class Maybe {
  static of(x) {
    return new Maybe(x);
  }

  get isNothing() {
    return this.$value === null || this.$value === undefined;
  }

  constructor(x) {
    this.$value = x;
  }

  map(fn) {
    return this.isNothing ? this : Maybe.of(fn(this.$value));
  }

  inspect() {
    return this.isNothing ? 'Nothing' : `Just(${inspect(this.$value)})`;
  }
}
```
> Implementation will split Maybe into two types: one for something (`Some`) and the other for nothing (`None`).

Either
======
```js
class Either {
  static of(x) {
    return new Right(x);
  }

  constructor(x) {
    this.$value = x;
  }
}

class Left extends Either {
  map(f) {
    return this;
  }
}

class Right extends Either {
  map(f) {
    return Either.of(f(this.$value));
  }
}

const left = x => new Left(x);
```

IO
==
```js
class IO {
  static of(x) {
    return new IO(() => x);
  }

  constructor(fn) {
    this.$value = fn;
  }

  map(fn) {
    return new IO(compose(fn, this.$value));
  }
}
```

```js
// url :: IO String
const url = new IO(() => window.location.href);

// toPairs :: String -> [[String]]
const toPairs = compose(map(split('=')), split('&'));

// params :: String -> [[String]]
const params = compose(toPairs, last, split('?'));

// findParam :: String -> IO Maybe [String]
const findParam = key => map(compose(Maybe.of, filter(compose(eq(key), head)), params), url);

// -- Impure calling code ----------------------------------------------

// run it by calling $value()!
findParam('searchTerm').$value();
// Just([['searchTerm', 'wafflehouse']])
```

Asynchronous Tasks
===================
```js
// getJSON :: String -> {} -> Task Error JSON
const getJSON = curry((url, params) => new Task((reject, result) => {
  $.getJSON(url, params, result).fail(reject);
}));

// blogPage :: Posts -> HTML
const blogPage = Handlebars.compile(blogTemplate);

// renderPage :: Posts -> HTML
const renderPage = compose(blogPage, sortBy(prop('date')));

// blog :: Params -> Task Error HTML
const blog = compose(map(renderPage), getJSON('/posts'));


// Impure 
blog({}).fork(
  error => $('#error').html(error.message),
  page => $('#main').html(page),
);

$('#spinner').show();
```

Sources
-------
[1]: [Mostly Adequate Guide to Functional Programming](https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)
[2]: [Curry and Function Composition](https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983)
[3]: [ES Fiddle](https://esfiddle.net)
[4]: [So You Still Don't Understand Hindley-Milner](http://akgupta.ca/blog/2013/05/14/so-you-still-dont-understand-hindley-milner/)
[5]: [Hindley-Milner StackOverflow](https://stackoverflow.com/questions/12532552/what-part-of-hindley-milner-do-you-not-understand)
[6]: [Wadler's paper](https://ttic.uchicago.edu/~dreyer/course/papers/wadler.pdf)
[7]: [Folktale](https://folktale.origamitower.com)
[8]: [Category Theory - Stanford Edu](https://plato.stanford.edu/entries/category-theory/)
[9]: [Category Theory - Quora](https://www.quora.com/What-is-category-theory-23346)
