---
title: "Cordova SDK Integration and Event Tracking"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Cordova_SDK_Integration_and_Event_Tracking"
---

<span id="_1-集成-增长营销套件-sdk"></span>
# 1. Integration, Growth Marketing Suite SDK

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

If you use CocoaPods remote integration, please refer to [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)subsections 1.1~ 1.4;

If you need to manually introduce the integration, please refer to Section 1.5.

<span id="_1-3-2-配置scheme-可选"></span>
### 1.3.2 Configuration Scheme (optional)

To use the real\-time event tracking ([Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)) feature, refer to [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)Section 3, Configuring Scheme.

<span id="_1-4-集成-android-原生端依赖"></span>
## 1.4 Integrated Android native dependencies

<span id="_1-4-1-集成android-sdk"></span>
### 1.4.1 Integrate Android SDK

If you use remote integration, please refer to [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Sections 1.1 to 1.5;

If you need to manually introduce the integration, please refer to Section 1.7.

<span id="_1-4-2-配置scheme-可选"></span>
### 1.4.2 Configuration Scheme (optional)

To use the [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)features, refer to [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Section 3, Configuring Scheme.

<span id="_2-初始化-增长营销套件sdk"></span>
# 2. Initialization, Growth Marketing Suite SDK

explain

The SDK will collect user information during initialization. Please ensure that you have obtained user authorization before collecting user information.

The compliance recommendations are as follows:

After the user authorizes, the SDK is initialized. All information will not be collected before the user authorizes, and the preset events will not be collected.

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk"></span>
## 2.3 Initializing the SDK

<span id="_2-3-1-saas版本"></span>
### 2.3.1 SaaS version

Cordova currently needs to be initialized in the native code, initializing the Android SDK, iOS SDK respectively.

If you use the SaaS deployment version, please refer to the following code:


* Android: [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Section 2.3

* iOS: [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)Section 2.3


<span id="_2-3-2-私有化版本"></span>
### 2.3.2 Privatization version

Cordova currently needs to be initialized in the native code, initializing the Android SDK, iOS SDK respectively.

If you use the private deployment version, please refer to the following code:


* Android: [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Section 2.4

* iOS: [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)Section 2.4


<span id="_2-3-3-saas云原生版本"></span>
### 2.3.3 SaaS cloud native version

Cordova currently needs to be initialized in the native code, initializing the Android SDK, iOS SDK respectively.

If you use the SaaS cloud native deployment version, please refer to the following code:


* Android: [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Section 2.5

* iOS: [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)Section 2.5


<span id="_3-用户与用户属性"></span>
# 3. Users and user attributes

<span id="_3-1-登录态变化调用"></span>
## 3.1 Login state change call

<span id="_3-1-1-账户登录"></span>
### 3.1.1 account login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```dart
const AppLog = cordova.plugins.AppLog;

//Set the ID of your account system when logging in and ensure its uniqueness
AppLog.setUserUniqueId('{{USER_UNIQUE_ID}}',(v)=>{
    console.log("登录成功"); //login succeeded
},(err) =>{
    console.log(err.message);
});
```


<span id="_3-1-2-账户登出"></span>
### 3.1.2 account Logout

Called when the account is logged out.

```dart
const AppLog = cordova.plugins.AppLog;

//Set uuid to null when logging out
AppLog.setUserUniqueId(null,()=>{
    console.log("登出成功"); //log out succeeded
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
    console.log('设置用户属性成功'); // set user property succeeded
}, (err) => {
    console.log('设置用户属性失败：' + err.message); // set user property failed
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
    console.log('设置用户属性成功'); // set user property succeeded
}, (err) => {
    console.log('设置用户属性失败：' + err.message); // set user property failed
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
    console.log('设置用户属性成功'); // set user property succeeded
}, (err) => {
    console.log('设置用户属性失败：' + err.message); // set user property failed
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
    console.log('设置用户属性成功'); // set user property succeeded
}, (err) => {
    console.log('设置用户属性失败：' + err.message); // set user property failed
});
```


<span id="_3-2-5-profileunset"></span>
### 3.2.5 profileUnset

Delete the user's attributes.

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Delete a user attribute named key
AppLog.profileUnset("key", () => {
    console.log('设置用户属性成功'); // set user property succeeded
}, (err) => {
    console.log('设置用户属性失败：' + err.message); // set user property failed
});
```


<span id="_4-事件与事件属性"></span>
# 4. Events and event properties

<span id="_4-1-上报代码埋点"></span>
## 4.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes.

Code event tracking that only reports events, as follows:

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Report an event that does not contain properties
AppLog.onEventV3("event", {}, () => {
    console.log('调用上报埋点成功'); //Call report event tracking points succeeded
}, (err) => {
    console.log('调用上报埋点失败：' + err.message); //Call report event tracking points failed
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
    console.log('调用上报埋点成功'); //Call report event tracking points succeeded
}, (err) => {
    console.log('调用上报埋点失败：' + err.message); //Call report event tracking points failed
});
```


<span id="_4-2-设置公共属性"></span>
## 4.2 Setting Public Properties

Please note about customizing "public properties":


1. The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute, so if you modify the custom public properties continuously within one minute, the last modification before the log sending shall prevail

2. It is not recommended to modify frequently, such as once per second


```dart
const AppLog = cordova.plugins.AppLog;

//Example: Set a custom public property with the property name key_public and the property value value_public
AppLog.setHeaderInfo({
    "key_public": "value_public"
}, () => {
    console.log('设置公共属性成功'); //set public property succeeded
}, (err) => {
    console.log('设置公共属性失败：' + err.message); //set public property failed
});
```


<span id="_5-其他功能"></span>
# 5. Other functions

<span id="_5-1-获取平台id与通知"></span>
## 5.1 Obtaining the platform ID and notification

Please note that deviceid is a volcanic ID, not an original device ID. This feature is not currently supported by Android

```dart
const AppLog = cordova.plugins.AppLog;

//Example: Get did
AppLog.getDeviceID((did) => {
    console.log('获取did成功：' + did); //require did succeeded
}, (err) => {
    console.log('获取did失败：' + err.message); //require did failed
});
```
