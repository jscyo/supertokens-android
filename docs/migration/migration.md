---
id: migration
title: Add SuperTokens to an existing application
sidebar_label: Migration
---

## Add the gradle dependency
```gradle
implementation 'io.supertokens:session:{latest-version}'
```

Add this to your app level build.gradle. You can find the latest version <a href="https://github.com/supertokens/supertokens-android/releases" target="_blank">here</a>

<div class="specialNote">
This package uses AndroidX artifacts and will break your build if your app does not use them. To learn more about AndroidX and how to migrate visit <a href="https://developer.android.com/jetpack/androidx" target="_blank">here</a>
</div>

## Using HttpURLConnection for API calls
The library is designed to allow integration with minimal changes. The library provides a callback function when using HttpURLConnection that allows you to perform all the operations on the connection object that you would perform normally. For example if your API flow looks something like this:

```java
URL url = new URL("YOUR API URL");
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("POST");
connection.connect();
if ( connection.getResponseCode() == 200 ) {
    InputStream inputStream = connection.getInputStream();
    ...
}
```

This code snippet would need to modified like so when using SuperTokens to make API calls.

```java
// Call this when your application initializes
// where 440 is the status code the backend configures to indicate unauthorized access
SuperTokens.init(getApplication(), "YOUR REFRESH TOKEN ENDPOINT", 440);

// Actual API call
URL url = new URL("YOUR API URL");
InputStream inputStream = SuperTokensHttpURLConnection.newRequest(url, new SuperTokensHttpURLConnection.SuperTokensHttpURLConnectionCallback<InputStream>() {
    @Override
    public InputStream runOnConnection(HttpURLConnection con) {
        try {
            con.setRequestMethod("POST");
            con.connect();
            if ( con.getResponseCode() == 200 ) {
                return con.getInputStream();
            }
            return null;
        } catch (Exception e) {
            return null;
        }
    }
});
...
```

Using the ```newRequest``` method allows SuperTokens to handle unauthorized errors for you. If the API call fails with the status code you provide (440 in this case) the library calls the refresh token endpoint, retrieves the new token values and retries the original API call automatically. The result of the callback function is returned when the API call does not fail.

SuperTokens uses cookies for session management and relies on you to set a default ```CookieManager```. If you do not set one the library will throw an exception. For an example of how to set a ```CookieManager``` for your application refer to our <a href="https://github.com/supertokens/android-demo" target="_blank">demo app</a>.

<div class="specialNote">
The library calls <code>HttpURLConnection.disconnect()</code> for you, please make sure to not call the disconnect method inside or after the callback function.
</div>

## Using OkHttp/Retrofit for API calls

This library provides an ```Interceptor``` to allow simple integration with OkHttp or Retrofit. To use SuperTokens simply add the ```SuperTokensInterceptor``` to your OkHttpClient like so

##### using OkHttp
```java
OkHttpClient.Builder clientBuilder = new OkHttpClient.Builder();
clientBuilder.interceptors().add(new SuperTokensInterceptor());
OkHttpClient client = clientBuilder.build();
```

##### using Retrofit
```java
OkHttpClient.Builder clientBuilder = new OkHttpClient.Builder();
clientBuilder.interceptors().add(new SuperTokensInterceptor());

OkHttpClient client = clientBuilder.build();

Retrofit instance = new Retrofit.Builder()
    .baseUrl("YOUR BASE URL")
    .client(client)
    .build();
```

If you use OkHttp or Retrofit the library relies on you to set a cookie jar when creating an instance of the ```OkHttpClient```. The demo project for SuperTokens Android uses a persistent cookie jar from the following dependency:

```gradle
implementation 'com.github.franmontiel:PersistentCookieJar:v1.0.1'
```