---
id: verifying-session-okhttp
title: Verifying if a session exists
sidebar_label: Verifying Sessions
---

## Call the SuperTokens.sessionPossiblyExists function: [API Reference](../api-reference/api-reference#supertokenssessionpossiblyexistsapplication-applicationcontext)


##### JAVA
```java
SuperTokens.sessionPossiblyExists(getApplicationContext());
```

##### Kotlin
```java
SuperTokens.sessionPossiblyExists(application);
```

- This method can be used to check if there is currently an active session.
- For example: To check whether a user should be asked to login or redirected to the main flow directly.

<div class="specialNote">
<span class="highlighted-text">SuperTokens does not persist cookies across app launches by default</span>, and relies on you to set a persistent cookie store for your OkHttpClient. Our demo app uses a persistent cookie store from the following dependency:
<br/>
<br/>
<code>implementation 'com.github.franmontiel:PersistentCookieJar:v1.0.1'</code>
</div>