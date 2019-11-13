## Effects
> Effects are plain JS objects that are yield from generator. These objects represents instructions to the middleware to perform some operation (e.g., invoke some asynchronous function, dispatch an action to the store, etc.).

## `call(fn, ...args)` (**Blocking**)
> Effect description that instructs the middleware to call the function fn with args as arguments.

- `fn`		: Function - A Generator function, or normal function which either returns a Promise as result, or any other value.
- `args		: Array<any>` - An array of values to be passed as arguments to fn.

>  Creates a plain object describing the function call (example below).

```js
// Effect -> call the function Api.fetch with `./products` as argument
{
  CALL: {
    fn: Api.fetch,
    args: ['./products']
  }
}
```

## `apply(context, fn, [args])` (**Blocking**)
> Alias for call([context, fn], ...args).

- `context`	: `this`

## `fork(fn, ...args)` (**Non-blocking**)
> Creates an Effect description that instructs the middleware to perform a **non-blocking** call on `fn`.

> `fork` so as `race` returns object of type `Task`.

### `Task`
> The Task interface specifies the result of running a Saga using fork, middleware.run or runSaga.

- `isRunning()` 
- `isCancelled()` 
- `result()` (`undefined` if still running) 
- `error()` (thrown `undefined` if still running) 
- `toPromise()`
- `cancel()`

## `race(effects)` (**Non-blocking**)
> Creates an Effect description that instructs the middleware to run a Race between multiple Effects and wait for **one** of them to complete.

- effects	: `Object` - a dictionary Object of the form {label: effect, ...}

```js
import { take, call, race } from `redux-saga/effects`
import fetchUsers from './path/to/fetchUsers'

function* fetchUsersSaga() {
  const { response, cancel } = yield race({
    response: call(fetchUsers),
    cancel: take(CANCEL_FETCH)
  })
}
```
> Winner is returned and return is one key object {response/cancel: ...}.

## `all([...effects])` (**Non-blocking**)
> Creates an Effect description that instructs the middleware to run multiple Effects in parallel and wait for **all** of them to complete.

```js
import { all, call } from 'redux-saga/effects'

// correct, effects will get executed in parallel
const [users, repos] = yield all([
  call(fetch, '/users'),
  call(fetch, '/repos')
])
```

## `join([...tasks])` (**Blocking**)
> Creates an Effect description that instructs the middleware to wait for the results of previously forked tasks.

> It wraps the array of tasks in join effects, roughly becoming the equivalent of yield `tasks.map(t => join(t))`.

## `cancel(task)` (**Non-blocking**)
> Creates an Effect description that instructs the middleware to cancel a previously forked task.

- `task`	: A `Task` object returned by a previous `fork`.

> `cancel` will let `task` to perform cleaning in `finally` phase with `cancelled` fn.

## `cancelled()` (**Non-blocking**)
> Creates an effect that instructs the middleware to return whether this generator has been cancelled.

### Automatic cancellation
> Besides manual cancellation there are cases where cancellation is triggered automatically.

1. `race`	: except winner every other competitor;
2. `all` 	: if one is rejected;

## `spawn(fn, ...args)` (**Non-blocking**)
> Same as `fork(fn, ...args)` but creates a detached task. A detached task remains independent from its parent and acts like a top-level task.

## `put(action)` (**Non-blocking**)
> Creates an Effect description that instructs the middleware to schedule the dispatching of an action to the store.

- `action`	: Object - dispatch object to the store. 

## `takeEvery(pattern, saga, ...args)` (**Non-blocking**)
> Creates a saga on each action dispatched to the Store that matches pattern.

- `pattern`	: String | Array | Function;
- `saga`	: generator saga function;
- `args`	: arguments to be passed to the started task;

## `takeLatest(pattern, saga, ...args)` (**Non-blocking**)
> Creates a saga on each action dispatched to the Store that matches pattern. **And** automatically cancels any previous saga task started previously if it's still running.

## `takeLeading(pattern, saga, ...args)` (**Non-blocking**)
> Spawns a saga on each action dispatched to the Store that matches pattern. After spawning a task once, it blocks until spawned saga completes and then starts to listen for a pattern again.

## `take(pattern)` (**Blocking**)
> Creates an Effect description that instructs the middleware to wait for a specified action on the Store. The Generator is suspended until an action that matches pattern is dispatched.

```js
import { select, take } from 'redux-saga/effects'

function* watchAndLog() {
  while (true) {
    const action = yield take('*')
    const state = yield select()

    console.log('action', action)
    console.log('state after', state)
  }
}
```
> `while` loop in generator simply means, that wait for another dispatched action.

## `select(selector, ...args)` (**Non-blocking**)
> Creates an effect that instructs the middleware to invoke the provided selector on the current Store's state (i.e. returns the result of `selector(getState(), ...args)`).

- `selector`	:  It takes the current state and optionally some arguments and returns a slice of the current Store's state (e.g. `state => state.cart`)
- `args`	:  Optional arguments to be passed to the selector in addition of `getState`.

> `select()` returns whole state.

## `throttle(ms, pattern, saga, ...args)` (**Non-blocking**)
> Ignores incoming actions for a given period of time while processing a task.

```js
yield throttle(1000, 'FETCH_AUTOCOMPLETE', fetchAutocomplete)
```

## `debounce(ms, pattern, saga, ...args)` (**Non-blocking**)
> Saga will be called after it stops taking pattern actions for ms milliseconds. Purpose of this is to prevent calling saga until the actions are settled off.

```js
yield debounce(1000, 'FETCH_AUTOCOMPLETE', fetchAutocomplete)
```

## `retry(maxTries, delay, fn, ...args)` (**Blocking**)
> Creates an Effect description that instructs the middleware to call the function fn with args as arguments. In case of failure will try to make another call after delay milliseconds, if a number of attempts < maxTries.

```js
const response = yield retry(3, 10 * SECOND, request, data)
```

## Sources
[1]:[Redux Saga Docs](https://redux-saga.js.org/docs/introduction/)
[2]:[Redux Saga API](https://redux-saga.js.org/docs/api/)
[3]:[Redux Saga Cheatsheet](https://medium.com/@sankalp.lakhina91/effects-in-redux-saga-cheat-sheet-271f9d0bea75)
[4]:[Auth Example Github](https://github.com/jcolemorrison/redux-sagas-authentication-app/blob/master/src/login/sagas.js)
[5]:[Redux Saga Typescript Examples](https://github.com/Lemoncode/redux-sagas-typescript-by-example)
[6]:[Blocking/Notblocking saga helpers](https://redux-saga.js.org/docs/api/)
