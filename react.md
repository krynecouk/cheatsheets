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

## Sources
[1]: [Udemy - React Redux](https://www.udemy.com/react-redux/learn/lecture/12531044?start=0#overview)
[2]: [MDN Import documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)
[3]: [BabelJS](https://babeljs.io)
