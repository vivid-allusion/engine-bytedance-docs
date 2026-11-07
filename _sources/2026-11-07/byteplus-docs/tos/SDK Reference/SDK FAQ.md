---
title: "SDK FAQ"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Sdk-faq"
---

This article describes common issues encountered during the use of the TOS SDK.

<span id=".57Si5byV"></span>
### Index


* S3 SDK

   * [What is the reason for the error Forbidden path to access server or InvalidPathAccess when accessing TOS using SDKs and tools that support the S3 protocol?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55So5pSv5oyBLXMzLeWNj-iurueahC1zZGst5ZKM5bel5YW36K6_6ZeuLXRvcy3ml7bvvIzmiqXplJktZm9yYmlkZGVuLXBhdGgtdG8tYWNjZXNzLXNlcnZlci3miJYtaW52YWxpZHBhdGhhY2Nlc3Mt5piv5LuA5LmI5Y6f5Zug77yf)

* Java

   * [What is the reason for using TOS Java SDK error com.fasterxml.jackson.core. JsonParseException?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1qYXZhLXNkay3miqXplJktY29tLWZhc3RlcnhtbC1qYWNrc29uLWNvcmUtanNvbnBhcnNlZXhjZXB0aW9uLeaYr-S7gOS5iOWOn-WboO-8nw==)

   * [What is the reason for using TOS Java SDK error com.fasterxml.jackson.core. JsonParseException?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1qYXZhLXNkay3miqXplJktY29tLWZhc3RlcnhtbC1qYWNrc29uLWNvcmUtanNvbnBhcnNlZXhjZXB0aW9uLeaYr-S7gOS5iOWOn-WboO-8nw==)

* C++

   * [How to handle Windows compile connection issues?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V5aSE55CGLXdpbmRvd3Mt57yW6K-R6L-e5o6l6Zeu6aKY77yf)

* Browser.js

   * [Using the TOS BrowserJS SDK to request a TOS service encounters a cross-domain problem, how to solve it?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1icm93c2VyanMtc2RrLeivt-axgi10b3Mt5pyN5Yqh6YGH5Yiw6Leo5Z-f6Zeu6aKY77yM5aaC5L2V6Kej5Yaz77yf)

   * [How does the TOS Browser. JS SDK support ListBuckets and CreateBuckets?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1icm93c2VyLWpzLXNkay3lpoLkvZXmlK_mjIEtbGlzdGJ1Y2tldHMt5ZKMLWNyZWF0ZWJ1Y2tldO-8nw==)

   * [Why does uploading objects with the TOS Browser. JS SDK feel slow?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5Li65LuA5LmI5L2_55SoLXRvcy1icm93c2VyLWpzLXNkay3kuIrkvKDlr7nosaHmhJ_op4nlvojmhaLvvJ8=)

* Python

   * [Use the TOS Python SDK to upload and download objects SignatureDoesNotMatch What is the reason?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1weXRob24tc2RrLeS4iuS8oOS4i-i9veWvueixoeaKpemUmS1zaWduYXR1cmVkb2Vzbm90bWF0Y2gt5piv5LuA5LmI5Y6f5Zug77yf)

   * [What is the reason for requesting an Unsupported Authorization Type or InvalidRequest using the TOS Python SDK?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1weXRob24tc2RrLeivt-axgi11bnN1cHBvcnRlZC1hdXRob3JpemF0aW9uLXR5cGUt5oiWLWludmFsaWRyZXF1ZXN0LeaYr-S7gOS5iOWOn-WboO-8nw==)

   * [How to solve the problem of poor performance of uploading and downloading objects after CRC verification is enabled?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V6Kej5Yaz5byA5ZCvLWNyYy3moKHpqozlkI7vvIzkuIrkvKDlkozkuIvovb3lr7nosaHmgKfog73lt67nmoTpl67popjvvJ8=)

