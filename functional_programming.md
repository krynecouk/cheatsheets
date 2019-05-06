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
httpGet('/post/2', (json, err) => renderPost(json, err));		// NOTOK
httpGet('/post/2', renderPost);						// OK
```

Sources
-------
[1]: [Mostly Adequate Guide to Functional Programming]e(https://mostly-adequate.gitbooks.io/mostly-adequate-guide/)
