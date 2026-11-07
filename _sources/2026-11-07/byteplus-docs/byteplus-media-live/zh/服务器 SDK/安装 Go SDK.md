---
title: "安装 Go SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-golang-sdk-zh-CN"
---

本主题介绍如何安装 Go SDK，并提供示例代码以帮助加快您的开发流程。

<span id="b4fa9856"></span>
## 前提条件


* 访问密钥：请参阅[服务端 SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-CN)。

* 环境要求：需安装 Go 1.13 或更高版本。有关下载和安装 Go 编译器、工具和库的说明，请参见[安装文档](https://go.dev/doc/install)。


<span id="9ee0aef8"></span>
## 安装或升级 SDK

在终端中运行以下命令以安装最新版本的 Go SDK：

```Python
go get github.com/byteplus-sdk/byteplus-sdk-golang
```


在终端中运行以下命令以升级到最新版本的 Go SDK：

```Groovy
go get -u github.com/byteplus-sdk/byteplus-sdk-golang
```


<span id="fe00307b"></span>
## 设置访问密钥

要设置**Access Key ID**和**Secret Access Key**，您可以采用以下任一方法：


* 将`BYTEPLUS_ACCESSKEY`环境变量设置为您的**Access Key ID**，并将`BYTEPLUS_SECRETKEY`环境变量设置为您的**Secret Access Key**。

* 调用 API 时传递**Access Key ID**和**Secret Access Key**。示例代码如下。

   ```Go
   instance := live_v20230101.NewInstance()
   instance.SetCredential(base.Credentials{
           AccessKeyID: "Access Key ID",
           SecretAccessKey: "Secret Access Key",
   })
   ```
