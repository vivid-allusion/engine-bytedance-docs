---
title: "Client initialization"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Java_Client_initialization"
---

This topic describes how to initialize the Java client.

<span id="Z1vyCyT1"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* You have obtained the Access Key ID (AK) and Secret Access Key (SK) for your account. For details, refer to [Managing an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey).

* You have obtained the regions supported by Cloud Search. For details, refer to [Service endpoints](https://docs.byteplus.com/en/docs/cloudsearch/request-structure#request-method).

* You have downloaded and installed the Cloud Search Go SDK. For details, refer to [Download and installation](https://docs.byteplus.com/en/docs/cloudsearch/Go_Download_and_installation).


<span id="r1MXL99c"></span>
## Initialize the client

Use the following code to initialize the client.

```java
public class java_demo {


    // Set the AK/SK authentication information and Region
    public static String ak = "Your AK";
    public static String sk = "Your SK";
    public static String region = "cn-beijing";

    // Use the regional API service address
    public static String endpoint = "escloud.cn-beijing.byteplusapi.com";


    // Create a Cloud Search SDK client to call APIs and execute task requests
    public static ApiClient apiClient = new ApiClient()
            .setCredentials(Credentials.getCredentials(ak, sk))
            .setRegion(region)
            .setEndpoint(endpoint)
            .setConnectTimeout(5000)
            .setReadTimeout(5000);

    public static void main(String[] args) {
        // Create an instance
        EscloudApi api = new EscloudApi(apiClient);
```
