---
title: "安装 Java SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-java-sdk-zh-CN"
---

本主题介绍如何安装 Java SDK，并提供示例代码以帮助加快您的开发流程。

<span id="07886c25"></span>
## 前提条件


* 访问密钥：请参阅 [服务端 SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-CN)。

* 环境要求：需要 JDK 1.8.0_131 或更高版本。


<span id="11dcf149"></span>
## 安装 SDK

将以下依赖项添加到您的项目中：

```Groovy
<dependency>
    <groupId>com.byteplus</groupId>
    <artifactId>byteplus-sdk-java</artifactId>
    <version>latest</version>
</dependency>
```


<span id="9f843183"></span>
## 设置访问密钥

要设置 **Access Key ID** 和 **Secret Access Key**，您可以采用以下任一方法：


* 将 `BYTEPLUS_ACCESSKEY` 环境变量设置为您的 **Access Key ID**，并将 `BYTEPLUS_SECRETKEY` 环境变量设置为您的 **Secret Access Key**。

* 调用 API 时传递 **Access Key ID** 和 **Secret Access Key**。示例代码如下。

   ```Java
   LiveService service = LiveService.getInstance();
           service.setAccessKey("Access Key ID");
           service.setSecretKey("Secret Access Key");
   ```
