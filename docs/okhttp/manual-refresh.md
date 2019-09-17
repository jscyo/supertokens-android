---
id: manual-refresh-okhttp
title: Manually Refreshing Sessions
sidebar_label: Manual refresh
---

## Call the attemptRefreshingSession: [API reference](../api-reference/api-reference#supertokensinterceptorattemptrefreshingsessionokhttpclient-client)

- This is required if you need to manually call the refresh token endpoint
- This will call the refresh token endpoint and handle all the token changes

```java
try {
    SuperTokensInterceptor.attemptRefreshingSession(okHttpClient)
} catch (IllegalAccessException e) {
    // SuperTokens.init not called or application context provided to init is null
} catch (IOException e) {
    // Something went wrong calling the refresh token endpoint
}
```