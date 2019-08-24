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
> Actions are plain objects representing event. Must have mandatory field `type` and optional `payload`.

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

### Reducer
> Reducers specify how the application's state changes in response to actions sent to the store.

> The reducer is a pure function that takes the previous state and an action, and returns the next state.

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
> `mapDispatchToProps` may be an object where each field is an action creator.

> It automatically binds action creator to `props`.

> React-Redux binds the dispatch of your store to each of the action creators using `bindActionCreators`.

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

[More about connect params](https://react-redux.js.org/api/connect)


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

## Sources
[1]:[Udemy React Redux](https://www.udemy.com/react-redux/learn/lecture/12531416)
[2]:[Redux Documentation](https://redux.js.org)
[3]:[Redux - Remove boilerplate](https://redux.js.org/recipes/reducing-boilerplate#reducers)
