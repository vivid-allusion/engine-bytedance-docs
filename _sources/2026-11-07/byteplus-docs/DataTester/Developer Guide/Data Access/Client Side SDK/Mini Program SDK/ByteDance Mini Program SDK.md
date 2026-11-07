---
title: "ByteDance Mini Program SDK"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/ByteDance-Mini-Program-SDK"
---

<span id="_1-集成"></span>
# 1. Integration

<span id="_1-1-安装sdk"></span>
## 1.1 Installing the SDK

> Install with npm


```plain
npm install @datarangers/sdk-mp
```


<span id="_1-2-域名配置准备"></span>
## **1.2 Domain name configuration preparation**

> For configuration in "Mini Program Background \- Development \- Development Settings \- Server Domain Name", please refer to the corresponding official documentation of Mini Program, such as WeChat Mini Program documentation https://developers.weixin.qq.com/miniprogram/en/dev/framework/ability/network.html


**Privatization business**: Add the data reporting domain name of the private deployment to the "request legal domain name" in the background of the Mini Program. If you don't know this domain name, please contact your project manager or customer success manager.

<span id="_1-4-旧版本说明"></span>
## **1.3 Old version description**

If you integrate an older version of the SDK (below 2.0), you need to add [https://mcs.ctobsnssdk.com ](https://mcs.ctobsnssdk.com)and [https://toblog.ctobsnssdk.com ](https://toblog.ctobsnssdk.com)to the request whitelist of the WeChat open API.

<span id="_2-初始化"></span>
# 2. Initialization

<span id="_2-1-获取appid"></span>
## **2.1 Get the appid**

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-初始化-sdk示例"></span>
## 2.2 Initializing the SDK example

<span id="_2-2-2-私有化业务"></span>
### **2.2.1 Privatization business**

Privatization requires a clear data reporting domain name. If you are unsure of this domain name, please contact your project manager or customer success manager.

```javascript
//Initialize the SDK on the entry page
// app.js
import $$Rangers from '@datarangers/sdk-mp';
$$Rangers.init({
    app_id: 0000, //Replace with the app_id of the application, refer to Section 2.1 to obtain, note that the type is number rather than string
    channel_domain: "{{DOMAIN}}", //Set up a private deployment data upload domain name, if you don't know this address, please contact your project manager or customer success manager
    log: true, //After opening, the console will print the log, which is helpful to view the event tracking report process during the development stage
    auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
    enable_ab_test: true, //start ab experiment
    ab_channel_domain: "{{ABTEST_DOMAIN}}", //Set the ab shunt interface domain name, the default is channel_domain setting
});
$$Rangers.config({
    mp_name: 'xyz Mini Program', //Some predefined properties can be set via config mp_version: '1.1.1',
});
$$Rangers.send();

App({
    onLaunch: function () {
        this.$$Rangers = $$Rangers;
    
        //If you want to set the user ID, such as using open_id to identify the user, you can set the value to user_unique_id after obtaining the open_id
        this.$$Rangers.config({
            user_unique_id: 'open_id that already acquired', //can be open_id, can also be union_id and other business sense can be used to identify the user uniqueness value
        });
        //Call the event method to report a specific event
        this.$$Rangers.event('test_event', {
            from: 'launch', //Supports arbitrary properties, values support numbers, strings, etc
        });
    }
});
 
Other pages report events, such as:
// pages/index/index.js
Page({
    onLoad() {
        getApp().$$Rangers.event('bind_view_tap', {
            'title': 'chart',
        });
    }
});
```


<span id="_3-用户与用户属性"></span>
# 3. Users and user attributes

<span id="_3-1-登录态变化调用"></span>
## 3.1 Login state change call

<span id="_3-1-1-账户登录"></span>
### 3.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

```javascript
$$Rangers.config({
    user_unique_id: '{{USER_UNIQUE_ID}}'
});
```


<span id="_3-2-设置用户属性"></span>
## 3.2 Setting user properties

<span id="_3-2-1-profileset"></span>
### 3.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```javascript
//Example: Set the user property, the property name is key, and the property value is value
$$Rangers.profileSet({
    key: 'value' //values support strings, numbers, arrays
});
```


<span id="_3-2-2-profilesetonce"></span>
### 3.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```javascript
//Example: Set a user property with the property name key_once and the property value value_once
$$Rangers.profileSetOnce({
    key_once: 'value_once' //values support strings, numbers, arrays
});
```


<span id="_3-2-3-profileincrement"></span>
### 3.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```javascript
//Example: Set the user property, the property name is key, and the property value is 1
$$Rangers.profileIncrement({
    key: 1
});
```


<span id="_3-2-4-profileappend"></span>
### 3.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```javascript
//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
$$Rangers.profileAppend({
    key: 'value_append'
});
```


<span id="_3-2-5-profileunset"></span>
### 3.2.5 profileUnset

Delete the user's attributes.

```javascript
//Example: Delete a user attribute named key
$$Rangers.profileUnset('key');
```


<span id="_4-获取实验参数"></span>
# 4. Obtain experimental parameters

1.0.9 version, SDK has added ab experiment capabilities, providing methods such as getVar and getAllVars, which are only valid when ab experiments are started, that is, enable_ab_test: true. "A/B testing" usually sends a shunt request to the shunt service after the SDK is initialized. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.


* Please note the precondition of this step: the experiment and related parameters have been created according to the demand side of the experiment.


<span id="_4-1-getvar"></span>
## 4.1 getVar

Gets the value corresponding to the variable in the ab experiment meta information. A variable name is bound to a vid. After successful acquisition, the corresponding vid will be set to the public properties reported by the sdk.

```javascript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; Bind to the global app for other pages to call.
    //experiment-key is the key of the experimental parameter, the user develops code branches, and the default-value is the bottom line when the network is abnormal. The suggestion is consistent with the control group value.
    this.$$Rangers.getVar('experiment-key', 'defaulte-value', function(value) {
        console.log(value);
    });
    //example
    this.$$Rangers.getVar('size', '1', function(value) {
        console.log(value);
    });
  }
});
```


When the getVar method is called, the exposure event (ab_exposure) is automatically reported, which is used to internally process the relevant statistics of the incoming users.

<span id="_4-2-getallvars"></span>
## 4.2 getAllVars

If you need to obtain the input information of all ab experiments, you can use the getAllVars method, but this method will not report the exposure event, so the system will not display data when calling this method, and only use the interface to obtain the input information.

```javascript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; Bind to the global app for other pages to call.
    this.$$Rangers.getAllVars(function(data) {
        The data format is as follows:
        // {
        //   "aa": {"vid": "1183", "val": true},
        //   "test_before_6d": {"vid": "2446", "val": "fail"}
        // }
    });
  }
});
```



|Parameter |Required |Description |Example |
|---|---|---|---|
|callback |Yes |(data: { [key: string]: { val: any,<br><br>vid: string } }) =\> void<br><br>Callback function for obtaining all experimental data. |{<br><br>"aa": {"vid": "1183", "val": true},<br><br>"test_before_6d": {"vid": "2446", "val": "fail"}<br><br>} |


<span id="_5-事件与事件属性（实验指标）"></span>
# 5. Events and event attributes (experimental metrics)

<span id="_5-1-上报代码埋点"></span>
## 5.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:

```javascript
//Example: Report an event that does not contain attributes
//placed in the corresponding position of business logic
app.$$Rangers.event('event');
```


Code event tracking for reporting events and corresponding properties, as follows:

```javascript
//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//. A property of type int, the property name key_int, the property value is 10
//placed in the corresponding position of business logic
app.$$Rangers.event('event', {
   key_string: 'value_string',
   key_int: 10
});
```


<span id="_5-2-事件公共属性"></span>
## 5.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="_5-2-1-设置公共属性"></span>
### 5.2.1 set public properties

```javascript
//Example: Set a custom public property with the property name key_public and the property value value_public
$$Rangers.config({
   key_public: 'value_public'
});
```


<span id="_6-api说明"></span>
# 6. API Description

<span id="_6-1-init"></span>
## **6.1 init**

Supported initialization parameters


| |Field |Field value |Field description |
|---|---|---|---|
|foundation |app_id |number |Unique identification of business products |
||log |boolean |After setting true, the console will print debug information |
||channel<br><br>Name: report_channel |Enumeration value:<br><br>cn、sg |The reporting channel corresponds to the built\-in reporting domain name and ab experimental domain name. Each application can only set one channel. Please set the appropriate channel according to the specific situation of the product.<br><br>Cn means domestic, sg means Singapore<br><br>The default value is cn.<br><br>Built\-in reporting domain name<br><br>cn：[https://mcs.volceapplog.com](https://mcs.volceapplog.com)<br><br>sg：[https://mcs.tobsnssdk.com](https://mcs.tobsnssdk.com)<br><br>Built\-in ab experimental domain name<br><br>cn：[https://abtest.volceapplog.com](https://abtest.volceapplog.com)<br><br>Sg: [https://toblog.tobsnssdk.com ](https://toblog.tobsnssdk.com)when the channel value is cn<br><br>Report the domain name as [https://mcs.volceapplog.com](https://mcs.volceapplog.com)<br><br>The domain name of ab experiment is [https://abtest.volceapplog.com](https://abtest.volceapplog.com) |
||channel_domain |string |You can customize the reporting domain name, which will override the channel settings, usually used in a privatized environment |
|automatic report |auto_report |boolean |Set true to automatically report predefined events such as app_launch, app_terminate, predefine_pageview, on_share |
|AB experiment |enable_ab_test |boolean |After setting true, the ab experiment function will be enabled, including using APIs such as getVar and getAllVars. |
||ab_channel_domain |string |You can customize the ab experimental domain name, which will override the channel settings, usually used in a privatized environment |
||clear_ab_cache_on_user_change |boolean |The default switch user retrieves the A/B configuration information, and sets the clear_ab_cache_on_user_change configuration item to false if you want to close it. |
|buffer<br><br>(Only supported 2.5.0 and above) |enable_buffer |boolean |After setting true, buffering will be turned on |
||buffer_interval |number |Buffer interval, in milliseconds, the default value is 5000, which means that all events in the buffer will be reported after the interval is reached |
||buffer_number |number |The maximum number of buffers, the default value is 5, meaning that all events in the buffer will be reported immediately after the number of buffers reaches this value |
|cache<br><br>(Only supported 2.5.0 and above) |enable_cache |boolean |After opening, the event of the failed request will be saved to the storage and reported when the user next enters the Mini Program |
|other |enable_profile |boolean |After setting true, you can use the profile related api. |
||enable_filter_crawler |boolean |After setting true, no more events will be reported in the crawler scene (scene: 1129) |
||enable_custom_webid |boolean |First, open enable_custom_webid when initializing, and then set web_id through config. Only after setting web_id will the initialization be completed. The value of web_id must be a number or a string type with all numbers.<br><br>$$Rangers.init({<br><br>enable_custom_webid: true,<br><br>});<br><br>$$Rangers.config({<br><br>web_id: '9876543210',<br><br>}); |


Example

```javascript
//Parameter: InitParams
//return value: void
$$Rangers.init({
    app_id: 1338,
    log: true,
    auto_report: true,
    enable_ab_test: true,
    clear_ab_cache_on_user_change: true,
    // ...
});
```


<span id="_6-2-config"></span>
## **6.2 config**

The config method can be called multiple times, and subsequent settings will overwrite the same property fields as before


| |Field |Type |Description |example |
|---|---|---|---|---|
|user |user_unique_id |string |Use the business's own user id to set user_unique_id |$$Rangers.config({<br><br>user_unique_id: 'zhangsan',<br><br>}); |
|custom |custom properties |string/number |When a property is a public property field, the property will have a clear location under the header<br><br>When the property is not a public property field, it will be placed under custrom in the header |$$Rangers.config({<br><br>City: 'Nanjing',<br><br>custom_name: 'vikings',<br><br>}); |


Example

```javascript
//Parameters: ConfigParams
//return value: void
$$Rangers.config({
    city: '南京', //Nanjing
    custom_name: 'vikings',
    // ...
});
```


<span id="_6-3-send"></span>
## **6.3 send**

After the initialization setting is completed, the send method must be called before the SDK is truly initialized, and no data will be reported before. example

```javascript
Parameters: None
//return value: void
$$Rangers.send();
```


<span id="_6-4-event"></span>
## **6.4 event**

Incident reporting. Event naming convention:


* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDKs to automatically report event names

* It is recommended that event names and attributes be lowercase

* Event property values accept only number and string types

* Do not nest objects in event properties, that is, the property value does not accept the object type

* If you want to express the meaning of event property value null, it is recommended to use "be_null", not "or"


Example

```javascript
//Parameters: name: string, params: object
//return value: void
$$Rangers.event('start_event', {
    start_time: 1630986183813,
    path: '...'
});
```


<span id="_6-5-sdk预设公共属性字段"></span>
## 6.5 SDK default public attribute fields

The SDK will assign values to some fields by default in `config ({})`, and these fields set by the SDK by default can be overridden.

Please note that the nickname, avatar, and geographical information of the "Share User" function in the growth analysis product need to be reported by you on your own initiative.


|**Field** |**Type** |**Description** |**Is it automatically set?**  |**Example** |
|---|---|---|---|---|
|platform |string |platform type |automatic collection |mp |
|device_brand |string |Equipment brand |automatic |"iPhone" |
|device_model |string |Equipment model |automatic |"iPhone 7" |
|os_name |string |Client side system |automatic |"ios" |
|os_version |string |Client side/OS version |automatic |"iOS 10.0.1" |
|screen_width |number |screen width |automatic |375 |
|screen_height |number |Screen height |automatic |812 |
|resolution |string |screen definition |automatic |"375x812" |
|access |string |network type |automatic |"wifi" |
|language |string |system language |automatic |"zh_CN" |
|device_id |number |Device ID |Business party settings |67834512 |
|app_name |string |app name |Business party settings |"xxx" |
|app_version |string |app version |Business party settings |"2.5.0" |
|region |string |region |Business party settings |"cn" |
|province |string |province |Business party settings |"Jiangsu." |
|city |string |city |Business party settings |"Nanjing." |
|nick_name |string |nickname |Business party settings |"Zhang San." |
|gender |string |Gender |Business party settings |"male" |
|avatar_url |string |avatar |Business party settings |"https://xxx" |
|timezone |number |Time Zone |Business party settings |8 |
|tz_offset |number |time zone offset |Business party settings |\-28800 |


<span id="_6-6-获取平台生成的各种id"></span>
## 6.6 Obtaining various IDs generated by the platform

Get the token information of the SDK, which contains web_id, ssid, user_unique_id information.

```typescript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; Bind to the global app for other pages to call.
    this.$$Rangers.getToken(function(token) { 
        //token data content for example:
        // {
        //    "web_id":"6748002161499735560",
        //    "ssid":"579bc89a-bd45-4021-8314-669c35f38e3d",
        //    "user_unique_id":"xxx",
        // }
    });
  }
});
```


<span id="_6-7-自定义webid"></span>
## 6.7 Custom webid

To change the SDK's default webid, first initialize with `enable_custom_webid: true`enabled, and then set web_id via config.

```javascript
$$Rangers.init({
    //Other initialization configurations
    enable_custom_webid: true, //Open enable_custom_webid at initialization
});
```


Once turned on, config web_id at other times.

```typescript
$$Rangers.config({
    web_id: '11111111111111', //The value of webid requires a pure number or a string type that is all numbers
});
```


It should be noted that when the custom webid is enabled, the webid must be actively set before the SDK can actually initialize and continue the subsequent process. This scenario is suitable for the H5 page to open in the WeChat Mini Program. You need to pass WeChat's unionID or openID to the H5 page.

<span id="_6-8-预置事件自动上报"></span>
## 6.8 Automatic reporting of preset events

Use preset event automatic reporting, you need to configure the `auto_report`parameter to true during initialization. It is recommended that you enable this event.

Note: The event name of a custom event should not be the same as the preset event.

Mini Program Preset Events Please refer to: [Mini Program Preset Events and Properties ](https://www.volcengine.com/docs/6285/108567).

<span id="_7-小程序第三方框架适配"></span>
# 7. Mini Program third\-party framework adaptation

For automatic event reporting (app_launch, app_terminate, etc.), the SDK is compatible with `taro`and `uni-app`third\-party frameworks. This compatibility requires that the SDK version is higher than 1.1.1.

<span id="_7-1-taro框架使用方式"></span>
## 7.1 How to use the taro framework


* Introducing the SDK via import in app.jsx

* Initialize the SDK before the App class


<span id="_7-2-uni-app框架使用方式"></span>
## 7.2 Usage of the uni\-app framework


* Introducing the SDK via import in main.js

* Initialize the SDK before the App class


<span id="_7-3-预置事件上报排查"></span>
## 7.3 Preset incident reporting for investigation

If you find that some automatic events have not been reported, you can check the following situations:


* The SDK version needs to be 1.1.1 +, and the initialization of the SDK should be placed at the front of the project entrance as much as possible;

* The third\-party framework requires a relatively new version, taro:, uni\-app: (other third\-party frameworks have not yet been specially compatible and may not support it);

* At the same time, other SDKs with similar functions are introduced. In this case, we try to initialize our SDK after other SDKs (but it still needs to be in front of the App class).


<span id="三、调试试验"></span>
# 8. Commissioning test

<span id="_1-为什么要调试实验"></span>
## **8.1. Why debug experiments?** 

Before the experiment is launched, it is necessary to ensure that the previous integration process is correct, and only after the experiment is launched can the scientific and effective results be guaranteed!

<span id="_2-开启调试状态"></span>
## **8.2. Turn on the debugging state**

Make the experiment in the "debugging" state, as shown in the following figure:


* The experimental status is divided into three categories: debugging, running, and completed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/681e7dd34bad4e0a88b381afeb2334f5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-通过接口获取调试设备的统计口径"></span>
## **8.3. Obtain the statistical caliber of the debugging equipment through the interface**

Open the log and A/B Test switches in the WeChat Mini Program SDK init and config respectively, and complete the initialization:


* Get the corresponding ssid through the getToken method in 6.6


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdbcb1b1abf34617ad45e74aadfc35e6~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-添加至白名单"></span>
## **8.4. Add to whitelist**

Add your test device ssid to the whitelist and click the "Save" button in the lower right corner.

<span id="_5-微信小程序参数调试"></span>
## **8.5. WeChat Mini Program parameter debugging**

After setting up the above steps, clear the cache and compile, and observe whether the ab data packet (that is, the experimental data returned by the abtest_config interface) obtains the configuration in Tester. The following figure shows the successful acquisition of experimental parameters:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5534d686298af26195b09c1667dd8de.png) </span>

If your WeChat Mini Program has not issued an experiment request, or the experiment request is empty, please follow the steps below to check:


* Is enable_ab_test: true correctly set during initialization?

* Whether the WeChat Mini Program adds "A/B Test Domain Name" and "Incident Report Domain Name" to the WeChat Developer Background/Development/Developer Settings/Server Domain Name "Request Legal Domain Name", please refer to Sections 1.2~ 1.4 for the specific domain name.


After triggering the experimental event, you can observe ab_sdk_version fields and content in the event packet header (the following figure is an example of ab_exposed event, other events, and so on):

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f1725d1d4d54f502bdc7d7dadc44529.png) </span>

<span id="_6-真机或模拟器实验场景调试"></span>
## **8.6. Real machine or emulator experimental scene debugging**

In the case of normal debugging of experimental parameters, development or QA/PM/operation, students need to observe whether the page where the experiment is located meets the expectations of the previous experimental design.

<span id="四、常见问题"></span>
# 9. Frequently Asked Questions

**9.1. When I need to create a client side experiment, but want to pay attention to the indicators related to server side events, how do I need to report server side events to view the experiment report normally?** 


* Get all the experimental IDs.


```javascript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; Bind to the global app for other pages to call.
    this.$$Rangers.getAllVars(function(data) {
        The data format is as follows:
        // {
        //   "aa": {"vid": "1183", "val": true},
        //   "test_before_6d": {"vid": "2446", "val": "fail"}
        // }
    });
});
```



* Pass to server side

* When calling the http interface to report the server side event, you need to bring the client side experiment information (ab_sdk_version) to the event. For the specific event reporting format, please refer to the [HTTP API (server side)](https://www.volcengine.com/docs/6285/65984).
