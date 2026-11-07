---
title: "Java  SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-java-sdk"
---

This article introduces how to install the Java SDK and provides code examples to help you accelerate your development process.

<span id="07886c25"></span>
## **Prerequisites**


* Access key, refer to [Server SDK overview](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk#get-access-key).

* Environmental requirements: JDK 1.8.0_131 or later is required.


<span id="11dcf149"></span>
## Installing the SDK

Add the following dependencies to your project:

```Groovy
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-sdk-java</artifactId>
    <version>latest</version>
</dependency>
```


<span id="9f843183"></span>
## Setting the Access key

To set the **Access Key ID** and **Secret Access Key**, you can use either of the following methods:


* Set the environment variables `BYTEPLUS_ACCESSKEY` as **Access Key ID** and `BYTEPLUS_SECRETKEY` as **Secret Access Key**.

* Pass the **Access Key ID** and **Secret Access Key** when calling the API. The code sample is as follows:

   ```Java
   LiveService service = LiveService.getInstance();
           service.setAccessKey("Access Key ID");
           service.setSecretKey("Secret Access Key");
   ```
