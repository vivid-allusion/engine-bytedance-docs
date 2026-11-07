---
title: "PHP SDK"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/PHP_SDK"
---

<span id="_1-使用说明："></span>
# 1. Instructions for use:

PHP version requirement \> = 7.4.

<span id="_1-1-composer方式安装"></span>
## 1.1 Installation in composer mode

<span id="_1-1-1-添加依赖"></span>
### 1.1.1 Add dependencies

Add dependencies in composer.json: (\> = 1.0.7 versions only support saas, ^ 1.0 means using the latest version)

```json
{
"require": {
        "datarangers/datarangers": "^1.0"
    }
}
```


<span id="_1-2-2安装依赖"></span>
### 1.2.2 Install dependencies

Execute the command:

```bash
composer require datarangers/datarangers
```


<span id="_1-2-源码安装方式"></span>
## 1.2 Source code installation method

In order for you to better understand and use our SDK, we have open sourced the SDK to https://github.com/volcengine/datarangers\-sdk\-php. You can directly download and use the SDK source code.

<span id="_2-配置初始化"></span>
# 2. Configuration initialization

<span id="8811651b"></span>
## Preparation: Get the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="48881e04"></span>
### SaaS\-cloud\-native


|SaaS\-cloud native environment<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|
|https://gator.uba.ap\-southeast\-1.bytepluses.com |* Report address: https://mcs.tobsnssdk.com<br><br>* OpenAPI Domain Name: https://analytics.byteplusapi.com |


<span id="c06d092e"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-1-saas初始化"></span>
## 2.1 SaaS initialization

```php
//initialize
CollectorConfig::init_datarangers_collector([
    "domain" => "https://xxxx",
    "save" => false,
    "headers" => [
        "Content-Type" => "application/json"
    ],
    // configure app_id => app_key, 1001 is an example application id, which needed to be replaced with the actual application id
    "app_keys" => [
        1001 => getenv("APP_KEY")
    ],
    // configure openapi, only SaaS-non cloud native should be configured, and you do not need to configure SaaS-cloud native and privatization version
    "openapi" => [
        "domain" => "https://xxxx",
        "ak" => getenv("OPENAPI_AK"),
        "sk" => getenv("OPENAPI_SK")
    ]
]);
```


Configuration instructions


