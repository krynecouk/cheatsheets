## Concept
```yml
    (change of browser route)
                |
		ˇ
	     history
	        |
	        ˇ
	      Router
	        |
	        ˇ
 Route path="<history.location.path>"
	        |
	        ˇ
	    Component
```

## `react-router-dom`

- `BrowserRouter`       : localhost:3000/**pagetwo**
- `HashRouter`          : localhost:3000/#/**pagetwo**
- `MemoryRouter`        : localhost:3000/

```js
import { BrowserRouter, Route } from 'react-router-dom';

const App = () => {
  return (
    <div>
      <BrowserRouter>
        <div>
          <Route path="/" exact component={ PageOne } />
          <Route path="/pageTwo" component={ PageTwo } />
	  <Route path="/pages/edit/:id component={ PageThree } />
        </div>
      </BrowserRouter>
    </div>
  );
}
```

## `Link`
```js
import { Link } from 'react-router-dom';
...
<Link to="/pagetwo">Navigate to page two</Link>
```
> Must **NOT** use `<a href>` tag because it will fetch all resources per every request.

## Router History
```js
import createHistory from 'history/createBrowserHistory';
export default createHistory();
```

```js
import { Router, Route } from 'react-router-dom';
import history from '../history';

<Router history={ history } />
```

```js
export const fooAction => async dispatch = {
	...
	history.push('/');
};
```

## Switch
```js
import { Router, Route, Switch } from 'react-router-dom';

<Router>
	<Switch>
		<Route path="/" />
		<Route path="/:id" />
	</Switch>
</Router>
```
> Returns first match from the `Router` list.


## Sources
[1]:[React Router Documentation](https://reacttraining.com/react-router/web/guides/quick-start)
[2]:[React History Object](https://github.com/ReactTraining/react-router/blob/master/packages/react-router/docs/api/history.md_
