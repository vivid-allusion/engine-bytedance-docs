---
title: "Initializing client"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/initializing_a_client"
---

This topic describes how to initialize the Java client.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Downloaded and installed the Redis Java SDK. For specific procedures, refer to [Downloading and installing SDK](https://docs.byteplus.com/en/docs/mongodb/download-install-java-sdk).

* Before initializing the client, ensure that you have obtained the following information:

   * Access Key ID (AK) and Secret Access Key (SK) for your account. For methods to obtain AKSK information, refer to [Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/reference-access-key).

   * Region information. For the regions supported by Redis, refer to [Service endpoints](https://docs.byteplus.com/en/docs/redis/request-structure#.5pyN5Yqh5Zyw5Z2A).


<span id=".5Yid5aeL5YyW5a6i5oi356uv"></span>
## Initializing client

Use the following code to initialize the client.

```Java
import com.byteplus.ApiClient;
import com.byteplus.ApiException;
import com.byteplus.sign.Credentials;

import com.byteplus.redis.RedisApi;
import com.byteplus.redis.model.*;

public class TestRedis {
    public static void main(String[] args) throws Exception {
        // Set AKSK authentication information and Region
        // Note the security of the example code. Code leakage may lead to AKSK leakage, which poses a great security risk.
        String ak = "Your AK";
        String sk = "Your SK";
        String region = "Your Region";

        ApiClient apiClient = new ApiClient()
                .setCredentials(Credentials.getCredentials(ak, sk))
                .setRegion(region);
        RedisApi redisApi = new RedisApi(apiClient);
        
        // Create an interface input parameter and configure it according to the parameter description of the interface to be called
        &{API_interface_name}Request request = new ${API_interface_name}Request();
        
        // Call the interface to complete the operation corresponding to the interface
        try {
            // Copy the code to run the example. Please print the API return value by yourself.
            ${API 接口名称}Response response = redisApi.${API 接口名称}(request);
            System.out.println(response);
        } catch (ApiException e) {
            // Copy the code to run the example. Please print the API error information by yourself.
            System.out.println(e.getResponseBody());
       }
    }
}
```
