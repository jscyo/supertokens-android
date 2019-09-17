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

<div class="specialNote">
This package uses AndroidX artifacts and will break your build if your app does not use them.
</div>

## Additional packages

For SuperTokens to work correctly you need to use cookies in your application. When using ```HttpUrlConnection``` the library provides a persistent cookie store that you can use. If you use OkHttp or Retrofit the library relies on you to set a cookie jar when creating an instance of the ```OkHttpClient```. The demo project for SuperTokens Android uses a persistent cookie jar from the following dependency:

```gradle
implementation 'com.github.franmontiel:PersistentCookieJar:v1.0.1'
```