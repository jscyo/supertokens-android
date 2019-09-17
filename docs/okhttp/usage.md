---
id: usage-okhttp
title: Initialization
sidebar_label: Initialization 
---

## Add the SuperTokensInterceptor to your OkHttpClient
This library provides an ```Interceptor``` to allow simple integration with OkHttp or Retrofit.

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

## Call the SuperTokens.init function: [API Reference](../api-reference/api-reference#supertokensinitapplication-applicationcontext-nonnull-string-refreshtokenendpoint-nullable-integer-sessionexpirystatuscode)

- To be called at least once before any http request is made to any of your APIs that require authentication. 
- <span class="highlighted-text">You only need to call this once in your app.</span>

#### JAVA
```java
import io.supertokens.session.SuperTokens

try {
    SuperTokens.init(getApplication(), "https://api.example.com/api/refreshsession", 440);
} catch (MalformedURLException e) {
    // Refresh URL was invalid
}
```

#### Kotlin
```java
import io.supertokens.session.SuperTokens

try {
    SuperTokens.init(application, "https://api.example.com/api/refreshsession", 440);
} catch (MalformedURLException e) {
    // Refresh URL was invalid
}
```