## OAuth
> Authentification on the outside service provider (Google, Facebook..)

> Can be used for user identification or making actions on behalf of user.

## Server OAuth
- result is token that server can use to make on behalf requests
- used when we need user data when they are **NOT** logged in
- complicated setup 

## Browser OAuth
- result is token that *browser* can use to make on behalf requests
- used when we need user data when they **are** logged in
- easy setup thanks to Google's JS lib to automate flow

```js
class GoogleAuth extends React.Component {
  componentDidMount() {
    window.gapi.load('client.auth2', () => {
      window.gapi.client.init({clientId:'...',scope:'email'})
        then(() => {
          this.auth = window.gapi.auth2.getInstance();
       	  this.auth.isSignedIn.listen(this.onAuthChange); 
        });
    });
  }
}
```


## Sources
[1]:[Google OAuth Scopes](https://developers.google.com/identity/protocols/googlescopes)
[2]:[Api Client JS library](https://developers.google.com/api-client-library/)
