# Cognito

* The Amplify Auth category provides an interface for authenticating a user.
* It comes with default, built-in support for Amazon Cognito User Pool and Identity Pool.

* how to added to your application:

1. initialize the command : amplify add auth then amplify push

2. add the following dependencies to build-gradle :

``` dependance
 implementation 'com.amplifyframework:aws-auth-cognito:1.24.0'
```

3. add the plugin in your application:

```
 Amplify.addPlugin(new AWSCognitoAuthPlugin());
 Amplify.configure(getApplicationContext()); 
```

## Check the current auth session

* to check we will run the following command :

```
Amplify.Auth.fetchAuthSession(
    result -> Log.i("AmplifyQuickstart", result.toString()),
    error -> Log.e("AmplifyQuickstart", error.toString())
);
```
