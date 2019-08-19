---
id: api-reference
title: API Reference
sidebar_label: API Reference
---

## ```SuperTokens.init(Application applicationContext, @NonNull String refreshTokenEndpoint, @Nullable Integer sessionExpiryStatusCode)```
##### Parameters
- ```applicationContext```
    - The application context for your app.

- ```refreshTokenEndpoint```
    - Should be the full request URL for your refresh session API endpoint. 
    - The library will use this endpoint in case of session expiry.

- ```sessionExpiryStatusCode```
    - Value for the HTTP Status Code which represents unauthorised access.
    - Optional, defaults to ```440```.

##### Returns
- ```void```

##### Throws
- ```MalformedURLException``` if the refreshTokenEndpoint does not start with http or https, or it has an invalid format.

<div class="divider"></div>

## ```SuperTokens.sessionPossiblyExists(Application applicationContext)```
#### Parameters
- ```applicationContext```
    - The application context for your app.

##### Returns
- ```Boolean``` value, true if there is an existing session

##### Throws
- nothing

<div class="divider"></div>

## ```SuperTokensHttpRequest.newRequest(URL url, SuperTokensHttpCallback<T> callback)```
##### Parameters
- ```url```
    - Type: java.net ```URL```
    - URL object used to create the Http/HttpsURLConnection
- ```callback```
    - Type: SuperTokensHttpCallback
    - callback that provides an instance of HttpURLConnection, this instance can be used to perform any operation on the connection. The callback returns an object with generic type ```T``` which can be configured when providing the callback to the ```newRequest``` method.

###### Returns
The output of the callback that is provided to this method.

##### Throws
- ```IllegalAccessException``` if ```SuperTokens.init``` has not been called or if the ```Application``` object provided to the init function is null.
- ```IOException``` if any of the operations on the connection fail
- ```URISyntaxException``` if the provided URL object or the refresh token endpoint provided to the ```SuperTokens.init``` function is invalid.