---
title: "安裝 Java SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-java-sdk-zh-TW"
---

本主題介紹如何安裝 Java SDK，並提供範例程式碼以協助加速您的開發流程。

<span id="07886c25"></span>
## 先決條件


* 存取金鑰：請參考 [Server SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-TW)。

* 環境需求：需安裝 JDK 1.8.0_131 或更高版本。


<span id="11dcf149"></span>
## 安裝 SDK

請將以下依賴項新增至您的專案：

```Groovy
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-sdk-java</artifactId>
    <version>latest</version>
</dependency>
```


<span id="9f843183"></span>
## 設定存取金鑰

若要設定 **Access Key ID** 和 **Secret Access Key**，您可以採用以下任一方法：


* 將 `BYTEPLUS_ACCESSKEY` 環境變數設為您的 **Access Key ID**，並將 `BYTEPLUS_SECRETKEY` 環境變數設為您的 **Secret Access Key**。

* 呼叫 API 時傳入 **Access Key ID** 和 **Secret Access Key**。範例程式碼如下。

   ```Java
   LiveService service = LiveService.getInstance();
           service.setAccessKey("Access Key ID");
           service.setSecretKey("Secret Access Key");
   ```
