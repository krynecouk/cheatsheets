## Redux Cycle
```yml
(to change state, we call an..)
     * Action Creator * 
             |
      (produces an..)
             |
             ˇ
        * Action *
             |
      (gets fed to..)
             |
             ˇ
       * dispatch *
             |
   (forwards actions to..)
             |
             ˇ
       * Middleware *
             |
 (stop, modify etc. action)
             |
             ˇ
        * Reducers *
             |
       (creates new)
             |
             ˇ
         * State *
             |
             ˇ
   (waits for next update)
```

### Action Creator
> An action creator is a plain function that returns an action object.

```js
function userLoggedIn() {
  return {
    type: USER_LOGGED_IN
  };
}
```


### Action
> Actions *MUST* be a plain js objects representing event. Must have mandatory field `type` and optional `payload`.

```js
{
  type: USER_LOGGED_IN
  payload: {
    name: 'Jim',
    surname: 'Fooler'
  }
}
``` 

### dispatch
> Method for dispatching actions to the reducers.

> Like `setState`, `dispatch` will re-render our component.

```js
store.dispatch(createUser('Jim', 'Fooler'));
```

### Middleware
> Function that gets called with every dispatched action.

> Has ability to *STOP*, *MODIFY*, or otherwise mess around with actions.

> Most custom Redux middlewares are used for async actions.

### Reducer
> The reducer is a pure function that takes the previous state and an action, and returns the next state.

> **Must** return value.

> **Must NOT** mutate its `state`. 

`(previousState, action) => newState`

```js
function todoApp(state = initialState, action) {
  switch (action.type) {
    case SET_VISIBILITY_FILTER:
      return Object.assign({}, state, {
        visibilityFilter: action.filter
      })
    default:
      return state
  }
}
```

### State
> State is stored in `store`.

> `store` holds the whole state tree of your application.

> The only way to change the state inside it is to dispatch an action on it.


## Installing with React
`npm install --save redux react-redux`

## Project structure
```yml
/src
  /actions      
  /components  
  /reducers 
  index.js
```

## Connecting Redux with React
- `Provider`
- `connect()`

### `Provider`
> The `<Provider />` makes the Redux store available to any nested components that have been wrapped in the `connect()` function.
```js
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

### `connect()`
> The `connect()` function connects a React component to a Redux store.

```js
function connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)(Object)
```

#### `mapStateToProps?: (state, ownProps?) => Object`
> If a `mapStateToProps` function is specified, the new wrapper component will subscribe to Redux store updates. This means that any time the store is updated, `mapStateToProps` will be called.
```js
const mapStateToProps = state => {
	return { songs: state.songs };
}
```
> `ownProps` are props passed in JSX.

#### `mapDispatchToProps?: Object | (dispatch, ownProps?) => Object`
> Maps `actionCreators` with binded `dispatch`(using `bindActionCreators`) to the `props`.

```js
const mapDispatchToProps = dispatch => {
  return {
    // dispatching plain actions
    increment: () => dispatch({ type: 'INCREMENT' }),
    decrement: () => dispatch({ type: 'DECREMENT' }),
    reset: () => dispatch({ type: 'RESET' })
  }
}
```

> `mapDispatchToProps` may be an object where each field is an action creator...

```js
import { addTodo, deleteTodo, toggleTodo } from './actionCreators'

const mapDispatchToProps = {
  addTodo,
  deleteTodo,
  toggleTodo
}

export default connect(
  null,
  mapDispatchToProps
)(TodoApp)
```

## General Data Loading with Redux
```yml
    Component is rendered 
              |
              ˇ
 `componentDidMount` is called
              |
              ˇ
     Action creator from 
 `componentDidMount` is called
              |
              ˇ
  Action creator runs code 
    to make API request
              |
              ˇ
    API responds with data
              |
              ˇ
Action creator returns `action` 
 with fetched data in payload
              |
              ˇ
   `dispatch` is called, 
state is modified by reducer
              |
              ˇ
    Component is re-rendered
```
> Components are responsible for fetching data.

> Action creators are responsible for making API requests.

> Fetched data are get to the `Component` by updating state and `mapStateToProps`

[More about connect params](https://react-redux.js.org/api/connect)

## Redux Dev Tools
```js
import { createStore, applyMiddleware, compose } from 'redux';

const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ || compose;
const store = createStore(
  reducers,
  composeEnhancers(applyMiddleware())
);
```

`localhost:<port>?debug_session=<some_string>`

## Appendix
### Create User Redux Cycle example
```js
// Action Creator
const createUser = (name, surname) => {
    return {
      type: 'CREATE_USER',
      payload: {
        name: name,
        surname: surname
      }
    }
}

// Reducer
const users = (users = [], action) => {
  if (action.type === 'CREATE_USER') {
    return [...users, action.payload];  
  }
  return users;
}

const reducers = combineReducers({ users });
const store = createStore(reducers);

// dispatch
store.dispatch(createUser('Jim', 'Beam'));
store.dispatch(createUser('Foo', 'Bar'));

// State
console.log(store.getState());
```

### Export reducers
```js
import { combineReducers } from 'redux';
...
export default combineReducers({
	songs: songsReducer,
	selectedSong: selectedSongReducer
});

// `combineReducers` is like DB ~ state 
// props are like tables of DB 
```

### `connect` boilerplate
```js
import {connect} from 'react-redux';

const mapStateToProps = state => {...};

export default connect(mapStateToProps)(SongList);
```

### Why reducer **must not** mutate state
> `combineReducers.js`
```js
...
hasChanged = hasChanged || nextStateForKey !== previousStateForKey
...
```
> If we mutate e.g. array state, then it has still same ref and redux won't notice the change 
-> won't update state -> won't re-render.

## Sources
[1]:[Redux Documentation](https://redux.js.org)
[2]:[Redux - Remove boilerplate](https://redux.js.org/recipes/reducing-boilerplate#reducers)
[3]:[Redux Dev Tools extension](https://github.com/zalmoxisus/redux-devtools-extension)
