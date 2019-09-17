---
id: verifying-session-http
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
<span class="highlighted-text">SuperTokens does not persist cookies across app launches by default</span>, and relies on you to set a persistent cookie manager for you app. SuperTokens provides a <code>SuperTokensPersistentCookieStore</code> class which can be used to persist cookies. To enable this cookie store simply use the following code before making any HTTP API calls that require authentication:
<br/>
<br/>
<code>CookieManager.setDefault(new CookieManager(new SuperTokensPersistentCookieStore(applicationContext), null));</code>
</div>