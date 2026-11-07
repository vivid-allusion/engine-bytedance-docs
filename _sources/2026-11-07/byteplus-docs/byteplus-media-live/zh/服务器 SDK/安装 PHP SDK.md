---
title: "安装 PHP SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-php-sdk-zh-CN"
---

本主题介绍如何安装 PHP SDK，并提供示例代码以帮助加快您的开发流程。

<span id="cda34ca7"></span>
## 前提条件


* 访问密钥：请参阅[服务端 SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-CN)。

* 环境要求：需要 PHP 7.1 或更高版本。您可以通过运行 `php -v` 命令来检查 PHP 版本。如果未安装 PHP，请访问 [php.net](https://www.php.net/downloads.php) 下载并安装相应版本。

* 您必须全局安装 Composer 工具。更多信息，请参见[全局安装 Composer 工具](https://getcomposer.org/doc/00-intro.md#globally)。


<span id="ba817d14"></span>
## 安装或升级 SDK

在终端中运行以下命令以安装最新版本的 PHP SDK：

```Groovy
composer require byteplus_sdk/byteplus-sdk-php
```


在终端中运行以下命令以升级到最新版本的 PHP SDK：

```Python
composer update
```


<span id="afc40932"></span>
## 设置访问密钥

要设置 **Access Key ID** 和 **Secret Access Key**，您可以采用以下任一方法：


* 将 `BYTEPLUS_ACCESSKEY` 环境变量设置为您的 **Access Key ID**，并将 `BYTEPLUS_SECRETKEY` 环境变量设置为您的 **Secret Access Key**。

* 调用 API 时传递 **Access Key ID** 和 **Secret Access Key**。示例代码如下。

   ```PHP
   instance := live_v20230101.NewInstance()
   instance.SetCredential(base.Credentials{
           AccessKeyID: "Access Key ID",
           SecretAccessKey: "Secret Access Key",
   })
   ```
