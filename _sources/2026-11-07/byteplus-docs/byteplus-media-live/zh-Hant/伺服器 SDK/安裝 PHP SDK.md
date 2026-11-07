---
title: "安裝 PHP SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-php-sdk-zh-TW"
---

本主題介紹如何安裝 PHP SDK，並提供範例程式碼以協助加速您的開發流程。

<span id="cda34ca7"></span>
## 先決條件


* Access Key：請參閱[Server SDK 概述](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk-zh-TW)。

* 環境需求：必須使用 PHP 7.1 或更高版本。您可以透過執行 `php -v` 指令來檢查 PHP 版本。若尚未安裝 PHP，請前往 [php.net](https://www.php.net/downloads.php) 下載並安裝適合的版本。

* 您必須全域安裝 Composer 工具。如需更多資訊，請參閱[全域安裝 Composer 工具](https://getcomposer.org/doc/00-intro.md#globally)。


<span id="ba817d14"></span>
## 安裝或升級 SDK

在終端機中執行以下指令，以安裝最新版本的 PHP SDK：

```Groovy
composer require byteplus_sdk/byteplus-sdk-php
```


在終端機中執行以下指令，以升級至最新版本的 PHP SDK：

```Python
composer update
```


<span id="afc40932"></span>
## 設定 Access Key

若要設定 **Access Key ID** 和 **Secret Access Key**，您可以採用以下任一方法：


* 將 `BYTEPLUS_ACCESSKEY` 環境變數設為您的 **Access Key ID**，並將 `BYTEPLUS_SECRETKEY` 環境變數設為您的 **Secret Access Key**。

* 在呼叫 API 時傳入 **Access Key ID** 和 **Secret Access Key**。範例程式碼如下。

   ```PHP
   instance := live_v20230101.NewInstance()
   instance.SetCredential(base.Credentials{
           AccessKeyID: "Access Key ID",
           SecretAccessKey: "Secret Access Key",
   })
   ```
