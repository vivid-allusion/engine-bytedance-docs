---
title: "React Native SDK Integration and Event Tracking"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/React_Native_SDK_Integration_and_Event_Tracking"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">React Native SDK integration documentation has been revised, please check the new documentation:<a href="https://docs.byteplus.com/docs/DataFinder/React_Native_SDK_Integration">React Native SDK Integration</a></div>


<span id="fceeaf6c"></span>
# 1. Integration, Growth Marketing Suite SDK

<span id="5f8d10a7"></span>
## 1.1 Integrated React Native plugins

```Shell
# Currently, the newest version is 0.2.11
npm i rangers_applog_reactnative_plugin
```


<span id="2c995896"></span>
## 1.2 Integrated iOS Native Dependencies

<span id="243fbc1d"></span>
### 1.2.1 Integration iOS SDK

If you use CocoaPods remote integration, please refer to [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)subsections 1.1~ 1.4;

If you need to manually introduce the integration, please refer to Section 1.5.

<span id="572d1c0a"></span>
### 1.2.2 Configuration Scheme (optional)

To use the [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)features, refer to [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)Section 3, Configuring Scheme.

<span id="44a06699"></span>
## 1.3 Integrated Android native dependencies

<span id="5b9ae21d"></span>
### 1.3.1 Integrate Android SDK

If you use remote integration, please refer to [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Sections 1.1\-1.6;

If you need to manually introduce the integration, please refer to Section 1.8.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">React Native integrate Android dependencies, you need to integrate the Lite version of the SDK package, that is, "Lite version: <code>com.bytedance.applog: RangersAppLog-Lite-cn</code>", so you can't use the full event tracking collection and circling function of the Android SDK for the time being.</div>


<span id="6e284c15"></span>
### 1.3.2 Configuration Scheme (optional)

To use the [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)features, refer to [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Section 3, Configuring Scheme.

<span id="f34aebba"></span>
# 2. Initialize the Growth Marketing Suite SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK will collect user information during initialization. Please ensure that you have obtained user authorization before collecting user information.</div>


The compliance recommendations are as follows:

After the user authorizes, the SDK is initialized. All information will not be collected before the user authorizes, and the preset events will not be collected.

<span id="e00ae8d4"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="40cf8416"></span>
## 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="2ba6e3b0"></span>
## 2.3 Initializing the SDK

<span id="e96a0833"></span>
### 2.3.1 SaaS version

React Native currently need to complete the initialization in the native code, initialize the Android SDK, iOS SDK respectively.

If you use the SaaS deployment version, please refer to the following code:


* Android: [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)2.3.1 section

* iOS: [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)2.3.1 section


<span id="e5f779a6"></span>
### 2.3.2 Privatization version

React Native currently need to complete the initialization in the native code, initialize the Android SDK, iOS SDK respectively.

If you use the private deployment version, please refer to the following code:


* Android: [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)2.3.2 section

* iOS: [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)2.3.2 section


<span id="f2de1dc3"></span>
### 2.3.3 SaaS cloud native version

React Native currently need to complete the initialization in the native code, initialize the Android SDK, iOS SDK respectively. If you use the SaaS cloud native deployment version, please refer to the following code:


* Android: [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)2.3.3 section

* iOS: [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)2.3.3 section


<span id="7ae77381"></span>
# 3. Users and user attributes

<span id="162b2971"></span>
## 3.1 Login state change call

<span id="a3461f96"></span>
### 3.1.1 Account login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Set the ID of your account system when logging in and ensure its uniqueness
RangersAppLogModule.setUserUniqueId('{{USER_UNIQUE_ID}}');
```


<span id="58fa6c42"></span>
### 3.1.2 Account Logout

Called when the account is logged out.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Set uuid to null when logging out
RangersAppLogModule.setUserUniqueId(null);
```


<span id="54e8e859"></span>
## 3.2 Setting user properties

<span id="6e2e6167"></span>
### 3.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, and the property value is value
RangersAppLogModule.profileSet({"key": "value"});
```


<span id="b6d130d3"></span>
### 3.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a user property with the property name key_once and the property value value_once
RangersAppLogModule.profileSetOnce({"key_once": "value_once"});
```


<span id="32fe8359"></span>
### 3.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, and the property value is 1
RangersAppLogModule.profileIncrement({"key": 1});
```


<span id="d419c57b"></span>
### 3.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
RangersAppLogModule.profileAppend({"key": "value_append"});
```


<span id="754a7c25"></span>
### 3.2.5 profileUnset

Delete the user's attributes.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Delete a user attribute named key
RangersAppLogModule.profileUnset("key");
```


<span id="52fe4267"></span>
# 4. Events and event properties

<span id="0f8123e4"></span>
## 4.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes.

Code event tracking that only reports events, as follows:

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Report an event that does not contain properties
RangersAppLogModule.onEventV3("event");
```


Code event tracking for reporting events and corresponding properties, as follows:

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//a property of type int, the property name key_int, the property value is 10
RangersAppLogModule.onEventV3("event", {
    "key_string": "value_string",
    "key_int": 10
});
```


<span id="0b204633"></span>
## 4.2 Event public attributes

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events.

<span id="3b79a4ca"></span>
### 4.2.1 set public properties

Please note about customizing "public properties":


1. The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute, so if you modify the custom public properties continuously within one minute, the last modification before the log sending shall prevail

2. It is not recommended to modify frequently, such as once per second


```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a custom public property with the property name key_public and the property value value_public
RangersAppLogModule.setHeaderInfo({
    "key_public": "value_public"
});
```


<span id="d798a70f"></span>
### 4.2.2 Remove Public Attributes

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a custom public property with the property name key_public and the property value value_public
RangersAppLogModule.removeHeaderInfo("key_public");
```


<span id="95a4d8ef"></span>
# 5. Other functions

<span id="0f65af1e"></span>
## 5.1 Obtaining the platform ID and notification

Please note that deviceid is a volcanic ID, not an original device ID.

```Dart
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Get did
let didPromise = RangersAppLogModule.getDeviceID();
didPromise.then((deviceID) => {
    console.log(deviceID);
});
```
