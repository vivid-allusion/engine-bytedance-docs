---
title: "PHP SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-php-sdk"
---

This article introduces how to install the PHP SDK and provides code examples to help you accelerate your development process.

<span id="cda34ca7"></span>
## **Prerequisites**


* Access key, refer to [Server SDK overview](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-server-sdk#get-access-key).

* Environmental requirements: PHP 7.1 or higher is required. You can check the PHP version through the `php -v` command. If PHP is not installed, visit [php.net](https://www.php.net/downloads.php) to download and install the appropriate version.

* You must globally install the Composer tool. For more information, see [Globally install the Composer tool](https://getcomposer.org/doc/00-intro.md#globally).


<span id="ba817d14"></span>
## Installing or Upgrade the SDK

In terminal, run the following command to install the latest version of the PHP SDK through Composer:

```Groovy
composer require byteplus_sdk/byteplus-sdk-php
```


In terminal, run the following command to upgrade the current version to the latest version of the PHP SDK through Composer:

```Python
composer update
```


<span id="afc40932"></span>
## Setting the Access key

To set the **Access Key ID** and **Secret Access Key**, you can use either of the following methods:


* Set the environment variables `BYTEPLUS_ACCESSKEY` as **Access Key ID** and `BYTEPLUS_SECRETKEY` as **Secret Access Key**.

* Pass the **Access Key ID** and **Secret Access Key** when calling the API. The code sample is as follows:

   ```Go
   instance := live_v20230101.NewInstance()
   instance.SetCredential(base.Credentials{
           AccessKeyID: "Access Key ID",
           SecretAccessKey: "Secret Access Key",
   })
   ```
