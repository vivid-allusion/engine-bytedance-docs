---
title: "WeChat Mini Program SDK Event Tracking and Properties"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/WeChat-Mini-Program-SDK-Event-Tracking-and-Properties"
---

<span id="a064dbb3"></span>
# 1. Users and user attributes

<span id="773079ea"></span>
## 1.1 Login state change call

<span id="5701e6e7"></span>
### 1.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

```javascript
$$Rangers.config({
    user_unique_id: '{{USER_UNIQUE_ID}}'
});
```


<span id="30761cf7"></span>
## 1.2 Setting user properties

<span id="142f0fd1"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```javascript
// Example: Set user properties, property name as key, property value as value
$$Rangers.profileSet({
    key: 'value' // Values support strings, numbers, and arrays
});
```


<span id="57f2caac"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```javascript
// Example: Set user properties, property name as key_once, property value as value_once
$$Rangers.profileSetOnce({
    key_once: 'value_once' // Values support strings, numbers, and arrays
});
```


<span id="5660db24"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```javascript
// Example: Set user properties, property name as key, property value as 1
$$Rangers.profileIncrement({
    key: 1
});
```


<span id="089e15e6"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```javascript
// Example: Set a user property with the property name 'key'. Originally, there was a property value, but now the property value has been added as' value_append'
$$Rangers.profileAppend({
    key: 'value_append'
});
```


<span id="aedac287"></span>
### 1.2.5 profileUnset

Delete the user's attributes.

```javascript
// Example: delete user property, with property name as key
$$Rangers.profileUnset('key');
```


<span id="3f790115"></span>
# 2. Obtain experimental parameters

1.0.9 version, SDK has added ab experiment capabilities, providing methods such as getVar and getAllVars, which are only valid when ab experiments are started, that is, enable_ab_test: true. "A/B testing" usually sends a shunt request to the shunt service after the SDK is initialized. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.


* Please note the precondition of this step: the experiment and related parameters have been created according to the demand side of the experiment, see [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment).


<span id="14709a81"></span>
## 2.1 getVar

Gets the value corresponding to the variable in the ab experiment meta information. A variable name is bound to a vid. After successful acquisition, the corresponding vid will be set to the public properties reported by the sdk.

```javascript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; // binding to global app, so that other pages can call it
    //experiment-key is the key of experimental parameters. User can develop a code branch. With default value as a fallback solution for network anomalies. It is recommended to match the value of the control group.
    this.$$Rangers.getVar('experiment-key', 'defaulte-value', function(value) {
        console.log(value);
    });
    //Example
    this.$$Rangers.getVar('size', '1', function(value) {
        console.log(value);
    });
  }
});
```


When the getVar method is called, the exposure event (ab_exposure) is automatically reported, which is used to internally process the relevant statistics of the incoming users.

<span id="8d503748"></span>
## 2.2 getAllVars

If you need to obtain the input information of all ab experiments, you can use the getAllVars method, but this method will not report the exposure event, so the system will not display data when calling this method, and only use the interface to obtain the input information.

```javascript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; // binding to global app, so that other pages can call it
    this.$$Rangers.getAllVars(function(data) {
        //data format as follows:
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


<span id="e2825c42"></span>
# 3. Events and event attributes (experimental metrics)

<span id="2ca4afe3"></span>
## 3.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:

```javascript
// Example: reporting event, this event does not include property
// Placed in the corresponding position of business logic
app.$$Rangers.event('event');
```


Code event tracking for reporting events and corresponding properties, as follows:

```javascript
// Example: reporting event, which includes two properties
//      a string type property, with property name key_string, and property value value_string
//      a int type property, with property name key_int, and property value 10
// Placed in the corresponding position of business logic
app.$$Rangers.event('event', {
   key_string: 'value_string',
   key_int: 10
});
```


<span id="00c12312"></span>
## 3.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="c3669296"></span>
### 3.2.1 Set public properties

```javascript
// Example: set custom public property with property name key_public and property value value_public
$$Rangers.config({
   key_public: 'value_public'
});
```


<span id="4c80169a"></span>
# 4. API Description

<span id="d7575f9c"></span>
## **4.1 init**

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
// Parameter: InitParams
// return value: void
$$Rangers.init({
    app_id: 1338,
    log: true,
    auto_report: true,
    enable_ab_test: true,
    clear_ab_cache_on_user_change: true,
    // ...
});
```


<span id="79477960"></span>
## **4.2 config**

The config method can be called multiple times, and subsequent settings will overwrite the same property fields as before


