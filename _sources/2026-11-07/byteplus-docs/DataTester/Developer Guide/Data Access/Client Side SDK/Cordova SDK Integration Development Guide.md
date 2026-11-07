---
title: "Cordova SDK Integration Development Guide"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Cordova-SDK-Integration-Development-Guide"
---

<span id="_1-集成sdk"></span>
# 1. Integrated SDK

<span id="_1-1-版本支持须知"></span>
## Version 1.1 Support Notes


* Cordova version support: 5.0.0 and above

* Minimum system version: Android 4.4\-10, iOS 8.0


<span id="_1-2-集成-cordova-插件"></span>
## 1.2 Integrated Cordova plugin

```shell
cordova plugin add cordova-plugin-rangersapplog
```


<span id="_1-3-集成-ios-原生端依赖"></span>
## 1.3 Integrated iOS Native Dependencies

<span id="_1-3-1-集成ios-sdk"></span>
### 1.3.1 Integration iOS SDK

If you use CocoaPods remote integration, please refer to [iOS SDK Integration ](https://docs.volcengine.com/docs/6285/65978?lang=en)1.1~ 1.4 subsections;

If you need to manually introduce the integration, please refer to Section 1.5.

<span id="_1-3-2-配置scheme-可选"></span>
### 1.3.2 Configuration Scheme (optional)

To use the [real-time event tracking](https://docs.volcengine.com/docs/6285/66054?lang=en) function, please refer to [iOS SDK Integration ](https://docs.volcengine.com/docs/6285/65978?lang=en)Section 3, Configuring Scheme.

<span id="_1-4-集成-android-原生端依赖"></span>
## 1.4 Integrated Android native dependencies

<span id="_1-4-1-集成android-sdk"></span>
### 1.4.1 Integrate Android SDK

If you use remote integration, please refer to [Android SDK Integration ](https://docs.volcengine.com/docs/6285/65980?lang=en)1.1~ 1.5 ;

If you need to manually introduce the integration, please refer to Section 1.7.

<span id="_1-4-2-配置scheme-可选"></span>
### 1.4.2 Configuration Scheme (optional)

To use the [real-time event tracking](https://docs.volcengine.com/docs/6285/66054?lang=en) function, please refer to Section 3, Configuring Scheme, [Android SDK Integration](https://docs.volcengine.com/docs/6285/65980?lang=en).

<span id="_2-初始化sdk"></span>
# 2. Initialize the SDK

Explain

The SDK will collect user information during initialization. Please ensure that you have obtained user authorization before collecting user information.

The compliance recommendations are as follows:

After the user authorizes, the SDK is initialized. All information will not be collected before the user authorizes, and the preset events will not be collected.

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk-saas版本"></span>
## 2.3 Initializing the SDK (SaaS version)

Cordova currently needs to be initialized in the native code, initializing the Android SDK, iOS SDK respectively.

If you use the SaaS deployment version, please refer to the following code:


* Android: [Android SDK Integration ](https://docs.volcengine.com/docs/6285/65980?lang=en)Section 2.3

* iOS [iOS SDK Integration ](https://docs.volcengine.com/docs/6285/65978?lang=en)Section 2.3


<span id="_2-4-初始化sdk-私有化版本"></span>
## 2.4 Initializing the SDK (privatized version)

Cordova currently needs to be initialized in the native code, initializing the Android SDK, iOS SDK respectively.

If you use the private deployment version, please refer to the following code:


* Android: [Android SDK Integration ](https://docs.volcengine.com/docs/6285/65980?lang=en)Section 2.4

* iOS [iOS SDK Integration ](https://docs.volcengine.com/docs/6285/65978?lang=en)Section 2.4


<span id="_3-用户与用户属性"></span>
# 3. Users and user attributes

<span id="_3-1-登录态变化调用"></span>
## 3.1 Login state change call

<span id="_3-1-1-账户登录"></span>
### 3.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

```dart
const AppLog = cordova.plugins.AppLog;

//Set the ID of your account system when logging in and ensure its uniqueness
AppLog.setUserUniqueId('{{USER_UNIQUE_ID}}',(v)=>{
    console.log("Successfully login");
},(err) =>{
    console.log(err.message);
});
```


<span id="_3-1-2-账户登出"></span>
### 3.1.2 Account Logout

Called when the account is logged out.

```dart
const AppLog = cordova.plugins.AppLog;

//Set uuid to null when logging out
AppLog.setUserUniqueId(null,()=>{
    console.log("Successfully logout");
},(err) =>{
    console.log(err.message);
});
```


<span id="_3-2-设置用户属性"></span>
## 3.2 Setting user properties

<span id="_3-2-1-profileset"></span>
### 3.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Set the user property, the property name is key, and the property value is value
AppLog.profileSet({
    "key": "value"
}, () => {
    console.log('Successfully set user property');
}, (err) => {
    console.log('failed to set user property：' + err.message);
});
```


<span id="_3-2-2-profilesetonce"></span>
### 3.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Set a user property with the property name key_once and the property value value_once
AppLog.profileSetOnce({
    "key_once": "value_once"
}, () => {
    console.log('Successfully set user properties');
}, (err) => {
    console.log('failed to set user property：' + err.message);
});
```


<span id="_3-2-3-profileincrement"></span>
### 3.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Set the user property, the property name is key, and the property value is 1
AppLog.profileIncrement({
    "key": 1
}, () => {
    console.log('Successfully set user properties');
}, (err) => {
    console.log('failed to set user property：' + err.message);
});
```


<span id="_3-2-4-profileappend"></span>
### 3.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
AppLog.profileAppend({
    "key": "value_append"
}, () => {
    console.log('Successfully set user properties');
}, (err) => {
    console.log('failed to set user property：' + err.message);
});
```


<span id="_3-2-5-profileunset"></span>
### 3.2.5 profileUnset

Delete the user's attributes.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Delete a user attribute named key
AppLog.profileUnset("key", () => {
    console.log('Successfully set user properties');
}, (err) => {
    console.log('failed to set user property：' + err.message);
});
```


<span id="_4-获取ab实验参数"></span>
# 4. Get AB test parameters

<span id="_4-1-获取ab实验值"></span>
## 4.1 Getting AB test Value

You can directly pass in the key to read the required value from the configuration (not supported by Anrdoid).

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Get the value with the key ab_test_key
AppLog.getABTestConfigValueForKey("ab_test_key", (value) => {
    console.log('Successfully acquired AB testing value：' + value);
}, (err) => {
    console.log('Failed to acquire AB testing value：' + err.message);
});
```


<span id="_4-2-获取所有ab实验版本"></span>
## 4.2 Get all AB test versions

The return value is all experimental Version IDs, separated by commas (not supported by Anrdoid).

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Get all abs sdk versions
AppLog.getAbSdkVersions((vids) => {
    console.log('Successfully acquired AbSdkVersions：' + vids);
}, (err) => {
    console.log('Failed to acquire AbSdkVersions：' + err.message);
});
```


<span id="_5-事件与事件属性"></span>
# 5. Events and event properties

<span id="_5-1-上报代码埋点"></span>
## 5.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes.

Code event tracking that only reports events, as follows:

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Report an event that does not contain attributes
AppLog.onEventV3("event", {}, () => {
    console.log('Successfully call reporting event tracking');
}, (err) => {
    console.log('Failed to call reporting event tracking：' + err.message);
});
```


Code event tracking for reporting events and corresponding properties, as follows:

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//a property of type int, the property name key_int, the property value is 10
AppLog.onEventV3("event", {
    "key_string": "value_string",
    "key_int": 10
}, () => {
    console.log('Successfully call reporting event tracking');
}, (err) => {
    console.log('Failed to call reporting event tracking：' + err.message);
});
```


<span id="_5-2-设置公共属性"></span>
## 5.2 Setting Public Properties

Please note about customizing "public properties":


1. The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log sending shall prevail.

2. It is not recommended to modify it frequently, such as once per second.


```dart
const AppLog = cordova.plugins.AppLog;

//Example: Set a custom public property with the property name key_public and the property value value_public
AppLog.setHeaderInfo({
    "key_public": "value_public"
}, () => {
    console.log('Successfully set public properties');
}, (err) => {
    console.log('Failed to set public properties：' + err.message);
});
```


<span id="_6-其他功能"></span>
# 6. Other functions

<span id="_6-1-获取平台id与通知"></span>
## 6.1 Obtaining the platform ID and notification

Please note that deviceid is a volcano\-generated ID, not the original device ID. This feature is not currently supported on Android.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Get did
AppLog.getDeviceID((did) => {
    console.log('Successfully acquired did：' + did);
}, (err) => {
    console.log('Failed to acquire did：' + err.message);
});
```