* Domain: Configure different addresses according to the access environment, see the above [Preparation: Get the data upload address](https://docs.byteplus.com/docs/DataFinder/PHP_SDK#8811651b)section.

* Save: SaaS cloud\-native environment only supports save as false.

* app_keys: APP Key of the application.

   * In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>

* OpenAPI: SaaS\-cloud native version does not need to set OpenAPI:

   * Domain: The domain name of OpenAPI.

   * Ak/sk Please contact the account manager to obtain


<span id="_2-2-私有化初始化"></span>
## 2.2 Initialization of privatization

<span id="_2-2-1-logagent-模式"></span>
### 2.2.1 Logagent mode

It needs to be used with the loagent.

```php
CollectorConfig::init_datarangers_collector([
    "save" => true,
    "logger_file_prefix" => "sdk/log/",
    "logger_file_name" => "datarangers.log",
    "log_max_bytes" => 1024 * 10
]);
$rc = new AppEventCollector();
```


<span id="_2-2-2-http-模式"></span>
### 2.2.2 HTTP mode

```php
//initialize
CollectorConfig::init_datarangers_collector([
    "domain" => "https://xxxx",
    "save" => false,
    "headers" => [
        "Content-Type" => "application/json"
    ],
    "http_timeout"=> 10000
]);
$rc = new AppEventCollector();
```


<span id="_2-3-配置说明"></span>
## 2.3 Configuration Instructions

The imported parameter of the init_datarangers_collector method is an array, and the specific parameters are


|Pattern |Parameter name |Is it necessary? |Explain |
|---|---|---|---|
|Http mode |save |Yes |Http mode is false |
||domain |Yes |DataRangers' domain name or ip, supports http and https |
||headers |No |Http header. |
||http_timeout |No |Http request timed out in milliseconds. Default is 1000. |
|LogAgent pattern |save |Yes |True in LogAgent mode, only privatization is supported |
||logger_file_prefix |No |log storage path |
||logger_file_name |No |log storage file name |
||log_max_bytes |Yes |The maximum size of the log, beyond which the log will be split |


<span id="_3-接口说明"></span>
# 3. Interface description

The SDK provides a Collector interface, the specific interface is as follows.

<span id="ed04f610"></span>
## Send events asynchronously

```PHP
/** * Function description: Send events asynchronously *@param $userUniqueId string uuid *@param $appId int application id *@param $Custom array User-defined public parameters, such as reporting custom public properties *@param $eventName object event name, can be array *@param $eventParams object The event parameter, which can be an array, is the same length as $eventName * For example $eventName $eventParams are * $eventName = "launch" $eventParams = ["param1"=>"param1","param2"=>"param2"] * $eventName = ["launch1","launch2"] $eventParams = [["param1"=>"param1","param2"=>"param2"],["param3"=>"param3","param4"=>"param4"]] */
public function sendEvent($userUniqueId, $appId, $custom, $eventName, $eventParams);
```


<span id="21c7d18c"></span>
## Set user properties

```PHP
/** * Function description: Set the user's properties *@param $userUniqueId string uuid *@param $appId int application id *@param $eventParams array User properties to be set example ["php_version" = > "1.3.0"] *@return mixed */
public function profileSet($userUniqueId, $appId, $eventParams);
```


<span id="9095218e"></span>
## Delete user attributes

```PHP
/** * Function description: Delete user's attributes *@param $userUniqueId string *@param $appId int *@param $eventParams array User properties to remove example ["php_version "=>""]. unset php_version *@return mixed */
public function profileUnset($userUniqueId, $appId, $eventParams);
```


<span id="77c2c522"></span>
## Set user properties (set once)

```PHP
/** * Function description: Set user properties, do not set if they exist, and create if they do not exist. It is suitable for first-time related user properties, such as first access time, etc. *@param $userUniqueId string *@param $appId int *@param $eventParams array set once profile example ["php_version"=>"1.1"]. set php_version only once *@return mixed */
public function profileSetOnce($userUniqueId, $appId, $eventParams);
```


<span id="e377528a"></span>
## Set user properties (Increment)

```PHP
/** * Function description: Set user properties of numeric types, which can be accumulated *@param $userUniqueId string *@param $appId int *@param $eventParams array increment profile example ["php_example"=>10]. php_example=php_example+10 *@return mixed */
public function profileIncrement($userUniqueId, $appId, $eventParams);
```


<span id="63cbe4eb"></span>
## Set user properties (append)

```PHP
/** * Function description: Set user attributes, continuously add user attributes *@param $userUniqueId string *@param $appId int *@param $eventParams array append profile example ["php_version"=>["1.1","1.2"]]. append php_version *@return mixed */
public function profileAppend($userUniqueId, $appId, $eventParams);
```


<span id="a9f3e1e7"></span>
## Set up business objects (items)

```PHP
/** * Function description: Set up business objects *@param $appId int app id *@param $itemName string The name of the business object *@param $Items array business object class, need to inherit Items class, note for example: ["item_id" = > "0001", "item_name" = > "book", "item_price" = > 5.0] *@return mixed */
public function itemSet($appId, $itemName, $items);
```


<span id="1863332d"></span>
## Delete business objects (items)

```PHP
/** * Function description: Delete the properties of the item *@param $appId int *@param $itemName string *@param $itemId string *@param $Items The item attribute to be removed example: ["param1", "param2", "param3"] *@return mixed */
public function itemUnset($appId, $itemName, $itemId, $items);
```


<span id="f8572663"></span>
## Set user properties (WithHeader)

```PHP
/** * set user profile *@param $header Header *@param $eventParams array set profile example ["php_version"=>"1.3.0"] *@return mixed */
public function profileSetWithHeader($header, $eventParams);
```


<span id="585a6543"></span>
## Delete user attributes (WithHeader)

```PHP
/** *@param $header Header *@param $eventParams array unset profile example ["php_version"=>""]. unset php_version *@return mixed */
public function profileUnsetWithHeader($header, $eventParams);
```


<span id="0e0f6915"></span>
## Set user properties (SetOnceWithHeader)

```PHP
/** *@param $header Header *@param $eventParams array set once profile example ["php_version"=>"1.1"]. set php_version only once *@return mixed */
public function profileSetOnceWithHeader($header, $eventParams);
```


<span id="b3bb6808"></span>
## Set user properties (IncrementWithHeader)

```PHP
/** *@param $header Header *@param $eventParams array increment profile example ["php_example"=>10]. php_example=php_example+10 *@return mixed */
public function profileIncrementWithHeader($header, $eventParams);
```


<span id="0f843cf7"></span>
## Set user properties (AppendWithHeader)

```php
/** *@param $header Header *@param $eventParams array append profile example ["php_version"=>["1.1","1.2"]]. append php_version *@return mixed */
public function profileAppendWithHeader($header, $eventParams);
```


<span id="_4-使用样例"></span>
# 4. Use sample

<span id="a91c8fc2"></span>
## 4.1 General usage

<span id="5ba5f09f"></span>
### Initialization

```PHP
//You need to initialize the configuration before using it. Here, take the initialization of saas as an example 
CollectorConfig::init_datarangers_collector([
    "domain" => "https://xxxx",
    "save" => false,
    "headers" => [
        "Content-Type" => "application/json"
    ],
    // configure app_id => app_key, 1001 is an example application id, which needed to be replaced with the actual application id
    "app_keys" => [
        1001 => getenv("APP_KEY")
    ],
    // configure openapi
    "openapi" => [
        "domain" => "https://xxxx",
        "ak" => getenv("OPENAPI_AK"),
        "sk" => getenv("OPENAPI_SK")
    ]
]);
```


<span id="32341856"></span>
### Report an incident

```PHP
//Use AppEventCollector for app type
$rc = new AppEventCollector();

//Application for web type using WebEventCollector
// $rc = new WebEventCollector();

//Application for Mini Program type using MpEventCollector
// $rc = new MpEventCollector();

#Report an incident
$rc->sendEvent("test-uuidsdk1", 1001, null, ["php_event"],
    [["php_name" => "php", "php_version" => "5.6"]]);
```


<span id="d966460a"></span>
### Report a single incident

```PHP
Report a single incident
$rc->sendEvent("test-uuidsdk1", 1001, null, "php_single_event",
    ["php_name" => "php", "php_version" => "5.6"]);
```


<span id="caca2b14"></span>
### Report user attributes

```PHP
#Report user attributes
$rc->profileSet("test-uuidsdk1", 1001, ["profile_php_name" => "php7", "profile_php_version" => "7.4", "profile_int" => 1]);
```


<span id="f69e5479"></span>
### Report item attributes

```PHP
#report item attributes
$rc->itemIdSet(1001, "book", "book3", ["author" => "吴承恩", "name" => "西游记", "price" => 59.90, "category" => 1]);
$rc->itemIdSet(1001, "book", "book4", ["author" => "Guanzhong Luo", "name" => "SanGuoYanYi", "price" => 69.90, "category" => 1]);
```


<span id="25225d3b"></span>
### Report items in the event

```PHP
#Report items in the event
$rc->sendEvent("test-uuidsdk1", 1001, null, ["php_event_with_item"],
    [["php_name" => "php", "php_version" => "5.6"]], [
        [["item_name" => "book", "item_id" => "book3"], ["item_name" => "book", "item_id" => "book4"]]
    ]);
```


<span id="3b94d369"></span>
### Report items in a single event

```php
#Report items in a single event
$rc->sendEvent("test-uuidsdk1", 1001, null, "php_single_event_with_item",
    ["php_name" => "php", "php_version" => "5.6"],
    [["item_name" => "book", "item_id" => "book3"], ["item_name" => "book", "item_id" => "book4"]]
);
```


<span id="4f51a37e"></span>
## 4.2 Special Usage

<span id="14a2da79"></span>
### Use device_id report anonymously

```PHP
//Use device_id report anonymously
$header2 = new Header();
$header2->setAppId(10000000);
$header2->setUserUniqueId("");
$header2->setDeviceId(7033713549469860107);
$rc->profileSetWithHeader($header2, ["profile_php_name" => "php7", "profile_php_version" => "7.4", "profile_int" => 2, "testdate"=>"2023-05-16"]);
```


<span id="807bbf3f"></span>
### Use anonymousId to report anonymously

```PHP
//Use anonymousId to report anonymously
$webRc = new WebEventCollector();
$header3 = new Header();
$header3->setAppId(10000000);
$header3->setUserUniqueId("");
$header3->setAnonymousId("test_anonymousId1");
$webRc->sendUserDefineEvent($header3, "", 10000000, null, "php_event_with_anonymous_id",
    ["php_name" => "php", "php_version" => "5.6", "float_param" => floatval(5), "session_id" => "1234567890"]);
```


<span id="a661ce52"></span>
### Multi\-criteria reporting using user_unique_id_type

```PHP
//Use user_unique_id_type for multi-criteria reporting, version requirements: > = 1.0.12
$appRc = new AppEventCollector();
$header3 = new Header();
$header3->setAppId(10000000);
$header3->setUserUniqueIdType("phone_id");
$appRc->sendUserDefineEvent($header3, "test_sdk_phone_id1", 10000000, null, "php_event_with_anonymous_id",
    ["php_name" => "php", "php_version" => "5.6", "float_param" => floatval(5), "session_id" => "1234567890"]);
```


<span id="_5-注意事项"></span>
# 5. Precautions


1. The generated log files are not automatically deleted. Please delete them yourself.

2. The built\-in id attribute of the business object, the corresponding field name is called item_id, so there is no need to define an `id`attribute.

3. When using the PHP SDK for data access, the event tracking real\-time verification function is not currently supported for access verification.
