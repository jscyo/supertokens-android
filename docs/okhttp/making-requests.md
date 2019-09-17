---
id: request-okhttp
title: Making API Calls
sidebar_label: Making API Calls
---

Since SuperTokens uses interception with both OkHttp and Retrofit the code to make API calls does not require any changes. <span class="highlighted-text">You do not need to check for unauthorized access in your responses.</span> In the case where the response status code matches the unauthorized status code you provide the library calls the refresh token endpoint for you and then retries the API call automatically.

## Making requests using OkHttp

```java
import okhttp3.Callback

val client: OkHttpClient // Your OkHtppClient

val request = Request.Builder()
    .url("http://192.168.29.145:8080/api/userInfo")
    .method("GET", null)
    .build()

client.newCall(request).enqueue(object: Callback {
    override fun onFailure(call: Call, e: IOException) {
        // API faulure
    }

    override fun onResponse(call: Call, response: Response) {
        // Handle Response
    }
})
```

## Making request using Retrofit

```java
interface RetrofitApiService {
    @POST("login")
    fun login(): Call<Void>
}
```

```java
import retrofit2.Callback

val call = retrofitApiService.login()
call.enqueue(object: Callback<Response>{
    override fun onFailure(call: Call<Response>, t: Throwable) {
        // API failure
    }

    override fun onResponse(call: Call<Response>, response: Response<Response>) {
        // Handle Response
    }
})
```
