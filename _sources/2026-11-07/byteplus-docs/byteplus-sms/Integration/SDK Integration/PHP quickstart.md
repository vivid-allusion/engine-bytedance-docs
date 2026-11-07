---
title: "PHP quickstart"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-php-quickstarts"
---

Use BytePlus SDK for PHP to call SendSms API so that you can send a text message to a group of recipients by using an example file.

<span id="3b20f162"></span>
## Prerequisites


* PHP Composer is installed.

   Composer is the standard package manager for PHP web development.

* Have generated AK (Access Key) and SK (Secret Key).

   If you haven't generated AK/SK yet, go to [BytePlus Console](https://console.byteplus.com/auth/login/) \> **User Profile** \> **IAM** \> **Key Management** \> **Create New Access Key**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Each BytePlus account can have maximum 2 pairs of AK/SK at the same time.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/1510f12-AKSK.png) </span>


<span id="268ca02d"></span>
## Downloading SDK for PHP

The SDK for PHP provides an example project file called [DemoSendSms.php](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Sms) for you to quickly call SendSms API.

To download the SDK, follow the steps:


1. Go to [BytePlus SDK for PHP](https://github.com/byteplus-sdk/byteplus-sdk-php).

2. In the upper right corner, click **Code** \> **Download ZIP**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/073ea20-PHP.png) </span>


<span id="94bbccef"></span>
## Installing the SDK

In the terminal window, run the following command to install BytePlus SDK for PHP.

```php
composer require byteplus_sdk/byteplus-sdk-php
```


<span id="78139bd0"></span>
## Setting up authentication

Open the example file [DemoSendSms.php](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Sms).

To set up authentication by AK/SK, fulfill your AK and SK in the example file as shown below.

Meanwhile, you can also specify the region as **ap\-singapore\-1** in the same file.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This is the recommended way to set up authentication.</div>


```php
$client = Sms::getInstance('your region');
$client->setAccessKey("your ak");
$client->setSecretKey("your sk");
```


Alternatively, you can also fulfill your AK and SK in the environment variable setting as shown below.

```php
BYTEPLUS_ACCESSKEY="your ak"  
BYTEPLUS_SECRETKEY="your sk"
```


Otherwise, you can fulfill your AK and SK by creating a JSON file under ～/.byteplus/config as shown below.

```php
{"ak":"your ak","sk":"your sk"}
```


Sending text messages using SendSms API


1. Fulfill the parameters in the body section of the example file **DemoSendSms.php** as shown below. To understand the parameters, refer to [SendSms](https://docs.byteplus.com/byteplus-sms/docs/sendsms).


```php
<?php
require('../../vendor/autoload.php');
use Byteplus\Service\Sms;
use Byteplus\Models\Vod\Request\VodApplyUploadInfoRequest;
use Byteplus\Models\Vod\Response\VodApplyUploadInfoResponse;

$client = Sms::getInstance('ap-singapore-1');
$client->setAccessKey("AK0000");
$client->setSecretKey("SK0000");

// template
$template = [
    'code' => 1111,
    'time' => 10,
];

$body = [
    'SmsAccount' => "19cb0000",
    'From' => "BytePlus",
    "TemplateID"=>    "SPT_1ba0000",
    "TemplateParam"=> json_encode($template),
    "PhoneNumbers"=>  "+6500000000",
    "Tag"=>           "tag",
];

$response = $client->sendSms(['json' => $body]);
echo $response;
```



2. In the terminal window, run the following command.


```php
php DemoSendSms.php
```


<span id="5a459868"></span>
## Result

After the text message is sent, you will receive a success message containing a MessageID in the response.
