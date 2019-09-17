---
id: request-http
title: Making API Calls
sidebar_label: Making API Calls
---


## Original API request using HttpURLConnection

##### JAVA
```java
URL url = new URL("https://api.example.com/api/getUerInfo");
HttpURLConnection connection = (HttpURLConnection) url.openConnection();
connection.setRequestMethod("POST");
connection.connect();
if ( connection.getResponseCode() == 200 ) {
    InputStream inputStream = connection.getInputStream();
    ...
} else if ( connection.getResponseCode() == 440 ) {
    // Unauthorized access
}
connection.disconnect();
```

##### Kotlin
```java
val url = URL("https://api.example.com/api/getUerInfo")
val connection = url.openConnection() as HttpURLConnection
connection.requestMethod = "POST"
connection.connect()
if ( connection.responseCode == 200 ) {
    val inputStream = connection.inputStream
    ...
} else if (connection.responseCode == 440) {
    // Unauthorized access
}
connection.disconnect();
```

## Requests made using SuperTokens

##### JAVA
```java
URL url = new URL("https://api.example.com/api/getUerInfo");
try {
    InputStream inputStream = SuperTokensHttpURLConnection.newRequest(url, new SuperTokensHttpURLConnection.SuperTokensHttpURLConnectionCallback<InputStream>() {
        @Override
        public InputStream runOnConnection(HttpURLConnection con) throws IOException {
            con.setRequestMethod("POST");
            con.connect();
            if ( con.getResponseCode() == 200 ) {
                return con.getInputStream();
            }
        }
    });
} catch (IOException e) {
    // Something went wrong making the API call
}
```

##### Kotlin
```java
val url = URL("https://api.example.com/api/getUerInfo")
try {
    val inputStream = SuperTokensHttpURLConnection.newRequest(url, SuperTokensHttpURLConnection.SuperTokensHttpURLConnectionCallback<InputStream> {
        it.requestMethod = "POST"
        it.connect()
        if ( it.responseCode == 200 ) {
            return it.inputStream
        }
    })
} catch (IOException e) {
    // Something went wrong making the API call
}
```

- Replace all ```connection.connect()``` calls with ```SuperTokensHttpURLConnection.newRequest```([api reference](../api-reference/api-reference#supertokenshttpurlconnectionnewrequesturl-url-supertokenshttpcallback-t-callback))
- All operations you would normally perform on the connection object are now performed inside the callback method. The output type of the callback is defined by you when making the request.
- <span class="highlighted-text">You do not need to check for unauthorized access inside the callback.</span> In the case where the response status code matches the unauthorized status code you provide the library calls the refresh token endpoint for you and then retries the API call automatically.

<div class="specialNote">
SuperTokens calls <code>HttpURLConnection.disconnect()</code> for you, please do not call the disconnect method inside the callback or anywhere else manually.
</div>