| |Field |Type |Description |Example |
|---|---|---|---|---|
|user |user_unique_id |string |Use the business's own user id to set user_unique_id |$$Rangers.config({<br><br>user_unique_id: 'zhangsan',<br><br>}); |
|custom |custom properties |string/number |When a property is a public property field, the property will have a clear location under the header<br><br>When the property is not a public property field, it will be placed under custrom in the header |$$Rangers.config({<br><br>City: 'Nanjing',<br><br>custom_name: 'vikings',<br><br>}); |


Example

```javascript
// Parameter: ConfigParams
// return value: void
$$Rangers.config({
    city: '南京', //Nanjing
    custom_name: 'vikings',
    // ...
});
```


<span id="5fa3cfe1"></span>
## **4.3 send**

After the initialization setting is completed, the send method must be called before the SDK is truly initialized, and no data will be reported before. example

```javascript
// Parameter: empty
// return value: void
$$Rangers.send();
```


<span id="24b21511"></span>
## **4.4 event**

Incident reporting. Event naming convention:


* Event naming only supports letters, numbers and underscores, do not use app_launch, app_terminate and other SDKs to automatically report event names

* It is recommended that event names and attributes be lowercase

* Event property values accept only number and string types

* Do not nest objects in event properties, that is, the property value does not accept the object type

* If you want to express the meaning of event property value null, it is recommended to use "be_null", not "or"


example

```javascript
// Parameter: name: string, params: object
// return value: void
$$Rangers.event('start_event', {
    start_time: 1630986183813,
    path: '...'
});
```


<span id="8d8827b6"></span>
## 4.5 SDK default public attribute fields

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


<span id="9d8a22ed"></span>
## 4.6 Obtaining various IDs generated by the platform

Get the token information of the SDK, which contains web_id, ssid, user_unique_id information.

```typescript
App({
  onLaunch: function () {
    this.$$Rangers = $$Rangers; // binding to global app, so that other pages can call it
    this.$$Rangers.getToken(function(token) { 
        //token data content as follows:
        // {
        //    "web_id":"6748002161499735560",
        //    "ssid":"579bc89a-bd45-4021-8314-669c35f38e3d",
        //    "user_unique_id":"xxx",
        // }
    });
  }
});
```


<span id="511530db"></span>
## 4.7 Obtaining the Experimental Version ID

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">AB test must call the API to obtain experimental parameters (see the <strong>++Getting Experimental Parameters ++</strong>section for details). You can use this API to obtain the Version IDs (vids) of all user exposures or hit experiments, which do not report abtest_exposure exposures.</div>


```JSON
$$Rangers.getAbSdkVersion();
```


<span id="6a3411c3"></span>
## 4.8 Custom webid

To change the SDK's default webid, first initialize with `enable_custom_webid: true` enabled, and then set web_id via config.

```javascript
$$Rangers.init({
    // other initialization configuration
    enable_custom_webid: true, // while initializing, enable enable_custom_webid
});
```


Once turned on, config web_id at other times.

```typescript
$$Rangers.config({
    web_id: '11111111111111', // The value of webid requires a string type of pure numbers or all numbers
});
```


It should be noted that when the custom webid is enabled, the webid must be actively set before the SDK can actually initialize and continue the subsequent process. This scenario is suitable for the H5 page to open in the WeChat Mini Program. You need to pass WeChat's unionID or openID to the H5 page.

<span id="3b8d13ab"></span>
## 4.9 Automatic reporting of preset events

Use preset event automatic reporting, you need to configure the `auto_report`parameter to true during initialization. It is recommended that you enable this event.

Note: The event name of a custom event should not be the same as the preset event.

Mini Program Preset Events Please refer to: [Mini Program Preset Events and Properties](https://docs.byteplus.com/docs/DataTester/Mini-Program-Preset-Events-and-Properties).

<span id="d3300323"></span>
# 5. Mini Program third\-party framework adaptation

For automatic event reporting (app_launch, app_terminate, etc.), the SDK is compatible with `taro`and `uni-app`third\-party frameworks. This compatibility requires that the SDK version is higher than 1.1.1.

<span id="3264f20c"></span>
## 5.1 How to use the taro framework


* Introducing the SDK via import in app.jsx

* Initialize the SDK before the App class


<span id="24b18ebd"></span>
## 5.2 Usage of the uni\-app framework


* Introducing the SDK via import in main.js

* Initialize the SDK before the App class


<span id="69bbb558"></span>
## 5.3 Preset incident reporting for investigation

If you find that some automatic events have not been reported, you can check the following situations:


* The SDK version needs to be 1.1.1 +, and the initialization of the SDK should be placed at the front of the project entrance as much as possible;

* The third\-party framework requires a relatively new version, taro:, uni\-app: (other third\-party frameworks have not yet been specially compatible and may not support it);

* At the same time, other SDKs with similar functions are introduced. In this case, we try to initialize our SDK after other SDKs (but it still needs to be in front of the App class).
