---
id: installation
title: Installing Supertokens
sidebar_label: Installation
---

## Add the SuperTokens package dependency

```gradle
implementation 'io.supertokens:session:{latest-version}'
```

Add this to your app level build.gradle. You can find the latest version <a href="https://github.com/supertokens/supertokens-android/releases" target="_blank">here</a>

## Additional packages

For SuperTokens to work correctly you need to use cookies in your application. When using ```HttpUrlConnection``` the library uses a persistent cookie store if you dont already use one. If you use OkHttp or Retrofit the library relies on you to set a cookie jar when creating an instance of the ```OkHttpClient```. The demo project for SuperTokens Android uses a persistent cookie jar from the following dependency:

```gradle
implementation 'com.github.franmontiel:PersistentCookieJar:v1.0.1'
```