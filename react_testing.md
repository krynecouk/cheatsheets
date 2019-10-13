## Jest
> testing framework
### [`expect`](https://jestjs.io/docs/en/expect)
```js
test('basic test', () => {
	const wrapper = shallow(<Foo />);
	expect(wrapper).toBeTruthy();
});
```

### [`toBe`](https://jestjs.io/docs/en/expect#tobevalue)
> Compare primitive values or to check referential identity of object instances.

### [`toBeTruthy()`](https://jestjs.io/docs/en/expect#tobetruthy)
> **NOT** `falsy` : false, 0, '', null, undefined, and NaN.

### [`toContain`](https://jestjs.io/docs/en/expect#tocontainitem)
> Use .toContain when you want to check that an item is in an array.

## Enzyme
> virtual DOM for tests

### [`shallow`](https://airbnb.io/enzyme/docs/api/shallow.html)
> rendering DOM element with mock of children

### [`mount`](https://airbnb.io/enzyme/docs/api/mount.html)
> rendering DOM element with childre (Full DOM rendering)

### [`find(selector)`](https://airbnb.io/enzyme/docs/api/ReactWrapper/find.html)
`expect(wrapper.find('.foo')).to.have.lengthOf(1);`

### [`state`](https://airbnb.io/enzyme/docs/api/ShallowWrapper/state.html)
`expect(wrapper.state('foo')).to.equal(10);`

### [`simulate`](https://airbnb.io/enzyme/docs/api/ShallowWrapper/simulate.html)
> Simulate events on the root node in the wrapper. It must be a single-node wrapper.
`wrapper.find('a').simulate('click');;`

### [`text`](https://airbnb.io/enzyme/docs/api/ShallowWrapper/text.html)
> Returns a string of the rendered text of the current render tree. 
```js
const wrapper = shallow(<div><b>important</b></div>);
expect(wrapper.text()).to.equal('important');
```


## Appendix
### How to install Jest + Enzyme
`npm install --save-dev jest enzyme jest-enzyme enzyme-adapter-react-16`

## Sources
[1]:[Jest Documentation](https://jestjs.io/docs/en/getting-started)
[2]:[Enzyme Documentation](https://airbnb.io/enzyme/)
[3]:[React testing library](https://github.com/testing-library/react-testing-library)