* Common FAQ

   * [How to handle returning 400 when calling the interface?](https://docs.byteplus.com/docs/tos/Sdk-faq#.6LCD55So5o6l5Y-j5pe26L-ULTQwMC3lpoLkvZXlpITnkIbvvJ8=)

   * [Why is the client side automatically disconnected during the process of uploading or downloading objects using the TOS SDK, and errors such as unexpected eof, request timeout, and use of closed network connection are reported?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1zZGst5LiK5Lyg5oiW5LiL6L295a-56LGh6L-H56iL5Lit5a6i5oi356uv6Ieq5Yqo5pat5byA77yM5oql6ZSZLXVuZXhwZWN0ZWQtZW9m44CBcmVxdWVzdC10aW1lb3V044CBdXNlLW9mLWNsb3NlZC1uZXR3b3JrLWNvbm5lY3Rpb24t562J6ZSZ6K-v5piv5Li65LuA5LmI77yf)

   * [The server returned an invalid body.](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1zZGst6K-35rGC5oql6ZSZLXNlcnZlci1yZXR1cm5lZC1hbi1pbnZhbGlkLWJvZHkt5piv5LuA5LmI5Y6f5Zug77yf)

   * [How to obtain error codes and error messages using the TOS SDK?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1zZGst5aaC5L2V6I635Y-W6ZSZ6K-v56CB44CB6ZSZ6K-v5L-h5oGv77yf)

   * [What is the principle of using the TOS SDK to generate a pre-signed URL?Will you interact with the server level?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1zZGst55Sf5oiQ6aKE562-5ZCNLXVybC3mmK_ku4DkuYjljp_nkIbvvJ_mmK_lkKbkvJrkuI7mnI3liqHnq6_kuqTkupLvvJ8=)

   * [When using the TOS SDK to upload objects containing special characters (e.g. spaces, Chinese), do I need URL encoding?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1zZGst5LiK5Lyg5YyF5ZCr54m55q6K5a2X56ym77yI5aaC56m65qC844CB5Lit5paH77yJ55qE5a-56LGh5pe277yM6ZyA6KaBLXVybC3nvJbnoIHlkJfvvJ8=)

   * [Why is a .temp temporary file generated when downloading files using the TOS SDK DownloadFile interface?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1zZGstZG93bmxvYWRmaWxlLeaOpeWPo-S4i-i9veaWh-S7tuaXtuS4uuS7gOS5iOS8muS6p-eUny10ZW1wLeS4tOaXtuaWh-S7tu-8nw==)

   * [How does TOS SDK use STS Token to initialize client side?](https://docs.byteplus.com/docs/tos/Sdk-faq#.dG9zLXNkay3lpoLkvZXkvb_nlKgtc3RzLXRva2VuLeWIneWni-WMluWuouaIt-err--8nw==)

   * [How to delete a directory using the TOS SDK?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V5L2_55SoLXRvcy1zZGst5Yig6Zmk55uu5b2V77yf)

   * [How to get object download link (URL) through TOS SDK?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V6YCa6L-HLXRvcy1zZGst6I635Y-W5a-56LGh5LiL6L296ZO-5o6l77yIdXJs77yJ77yf)

   * [How to use the TOS SDK to achieve shard upload, download, or copy?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V5L2_55SoLXRvcy1zZGst5a6e546w5YiG54mH5LiK5Lyg44CB5LiL6L295oiW5aSN5Yi277yf)

   * [How to open the log of the TOS SDK?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V5byA5ZCvLXRvcy1zZGst55qE5pel5b-X77yf)

   * [How to obtain data for a range of objects?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V6I635Y-W5a-56LGh5p-Q5Liq5Yy66Ze055qE5pWw5o2u77yf)

   * [How do I add a retry policy?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5aaC5L2V5re75Yqg6YeN6K-V562W55Wl77yf)

* Android

   * [Compatibility problems with TOS Android SDK, error java.lang.ClassNotFoundException or java.lang.NoClassDefFoundException How to solve?](https://docs.byteplus.com/docs/tos/Sdk-faq#.5L2_55SoLXRvcy1hbmRyb2lkLXNkay3lh7rnjrDlhbzlrrnmgKfpl67popjvvIzmiqXplJktamF2YS1sYW5nLWNsYXNzbm90Zm91bmRleGNlcHRpb24t5oiWLWphdmEtbGFuZy1ub2NsYXNzZGVmZm91bmRleGNlcHRpb24t6ZSZ6K-v5aaC5L2V6Kej5Yaz77yf)


<span id=".5L2_55So5pSv5oyBLXMzLeWNj-iurueahC1zZGst5ZKM5bel5YW36K6_6ZeuLXRvcy3ml7bvvIzmiqXplJktZm9yYmlkZGVuLXBhdGgtdG8tYWNjZXNzLXNlcnZlci3miJYtaW52YWxpZHBhdGhhY2Nlc3Mt5piv5LuA5LmI5Y6f5Zug77yf"></span>
### What is the reason for the error Forbidden path to access server or InvalidPathAccess when accessing TOS using SDKs and tools that support the S3 protocol?

The above error is caused by using the PathStyle request method. TOS does not support the path style (i.e. PathStyle) request method, only supports the request method using the [virtual host ](https://docs.aws.amazon.com/AmazonS3/latest/userguide/VirtualHosting.html?spm=a2c4g.11186623.0.0.6b9d64012JMDoP)(i.e. VirtualHostStyle).

The main difference between Path and VirtualHost is the location of the bucket name in the HTTP URL, as follows:

```Plain
# Path access method
https://tos-s3-cn-beijing.bytepluses.com.cn/{bucketname} 

# VirtualHost access method
https://{bucketname}.tos-s3-cn-beijing.bytepluses.com.cn
```


When accessing TOS using various SDKs and tools that support the S3 protocol, be sure to configure the VirtualHostStyle request method. For example:


* When using the AWS S3 Java SDK, you need to ensure that the configuration parameter that disables PathStyle is set during client\-side initialization: `AmazonS3Builder. withPathStyleAccessEnabled (false)`.

* When accessing TOS using the AWS CLI tool, you need to add addressing_style = virtual content to the ~/.aws/conf`addressing_style = virtual content to the ~/.aws/config`file, ensuring that the request method is VirtualHostStyle.


<span id=".5L2_55SoLXRvcy1qYXZhLXNkay3miqXplJktY29tLWZhc3RlcnhtbC1qYWNrc29uLWNvcmUtanNvbnBhcnNlZXhjZXB0aW9uLeaYr-S7gOS5iOWOn-WboO-8nw=="></span>
### What is the reason for using TOS Java SDK error com.fasterxml.jackson.core. JsonParseException?

The above error is usually due to the domain name (Endpoint) error of the TOS service set when initializing the client side. The TOS SDK currently only supports the use of TOS protocol domain names (for example, the Beijing regional domain name is tos\-cn\-beijing.bytepluses.com.cn), and does not support the use of S3 protocol domain names (for example, Beijing tos\-s3\-cn\-beijing.bytepluses.com.cn). For domain name information supported by TOS, please refer to [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

<span id=".amF2YS1zZGst54mI5pys5L6d6LWW566h55CG"></span>
### Java SDK Version Dependency Management

The following lists the dependency packages and versions of the TOS Java SDK. If you encounter `java.lang. NoSuchMethodError`, `java.lang. ClassNotFoundException`and other errors, you can compare and refer to the following dependencies to solve the problem of dependency conflicts.

```java
<dependencies>
    <dependency>
        <groupId>com.squareup.okhttp3</groupId>
        <artifactId>okhttp</artifactId>
        <version>4.9.2</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-annotations</artifactId>
        <version>2.12.5</version>
    </dependency>
    <dependency>
        <groupId>com.fasterxml.jackson.core</groupId>
        <artifactId>jackson-databind</artifactId>
        <version>2.12.5</version>
    </dependency>
    <dependency>
        <groupId>org.slf4j</groupId>
        <artifactId>slf4j-api</artifactId>
        <version>1.7.25</version>
        <scope>compile</scope>
    </dependency>
```


TOS Java okhttp client that the SDK relies on, relying on the 1.4.10 version of kotlin\-stdlib. If you encounter a dependency conflict error with okhttp client, you can declare the 1.4.10 version of kotlin\-stdlib component dependencies in the outermost pom.xml.

```java
<dependency>
  <groupId>org.jetbrains.kotlin</groupId>
  <artifactId>kotlin-stdlib</artifactId>
  <version>1.4.10</version>
  <scope>compile</scope>
</dependency>
```


<span id=".5aaC5L2V5aSE55CGLXdpbmRvd3Mt57yW6K-R6L-e5o6l6Zeu6aKY77yf"></span>
### How to handle Windows compile connection issues?


* If prompted that MSVCR.120 dll cannot be found, you need to click the [link ](https://www.microsoft.com/zh-cn/download/confirmation.aspx?id=40784)to install Visual C++.

* If you get an error of 0xc000007b, you need to check if you are linking to the correct DLL.


<span id=".5L2_55SoLXRvcy1icm93c2VyanMtc2RrLeivt-axgi10b3Mt5pyN5Yqh6YGH5Yiw6Leo5Z-f6Zeu6aKY77yM5aaC5L2V6Kej5Yaz77yf"></span>
### Using the TOS BrowserJS SDK to request a TOS service encounters a cross\-domain problem, how to solve it?

You need to configure the CORS policy of the bucket first to allow cross\-domain requests. For detailed configuration methods, please refer to [Cross-Origin Resource Sharing Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).

<span id=".5L2_55SoLXRvcy1icm93c2VyLWpzLXNkay3lpoLkvZXmlK_mjIEtbGlzdGJ1Y2tldHMt5ZKMLWNyZWF0ZWJ1Y2tldO-8nw=="></span>
### How does the TOS Browser. JS SDK support ListBuckets and CreateBuckets?

due to [Cross-Origin Resource Sharing Settings](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings)(CORS policy) is configured on buckets, so the BrowserJS SDK cannot support ListBuckets and CreateBuckets.

<span id=".5Li65LuA5LmI5L2_55SoLXRvcy1icm93c2VyLWpzLXNkay3kuIrkvKDlr7nosaHmhJ_op4nlvojmhaLvvJ8="></span>
### Why does uploading objects with the TOS Browser. JS SDK feel slow?

There are two reasons for this problem:


* For a single large object (MB + level), since the TOS BrowserJS SDK is transmitted from the public network through the user's browser, it is limited by the bandwidth of the user's local network from the public network to the TOS service. In the case of weak connection (such as uploading using the browser on the mobile end) and slow network, the entire upload may take a long time.

* In the case of batch uploading of multiple objects, due to the concurrency limit of the browser itself (e.g. Google Chrome's concurrency limit is 6), it is impossible to perform higher concurrent upload requests, resulting in slower batch uploads overall.


<span id=".5L2_55SoLXRvcy1weXRob24tc2RrLeS4iuS8oOS4i-i9veWvueixoeaKpemUmS1zaWduYXR1cmVkb2Vzbm90bWF0Y2gt5piv5LuA5LmI5Y6f5Zug77yf"></span>
### Use the TOS Python SDK to upload and download objects SignatureDoesNotMatch What is the reason?

The reasons for the error are usually as follows:


* When initializing the client side, the AK/SK used was incorrect.

* Upload/download the object name to `.` The current Python SDK does not support object names starting with `.`


If the error is not caused by the above reasons, please submit work order to contact technical support.

<span id=".5L2_55SoLXRvcy1weXRob24tc2RrLeivt-axgi11bnN1cHBvcnRlZC1hdXRob3JpemF0aW9uLXR5cGUt5oiWLWludmFsaWRyZXF1ZXN0LeaYr-S7gOS5iOWOn-WboO-8nw=="></span>
### What is the reason for requesting an Unsupported Authorization Type or InvalidRequest using the TOS Python SDK?

The above error is usually due to the domain name (Endpoint) error of the TOS service set when initializing the client side. The TOS SDK currently only supports the use of TOS protocol domain names (for example, the Beijing regional domain name is tos\-cn\-beijing.bytepluses.com.cn), and does not support the use of S3 protocol domain names (for example, Beijing tos\-s3\-cn\-beijing.bytepluses.com.cn). For domain name information supported by TOS, please refer to [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

<span id=".5aaC5L2V6Kej5Yaz5byA5ZCvLWNyYy3moKHpqozlkI7vvIzkuIrkvKDlkozkuIvovb3lr7nosaHmgKfog73lt67nmoTpl67popjvvJ8="></span>
### How to solve the problem of poor performance of uploading and downloading objects after CRC verification is enabled?

You can set `enable_crc = False`to turn off CRC checking. For more information, please refer to [Initializing the Client Side (Python SDK)](https://docs.byteplus.com/docs/tos/Initializing-the-client-side-python-sdk).

<span id=".6LCD55So5o6l5Y-j5pe26L-ULTQwMC3lpoLkvZXlpITnkIbvvJ8="></span>
### How to handle returning 400 when calling the interface?

Failed to call the interface, HTTP status code returns 400, indicating that the configuration or parameters on the client side are wrong, and reconfigure according to the returned information prompt.

<span id=".5L2_55SoLXRvcy1zZGst5LiK5Lyg5oiW5LiL6L295a-56LGh6L-H56iL5Lit5a6i5oi356uv6Ieq5Yqo5pat5byA77yM5oql6ZSZLXVuZXhwZWN0ZWQtZW9m44CBcmVxdWVzdC10aW1lb3V044CBdXNlLW9mLWNsb3NlZC1uZXR3b3JrLWNvbm5lY3Rpb24t562J6ZSZ6K-v5piv5Li65LuA5LmI77yf"></span>
### Why is the client side automatically disconnected during the process of uploading or downloading objects using the TOS SDK, and errors such as unexpected eof, request timeout, and use of closed network connection are reported?

The above error is usually caused by the high latency of the network from the client side to the TOS server (triggering the client side\-server level disconnection and then requesting an interrupt), such as the client side's network is too slow, the client side bandwidth is too low, the client side requests excessive bandwidth, the client side CPU is too high, resulting in abnormal sending and receiving flows, etc. It is recommended that you first confirm the current network of the client side and the load of the program operating environment. If there is no problem with the above, you can submit work order to **c**ontact technical support.

<span id=".5L2_55SoLXRvcy1zZGst6K-35rGC5oql6ZSZLXNlcnZlci1yZXR1cm5lZC1hbi1pbnZhbGlkLWJvZHkt5piv5LuA5LmI5Y6f5Zug77yf"></span>
### The server returned an invalid body.

The above error is usually due to the wrong configuration of the domain name (Endpoint) of the TOS service. The TOS SDK currently only supports the use of the TOS protocol domain name (for example, the Beijing regional domain name is tos\-cn\-beijing.bytepluses.com.cn), and does not support the use of the S3 protocol domain name (for example, Beijing tos\-s3\-cn\-beijing.bytepluses.com.cn). For information on the domain names supported by TOS, please see [Region and Endpoint](https://docs.byteplus.com/docs/tos/docs-region-and-endpoint).

<span id=".5L2_55SoLXRvcy1zZGst5aaC5L2V6I635Y-W6ZSZ6K-v56CB44CB6ZSZ6K-v5L-h5oGv77yf"></span>
### How to obtain error codes and error messages using the TOS SDK?

The TOS SDK uniformly defines server level errors (TosServerError) and client side errors (TosClientError). For detailed access to error codes for each SDK, please refer to the following documents:


* [Exception Handling (Java SDK)](https://docs.byteplus.com/docs/tos/Exception-handling-java-sdk)

* [Exception Handling (Go SDK)](https://docs.byteplus.com/docs/tos/Exception-handling-go-sdkSDK)

* [Exception Handling (Python SDK)](https://docs.byteplus.com/docs/tos/Exception-handling-python-sdk)

* [Exception Handling (C++ SDK)](https://docs.byteplus.com/docs/tos/Exception-handling-c-sdk)


<span id=".5L2_55SoLXRvcy1zZGst55Sf5oiQ6aKE562-5ZCNLXVybC3mmK_ku4DkuYjljp_nkIbvvJ_mmK_lkKbkvJrkuI7mnI3liqHnq6_kuqTkupLvvJ8="></span>
### What is the principle of using the TOS SDK to generate a pre\-signed URL?Will you interact with the server level?

The pre\-signed URL is generated entirely locally by the TOS SDK through the signature algorithm, does not interact with the server level, and therefore does not verify the validity (e.g. the existence of a bucket, the existence of an object, etc.). Only when the pre\-signed URL is used for the actual request will the pre\-signed URL be validated.

<span id=".5L2_55SoLXRvcy1zZGst5LiK5Lyg5YyF5ZCr54m55q6K5a2X56ym77yI5aaC56m65qC844CB5Lit5paH77yJ55qE5a-56LGh5pe277yM6ZyA6KaBLXVybC3nvJbnoIHlkJfvvJ8="></span>
### When using the TOS SDK to upload objects containing special characters (e.g. spaces, Chinese), do I need URL encoding?

No, the TOS SDK will handle the issue of special characters by itself to ensure that the object name in the bucket is the same as the object name passed in after uploading.

<span id=".5L2_55SoLXRvcy1zZGstZG93bmxvYWRmaWxlLeaOpeWPo-S4i-i9veaWh-S7tuaXtuS4uuS7gOS5iOS8muS6p-eUny10ZW1wLeS4tOaXtuaWh-S7tu-8nw=="></span>
### Why is a .temp temporary file generated when downloading files using the TOS SDK DownloadFile interface?

When the TOS SDK downloads an object, it will first generate a `.temp`temporary file and write the downloaded data to the temporary file. When the temporary file is completely written successfully, it will be renamed to the final file to avoid the existing file being overwritten by the intermediate state file that has not been written. The existing file is damaged.

<span id=".dG9zLXNkay3lpoLkvZXkvb_nlKgtc3RzLXRva2VuLeWIneWni-WMluWuouaIt-err--8nw=="></span>
### How does TOS SDK use STS Token to initialize client side?

The TOS SDK supports generating client side through temporary AK, temporary SK and STS Token. The initialization examples of common mainstream languages are as follows:


* [Configure STS(Java SDK)](https://docs.byteplus.com/en/docs/tos/Initialize-client-side-java-sdk#configure-sts)

* [Configure STS(Go SDK)](https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-go-sdk#configure-sts)

* [Configure STS(Python SDK)](https://docs.byteplus.com/en/docs/tos/Initializing-the-client-side-python-sdk#configure-sts)

* [Configure STS(C++)](https://docs.byteplus.com/en/docs/tos/Initialize-client-side-c-sdk#configure-sts)


<span id=".5aaC5L2V5L2_55SoLXRvcy1zZGst5Yig6Zmk55uu5b2V77yf"></span>
### How to delete a directory using the TOS SDK?

The TOS API does not provide an interface for deleting directories. Using the TOS SDK can be achieved by combining enumerating objects and deleting object interfaces. You can refer to the following documentation settings:


* [Java SDK](https://docs.byteplus.com/en/docs/tos/catalog-scenes-java-sdk#delete-directory)

* [Go SDK](https://docs.byteplus.com/en/docs/tos/Directory-scenes-go-sdk#delete-files-in-directory)

* [Python SDK](https://docs.byteplus.com/en/docs/tos/Directory-scenes-python-sdk#delete-directory)

* [C++](https://docs.byteplus.com/en/docs/tos/Catalog-scenes-c-sdk#delete-directory)


If you need to periodically delete objects in the bucket, you can create a lifecycle rule. For more information, see [Setting Lifecycle Rules](https://docs.byteplus.com/docs/tos/docs-setting-lifecycle-rules).

<span id=".5aaC5L2V6YCa6L-HLXRvcy1zZGst6I635Y-W5a-56LGh5LiL6L296ZO-5o6l77yIdXJs77yJ77yf"></span>
### How to get object download link (URL) through TOS SDK?


* If the object ACL is public read, you can stitch the download link of the object by yourself, and the stitching method is `https://{bucketname}. {endpoint}/{objectkey}`.

* If the object is not publicly readable, a signed download link for the object can be generated through the PreSignedURL function of the TOS SDK.


<span id=".5aaC5L2V5byA5ZCvLXRvcy1zZGst55qE5pel5b-X77yf"></span>
### How to open the log of the TOS SDK?

The logging of the TOS SDK is turned off by default. If you need to open the logging, you can refer to the following documents:


* [Log Configuration (Java SDK)](https://docs.byteplus.com/docs/tos/Log-configuration-java-sdk)

* [Log Configuration (Go SDK)](https://docs.byteplus.com/docs/tos/Log-configuration-go-sdk)

* [Logging Configuration (Python SDK)](https://docs.byteplus.com/docs/tos/Logging-configuration-python-sdk)

* [Log Configuration (C++ SDK)](https://docs.byteplus.com/docs/tos/log-configuration-c-sdk)


<span id=".5aaC5L2V5L2_55SoLXRvcy1zZGst5a6e546w5YiG54mH5LiK5Lyg44CB5LiL6L295oiW5aSN5Yi277yf"></span>
### How to use the TOS SDK to achieve shard upload, download, or copy?

The TOS SDK uniformly encapsulates the UploadFile, DownloadFile, and ResumableCopyObject functions for shard upload, sharding download, and sharding copy, respectively. It supports setting concurrency and realizes breakpoint continuation capabilities. For detailed sample code, please refer to the SDK documentation for each language.

<span id=".5aaC5L2V6I635Y-W5a-56LGh5p-Q5Liq5Yy66Ze055qE5pWw5o2u77yf"></span>
### How to obtain data for a range of objects?

If you want to obtain the data of a certain range of the object, you can download it through the Range download method. Range download can also divide large objects into multiple Range downloads to improve download efficiency. For specific usage examples, please refer to [Scope Download (C++ SDK)](https://docs.byteplus.com/docs/tos/Scope-download-c-sdk)、[Scope Download (Java SDK)](https://docs.byteplus.com/docs/tos/Scope-download-java-sdk)、[Scope Download (Go SDK)](https://docs.byteplus.com/docs/tos/Scope-download-go-sdk)、[Scope Download (Python SDK)](https://docs.byteplus.com/docs/tos/Scope-download-python-sdk)、[Scope Download (Node.js SDK)](https://docs.byteplus.com/docs/tos/Scope-download-node-js-sdk).

<span id=".5aaC5L2V5re75Yqg6YeN6K-V562W55Wl77yf"></span>
### How do I add a retry policy?

Since the 2.1.0 version, the TOS Java SDK has added a failure retry mechanism. For 429 and 5xx errors returned by the server level, exponential backoff retries will be performed by default, and the maximum number of retries will be 3 by default. You can adjust the maximum number of retries by TOSClientConfiguration configure the maxRetryCount parameter when initializing TOSV2Client, and set it to 0 to turn off the retry mechanism. For specific instructions, please refer to [Initialize Client Side (Java SDK)](https://docs.byteplus.com/docs/tos/Initialize-client-side-java-sdk).

TOS PHP SDK and TOS. NET SDK do not have a failure retry mechanism. In the case of poor network environment, the request failure caused by the network may occur. It is recommended that you add a retry mechanism to your code according to the actual business situation.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Do not retry indefinitely. It is recommended to retry 2 to 3 times. Retry will cause the index to fall back for a period of time. If the failure rate of retries is relatively high over a period of time, it is recommended that you give up retrying.</div>


<span id=".5L2_55SoLXRvcy1hbmRyb2lkLXNkay3lh7rnjrDlhbzlrrnmgKfpl67popjvvIzmiqXplJktamF2YS1sYW5nLWNsYXNzbm90Zm91bmRleGNlcHRpb24t5oiWLWphdmEtbGFuZy1ub2NsYXNzZGVmZm91bmRleGNlcHRpb24t6ZSZ6K-v5aaC5L2V6Kej5Yaz77yf"></span>
### Compatibility problems with TOS Android SDK, error java.lang.ClassNotFoundException or java.lang.NoClassDefFoundException How to solve?

The above error is usually caused by the low Android environment version of the client, which needs to be desaccharified. For detailed configuration, please refer to [prerequisite](https://docs.byteplus.com/docs/tos/Install-the-android-sdk#%E5%89%8D%E6%8F%90%E6%9D%A1%E4%BB%B6).
