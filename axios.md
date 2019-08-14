## How to install
`npm install axios`

## `GET` request
```js
axios.get('https://site.com/', {
  	params: {
    		name: 'Foo'
  	}
})
```

## `POST` request
```js
axios.post('https://site.com/', {
  	name: 'Foo'
})
```

## query params
```js
axios.get('https://site.com/', {
	params: { query: 'foo' }
}
```

## `Authorization` header
```js
axios.get('https://site.com/', {
	headers: {
		Authorization: 'Client-ID 34e393...'
	}
}
```
	
## `then`
```js
axios
	.get('https://site.com/', {})
	.then((res) => console.log(res.data.results));
```

## `async/await`
```js
async foo() {
	const res = await axios.get(...);
	console.log(res.data.results);
}
```

## Sources
[1]: [Axios GitHub](https://github.com/axios/axios)
[2]: [Axios Cheatsheets](https://kapeli.com/cheat_sheets/Axios.docset/Contents/Resources/Documents/index)
[3]: [Axios async/await tutorial](https://flaviocopes.com/axios/)
