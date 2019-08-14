## Installing React App 
```sh
npx create-react-app <project-name>
```

## Project structure
```yaml
-- src 			: source code
|
-- public 		: static files (images) 
|
-- node_modules		: project dependencies
|
-- package.json 	: configuraton for project (like scripts) and dependencies 
|
-- package-lock.json 	: versions of dependencies 
|
-- README.md 		: readme
```
## Starting app
`npm start`

## Mandatory dependencies
```js
import React from 'react';
import ReactDOM from 'react-dom';
```

## React component
> Is a function/class that produces HTML (using JSX) and handles feedback from user (by Event Handlers).

## JSX
> JSX is an XML/HTML-like syntax used by React that extends ECMAScript so that XML/HTML-like text can co-exist with JavaScript/React code. JSX is then transpiled by Babel.

```js
const App = () => <div>Hello there</div>;
```
=> 
```js
var App = function App() {
  return React.createElement("div", null, "Hello there");
};
```

## JSX vs HTML
### Inline Style
```html
<div style = "background-color: red;"></div>
```
=>
```js
<div style = {{ backgroundColor: 'red' }}></div>
```
> `{` for referencing javascript variable inside JSX
> `{}` inside is just js literal for an object

### ClassName
```html 
<label class = "label"></label>
```
=> 
```js
<label className = "label"></label>
```

### JS variables ref
```js
<label className = { labelName }></label>
```

## `'` vs `"` in JSX
- `"` when JSX string property
- `'` when non-JSX property

## Tenets of React Compoment
- Nesting
- Reusability
- Configuration

## `props` system
> System for passing data from a parent component to a child component. 
> Goal is to customize or configure a child component. 

### `props` attributes
```js
<CommentDetail author="Sam" />
```
```js
const CommentDetail = props => {
	return <div>{ props.author }</div>
}
```

### `props` children
```js
const App = () => {
    <ApprovalCard>
        <CommentDetail author="goobi" />
    </ApprovalCard>
};

const ApprovalCard = props => {
    return <div>{ props.children }</div>
};
```

### `props` defaults
```js
App.defaultProps = {
	author="foo"
}
```

## `class` component
- extends `React.Component`
- must impl `render`

```js
class App extends React.Component {
	render() {
		return <div>foo</div>;
	}
```

## `state`
- js object that contains data relevant for component
- updating `state` causes component to instantly rerender
- must be initialized when component is created 
- state can *only* be updated using the `setState` function

### Init `state` with constructor
```js
class App extends React.Component {
	constructor(props) {
		super(props);	
		// WARN: this is *only* time we do direct assignment
		this.state = { foo: null };
		// WARN: this is *only* way how to update state
		this.setState( { foo: asyncFetchFoo() } );
	}		
}
```

> *WARNING:* `render` function is called multiple times - avoid putting performance heavy operations.

> Can be used with member variables like so:
```js
class App extends React.Component {
	state = { foo: null };
}
```

## Component Lifecycle
```yml
       constructor
            |
          render
            |
* content visible on the screen *
            |
    componentDidMount
            |
   * waits for updates *	
            |
    componentDidUpdate
            |
   * waits for destroy *
            |
   componentWillUnmount
```

## Event Handlers
- `onClick`
- `onChange`
- `onSubmit`
- [more here](https://reactjs.org/docs/events.html#supported-event)

```js
onInputChange(event) {
	console.log(event.target.value);
}
```

```js
<input type="text" onChange={this.onInputChange} />
```
> *WARNING*: function reference, not call.

> `onInputChange` is a function name by convention: on\<El\>\<Event\>. 

## Controlled vs Uncontrolled elements
> Example above is uncontrolled element (state is managed by DOM itself). 

> Controlled element is element where its state is managed by react `state`.
```js
state = { term: '' }; 

<input type="text" value={ this.state.term } onChange={ (e) => this.setState({ term: e.target.value }) } />
```

> Controlled element is preferable because we don't have to touch DOM in order to get state.

## Invoking callback in children component
```js
class App extends React.Component {
	render() {
		<SearchBar onSubmit={ this.foo } />
	}
}
```

```js
class SearchBar extends React.Component {
	render() {
		<form onSubmit={ () => this.props.onSubmit(this.state.term) }>
	}	
}
```

## Appendix
### CSS importing
```js
import './Foo.css'
```

### CSS and root div
> Use `className` of root `div` (container) same as react component (e.g. `SeasonDisplay` react component has root `<div className={'season-display'}>...</div>`. 

### CSS for center text
```css
.foo {
	display: flex;
	justify-content: center;
	align-items: center;
	height: 100vh;
}
```

### `render` and `return`
> Best practice is to have only one return statement in our `render` function.

### Project hiararchy
> Best practice is to to have all components in `/src/components` folder. 

### `import` position
> By conventions we place imports of third party libs above the ours.

## Sources
[1]: [Udemy - React Redux](https://www.udemy.com/react-redux/learn/lecture/12531044?start=0#overview)
[2]: [MDN Import documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
[3]: [BabelJS](https://babeljs.io)
[4]: [Axios](https://github.com/axios/axios)
[5]: [Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
