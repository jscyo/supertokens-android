---
id: usage-http
title: Initialization
sidebar_label: Initialization 
---

## Call the SuperTokens.init function: [API Reference](../api-reference/api-reference#supertokensinitapplication-applicationcontext-nonnull-string-refreshtokenendpoint-nullable-integer-sessionexpirystatuscode)

- To be called at least once before any http request is made to any of your APIs that require authentication. 
- <span class="highlighted-text">You only need to call this once in your app.</span>

##### JAVA
```java
import io.supertokens.session.SuperTokens

try {
    SuperTokens.init(getApplication(), "https://api.example.com/api/refreshsession", 440);
} catch (MalformedURLException e) {
    // Refresh URL was invalid
}
```

##### Kotlin
```java
import io.supertokens.session.SuperTokens

try {
    SuperTokens.init(application, "https://api.example.com/api/refreshsession", 440);
} catch (MalformedURLException e) {
    // Refresh URL was invalid
}
```