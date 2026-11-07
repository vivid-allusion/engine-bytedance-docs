---
title: "React Native SDK Integration Development Guide"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/React-Native-SDK-Integration-Development-Guide"
---

<span id="_1-集成-sdk"></span>
# 1. Integrated SDK

<span id="_1-1-集成react-native插件"></span>
## 1.1 Integrated React Native plugins

```shell
npm i rangers_applog_reactnative_plugin
shell
```


<span id="_1-2-集成-ios-原生端依赖"></span>
## 1.2 Integrated iOS Native Dependencies

<span id="_1-2-1-集成ios-sdk"></span>
### 1.2.1 Integration iOS SDK

If you use CocoaPods remote integration, please refer to the [iOS SDK integration ](https://www.volcengine.com/docs/6285/65978)section 1.1~ 1.4; if you need to manually introduce the integration, please refer to the 1.5 section.

<span id="_1-2-2-配置scheme-可选"></span>
### 1.2.2 Configuration Scheme (optional)

To use the [real-time event tracking](https://docs.volcengine.com/docs/6285/66054?lang=en) feature, refer to Section 3, Configuring Scheme, [iOS SDK Integration ](https://www.volcengine.com/docs/6285/65978).

<span id="_1-3-集成-android-原生端依赖"></span>
## 1.3 Integrated Android native dependencies

<span id="_1-3-1-集成android-sdk"></span>
### 1.3.1 Integrate Android SDK

If you use remote integration, please refer to the [Android SDK Integration ](https://www.volcengine.com/docs/6285/65980)section 1.1 to 1.5; if you need to manually introduce the integration, please refer to the 1.7 section.

<span id="_1-3-2-配置scheme-可选"></span>
### 1.3.2 Configuration Scheme (optional)

To use [real-time event tracking](https://docs.volcengine.com/docs/6285/66054?lang=en), refer to Section 3, Configuring Scheme, [Android SDK Integration](https://www.volcengine.com/docs/6285/65980).

<span id="_2-初始化sdk"></span>
# 2. Initialize the SDK

The SDK will collect user information at initialization. Please ensure that you have obtained user authorization before collecting user information. The compliance recommended operation is as follows: After the user authorizes, the SDK is initialized. All information will not be collected before the user authorizes, and the preset events will not be collected.

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-4-初始化sdk-私有化版本"></span>
## 2.3 Initializing the SDK (privatized version)

React Native currently need to complete the initialization in the native code, initialize the Android SDK, iOS SDK respectively. If you use the private deployment version, please refer to the following code:


* Android: [Android SDK Integration ](https://www.volcengine.com/docs/6285/65980)Section 2.4

* iOS: [iOS SDK Integration ](https://www.volcengine.com/docs/6285/65978)Section 2.4


<span id="_3-用户与用户属性"></span>
# 3. Users and user attributes

<span id="_3-1-登录态变化调用"></span>
## 3.1 Login state change call

<span id="_3-1-1-账户登录"></span>
### 3.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Set the ID of your account system when logging in and ensure its uniqueness
RangersAppLogModule.setUserUniqueId('{{USER_UNIQUE_ID}}');
dart
```


<span id="_3-1-2-账户登出"></span>
### 3.1.2 Account Logout

Called when the account is logged out.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Set uuid to null when logging out
RangersAppLogModule.setUserUniqueId(null);
dart
```


<span id="_3-2-设置用户属性"></span>
## 3.2 Setting user properties

<span id="_3-2-1-profileset"></span>
### 3.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, and the property value is value
RangersAppLogModule.profileSet({"key": "value"});
dart
```


<span id="_3-2-2-profilesetonce"></span>
### 3.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a user property with the property name key_once and the property value value_once
RangersAppLogModule.profileSetOnce({"key_once": "value_once"});
dart
```


<span id="_3-2-3-profileincrement"></span>
### 3.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, and the property value is 1
RangersAppLogModule.profileIncrement({"key": 1});
dart
```


<span id="_3-2-4-profileappend"></span>
### 3.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
RangersAppLogModule.profileAppend({"key": "value_append"});
dart
```


<span id="_3-2-5-profileunset"></span>
### 3.2.5 profileUnset

Delete the user's attributes.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Delete a user attribute named key
RangersAppLogModule.profileUnset("key");
dart
```


<span id="_4-ab实验"></span>
# 4. AB testing

<span id="_4-1-获取ab实验值"></span>
## 4.1 Getting AB test Value

You can pass in the key directly to read the required value from the configuration.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Get the value with the key ab_test_key
let abValuePromise = RangersAppLogModule.getABTestConfigValueForKey("ab_test_key");
abValuePromise.then((abValue) => {
    console.log(abValue);
});
```


<span id="_4-2-获取ab实验版本"></span>
## 4.2 Acquiring AB test Version

The return value is the ID of all experimental versions, separated by commas.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Get all abs sdk versions
let vidsPromise = RangersAppLogModule.getAbSdkVersion();
vidsPromise.then((vids) => {
    console.log(vids);
});
```


<span id="_4-3-获取ab实验完整配置"></span>
## 4.3 Get AB test full configuration

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Get the full ab config
let configsPromise = RangersAppLogModule.getAllAbTestConfigs();
configsPromise.then((configs) => {
    console.log(configs);
});
```


<span id="_5-事件与事件属性（实验指标）"></span>
# 5. Events and event attributes (experimental metrics)

<span id="_5-1-上报代码埋点"></span>
## 5.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking that only reports events, as follows:

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Report an event that does not contain attributes
RangersAppLogModule.onEventV3("event");
dart
```


Code event tracking for reporting events and corresponding properties, as follows:

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//a property of type int, the property name key_int, the property value is 10
RangersAppLogModule.onEventV3("event", {
    "key_string": "value_string",
    "key_int": 10
});
dart
```


<span id="_5-2-事件公共属性"></span>
## 5.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events.

<span id="_5-2-1-设置公共属性"></span>
### 5.2.1 set public properties

Please note about customizing "public properties":


1. The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log sending shall prevail.

2. It is not recommended to modify it frequently, such as once per second.


```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a custom public property with the property name key_public and the property value value_public
RangersAppLogModule.setHeaderInfo({
    "key_public": "value_public"
});
dart
```


<span id="_5-2-2-移除公共属性"></span>
### 5.2.2 Remove Public Attributes

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a custom public property with the property name key_public and the property value value_public
RangersAppLogModule.removeHeaderInfo("key_public");
dart
```


<span id="_6-其他功能"></span>
# 6. Other functions

<span id="_6-1-获取平台id与通知"></span>
## 6.1 Obtaining the platform ID and notification

Please note that deviceid is a volcanic ID, not an original device ID.

```dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Get did
let didPromise = RangersAppLogModule.getDeviceID();
didPromise.then((deviceID) => {
    console.log(deviceID);
});
```
