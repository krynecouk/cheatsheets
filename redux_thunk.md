## Redux Rules
- Action Creators *must* return action objects.
- Actions *must* have a type property.
- Actions can optionally have a `payload` property.

## Redux Rules with Redux Thunk
- Action Creators *can* return action objects or
- Action Creators *can* return functions.

## Redux Cycle with Redux Thunk middleware
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
       * dispatch * <-------------------------- * New Action *                             
             |                                         |
   (forwards actions to..)                (manually dispatch action)
             |
             ˇ                                         |
      * Redux Thunk *                    (wait for request to finish)
             |
  (is `action` a function?)  ---                       ^
             |                 |                       |
	    (NO)             (YES) -- (Invoke with `dispatch` and `getState`)

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

## How to install
`npm install --save redux react-redux redux-thunk`

## How to import
```js
import { createStore, applyMiddleware } from 'redux';
import thunk from `redux-thunk`;

const store = createStore(reducers, applyMiddleware(thunk));
```

## How to write thunk
```js
export const fetchPosts = () => async (dispatch, getState) => {
    const response = await jsonPlaceholder.get('/posts');
    dispatch({ type: 'FETCH_POSTS', payload: response });
};
```

## Sources
[1]: [Udemy Redux Thunk](https://www.udemy.com/react-redux/learn/lecture/12586858#overview)
[2]: [Thunks in Redux](https://medium.com/fullstack-academy/thunks-in-redux-the-basics-85e538a3fe60)
