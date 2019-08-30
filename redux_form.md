## Concept
```yml
DOM:onChange -> Component:handler -> Redux Form:Action Creator -> Redux Form Reducer
                                                                         |
DOM:value <---- Component:props  <-- Redux Form:mapStateToProps <---------
```

## Usage
```js
import { reducer as formReducer } from 'redux-form';

export default combineReducers({
	form: formReducer
});
```

> `form` is a mandatory key. 

```js
import { Field, reduxForm } from 'redux-form';

class Foo extends React.Component {

	renderInput(formProps) {
		return (
			<input onChange={formProps.input.onChange} value={formProps.input.value} />
			<input {...formProps.input}/>
		);
	}

	onSubmit(formValues) {
	...	
	}

	render() {
		return (
			<form onSubmit={this.props.handleSubmit(this.onSubmit)}>
				<Field name="title" component={this.renderInput} />
			</form>
		)
	}		
	
}

export default reduxForm({
	form: 'fooForm'
})(Foo);
```

## Sources
[1]:[Redux Form Documentation](https://github.com/erikras/redux-form)
[2]:[What you need to know about forms in React](https://goshakkk.name/on-forms-react/)
[3]:[Should you put form state in redux?](https://redux.js.org/faq/organizing-state#should-i-put-form-state-or-other-ui-state-in-my-store)
