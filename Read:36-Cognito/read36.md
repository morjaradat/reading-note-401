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

## Sign in

* The Auth category can be used to register a user, confirm attributes like email/phone, and sign in with optional multi-factor authentication.

***Register a user***

* Example of registering a user :

```
AuthSignUpOptions options = AuthSignUpOptions.builder()
    .userAttribute(AuthUserAttributeKey.email(), "my@email.com")
    .build();
Amplify.Auth.signUp("username", "Password123", options,
    result -> Log.i("AuthQuickStart", "Result: " + result.toString()),
    error -> Log.e("AuthQuickStart", "Sign up failed", error)
);
```

* the query of sign-up :

```
Amplify.Auth.confirmSignUp(
    "username",
    "the code you received via email",
    result -> Log.i("AuthQuickstart", result.isSignUpComplete() ? "Confirm signUp succeeded" : "Confirm sign up not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

***For Sign in a user***

```
Amplify.Auth.signIn(
    "username",
    "password",
    result -> Log.i("AuthQuickstart", result.isSignInComplete() ? "Sign in succeeded" : "Sign in not complete"),
    error -> Log.e("AuthQuickstart", error.toString())
);
```

## Sign in with web UI

* we need to modify hte manifest :

```
<queries>
  <intent>
    <action android:name="android.intent.action.VIEW" />
    <data android:scheme="https" />
  </intent>
  <intent>
    <action android:name=
        "android.support.customtabs.action.CustomTabsService" />
  </intent>
</queries>
<application ...>
  ...
  <activity
      android:name="com.amplifyframework.auth.cognito.activities.HostedUIRedirectActivity"
      android:exported="true">
      <intent-filter>
          <action android:name="android.intent.action.VIEW" />
          <category android:name="android.intent.category.DEFAULT" />
          <category android:name="android.intent.category.BROWSABLE" />
          <data android:scheme="myapp" />
      </intent-filter>
  </activity>
  ...
</application>
```
