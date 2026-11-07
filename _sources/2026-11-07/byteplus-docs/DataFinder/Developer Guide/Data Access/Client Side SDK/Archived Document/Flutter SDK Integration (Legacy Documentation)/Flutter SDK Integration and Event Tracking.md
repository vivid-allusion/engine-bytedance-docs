---
title: "Flutter SDK Integration and Event Tracking"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Flutter_SDK_Integration_and_Event_Tracking"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Flutter SDK integration documentation has been revised, please check the new documentation: <a href="https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration">Flutter SDK Integration</a>.</div>


<span id="_1-集成-增长营销套件-sdk"></span>
# 1. Integration, Growth Marketing Suite SDK

<span id="_1-1-集成-flutter-插件"></span>
## 1.1 Integrated Flutter plugin

Add `rangers_applog_flutter_plugin`dependencies in `pubspec.yaml`for Flutter project

```yaml
dependencies:
  ......
  rangers_applog_flutter_plugin: 1.5.0
```


And install the plugin

```shell
flutter packages get
```


<span id="_1-2-集成-ios-原生端依赖"></span>
## 1.2 Integrated iOS Native Dependencies

<span id="_1-2-1-集成ios-sdk"></span>
### 1.2.1 Integration iOS SDK

If you use CocoaPods remote integration, please refer to [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)subsections 1.1~ 1.4;

If you need to manually introduce the integration, please refer to Section 1.5.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When introducing, you need to choose the code to import the SDK according to the environment you are currently using</div>


* <div data-tips="true" data-tips-type="warning">SaaS\-cloud\-native (including overseas Johor regions) and privatized environments do not need to configure the Host parameters.</div>



<span id="_1-2-2-配置scheme-可选"></span>
### 1.2.2 Configuration Scheme (optional)

To use the real\-time event tracking ([Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)) feature, refer to [(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)Section 3, Configuring Scheme.

<span id="_1-3-集成-android-原生端依赖"></span>
## 1.3 Integrated Android native dependencies

<span id="_1-3-1-集成android-sdk"></span>
### 1.3.1 Integrate Android SDK

If you use remote integration, please refer to [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Sections 1.1 to 1.5;

If you need to manually introduce the integration, please refer to Section 1.7.

<span id="_1-3-2-配置scheme-可选"></span>
### 1.3.2 Configuration Scheme (optional)

To use the real\-time event tracking ([Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)) feature, refer to [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)Section 3, Configuring Scheme.

<span id="6681b604"></span>
## 1.4 Integration, Hongmeng, native dependencies (version greater than 1.4.1)

Please move to the document: [Flutter SDK Harmony Access](https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Harmony_Access)

<span id="_2-初始化-增长营销套件sdk"></span>
# 2. Initialization, Growth Marketing Suite SDK

Explain

The SDK will collect user information during initialization. Please ensure that you have obtained user authorization before collecting user information.

The compliance recommendations are as follows:

After the user authorizes, the SDK is initialized. All information will not be collected before the user authorizes, and the preset events will not be collected.

<span id="_2-1-获取appid"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-获取数据上送地址"></span>
## 2.2 Obtain the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="cade7d82"></span>
### SaaS\-cloud\-native


|End type |SaaS\-cloud native environment<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|Flutter |* https://gator.uba.ap\-southeast\-1.bytepluses.com |`Host = null`, using the default data reporting address |


<span id="e9d06e2b"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk"></span>
## 2.3 Initializing the SDK

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because the Android flutter instance is initialized in MainActivity, the startup time is too late. If it is initialized on the dart side, there is a certain probability that app_launch event will be lost, and others will not be affected. If the lost app_launch cannot be accepted, it is recommended to initialize it on the native side (refer to the <a href="https://www.volcengine.com/docs/84129/1261741#_2-3-%E5%88%9D%E5%A7%8B%E5%8C%96-sdk">Android SDK integration document, initialization part </a>). After the native side is initialized, the dart side does not need to call the initialization interface and can be used normally.</div>


<span id="_2-3-1-saas版本"></span>
### 2.3.1 SaaS \- Cloud Native

If you use SaaS\-cloud native, please refer to the following code to initialize the SDK.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Initialize the SDK
String appId = '{{APPID}}'; //Refer to Section 2.1 to obtain
String channel = '{{CHANNEL}}'; //Fill in the app download/distribution channel, for example iOS is generally'App Store'
bool enableEncrypt = true; //encryption switch
bool enableDebugLog = false; //native log switch

//Set the data upload address
//Domestic - North China
String? host = 'https://gator.volces.com';
//Domestic - South China
// String? host = 'https://gator.uba.cn-guangzhou.volces.com';
//Overseas - Johor
// String? host = 'https://gator.uba.ap-southeast-1.bytepluses.com';

RangersApplogFlutterPlugin.addInitParams({
    'service_vendor': 'private', //fixed value private
});

RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
```


<span id="_2-3-2-私有化版本"></span>
### 2.3.2 Privatization version

If you use the private deployment version, please refer to the following code to initialize the SDK.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Initialize the SDK
String appId = '{{APPID}}'; //Refer to Section 2.1 to obtain
String channel = '{{CHANNEL}}'; //Fill in the app download/distribution channel, for example iOS is generally'App Store'
bool enableEncrypt = true; //encryption switch
bool enableDebugLog = false; //native log switch

//Set the private deployment data upload address, refer to Section 2.2 to obtain, {{REPORT_URL}} For example https://yourdomain.com, be careful not to add "/" after the domain name
String? host = '{{REPORT_URL}}';

RangersApplogFlutterPlugin.addInitParams({
    'service_vendor': 'private', //fixed value private
});

RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
```


<span id="ca7255eb"></span>
### 2.3.3 Non\-core initialization parameters (optional) (version \> = 1.4.1)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In general, the following scenarios require attention to this part:</div>



1. <div data-tips="true" data-tips-type="tip">If the SDK initialization method and start method need to be called separately due to some special reasons, you need to pay attention to the autoStart parameter</div>


2. <div data-tips="true" data-tips-type="tip">You need to customize some built\-in fields, and you need to pay attention to other parameters</div>



```TypeScript
//Currently supported regions/autoStart
Map<String, dynamic> initParams = {
  'region': 'cn',//Corresponding to the app_region field reported by the client side, for cases where custom app_region is required
  'autoStart': true,//false-initialization does not start, true-initialization is start, the default is true (for scenarios where init and start need to be separated)
};
RangersApplogFlutterPlugin.addInitParams(initParams);

RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
```


<span id="_3-用户与用户属性"></span>
# 3. Users and user attributes

<span id="_3-1-登录态变化调用"></span>
## 3.1 Login state change call

<span id="_3-1-1-账户登录"></span>
### 3.1.1 Account login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Set the ID of your account system when logging in and ensure its uniqueness
RangersApplogFlutterPlugin.setUserUniqueId('{{USER_UNIQUE_ID}}');
```


<span id="_3-1-2-账户登出"></span>
### 3.1.2 Account Logout

Called when the account is logged out.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Set uuid to null when logging out
RangersApplogFlutterPlugin.setUserUniqueId(null);
```


<span id="_3-2-设置用户属性"></span>
## 3.2 Setting user properties

<span id="_3-2-1-profileset"></span>
### 3.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set the user property, the property name is key, and the property value is value
RangersApplogFlutterPlugin.profileSet({"key": "value"});
```


<span id="_3-2-2-profilesetonce"></span>
### 3.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set a user property with the property name key_once and the property value value_once
RangersApplogFlutterPlugin.profileSetOnce({"key_once": "value_once"});
```


<span id="_3-2-3-profileincrement"></span>
### 3.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set the user property, the property name is key, and the property value is 1
RangersApplogFlutterPlugin.profileIncrement({"key": 1});
```


<span id="_3-2-4-profileappend"></span>
### 3.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
RangersApplogFlutterPlugin.profileAppend({"key": "value_append"});
```


<span id="_3-2-5-profileunset"></span>
### 3.2.5 profileUnset

Delete the user's attributes.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Delete user attribute named key
RangersApplogFlutterPlugin.profileUnset("key");
```


<span id="_4-事件与事件属性"></span>
# 4. Events and event properties

<span id="_4-1-上报代码埋点"></span>
## 4.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes.

Code event tracking that only reports events, as follows:

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Report an event that does not contain properties
RangersApplogFlutterPlugin.onEventV3("event");
```


Code event tracking for reporting events and corresponding properties, as follows:

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//a property of type int, the property name key_int, the property value is 10
RangersApplogFlutterPlugin.onEventV3("event", {
    "key_string": "value_string",
    "key_int": 10
});
```


<span id="_4-2-事件公共属性"></span>
## 4.2 Event public attributes

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events.

<span id="_4-2-1-设置公共属性"></span>
### 4.2.1 set public properties

Please note about customizing "public properties":


1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute, so if you modify the custom public properties continuously within one minute, the last modification before the log sending shall prevail. 2. High\-frequency modifications are not recommended, such as once per second


```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Set a custom public property, the property name is key_public, and the property value is value_public
RangersApplogFlutterPlugin.setHeaderInfo({
    "key_public": "value_public"
});
```


<span id="_4-2-2-移除公共属性"></span>
### 4.2.2 Remove Public Attributes

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Remove a public property named key_public
RangersApplogFlutterPlugin.removeHeaderInfo("key_public");
```


<span id="_5-其他功能"></span>
# 5. Other functions

<span id="_5-1-获取平台id与通知"></span>
## 5.1 Obtaining the platform ID and notification

Please note that deviceid is a volcanic ID, not an original device ID.

```dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Please start fetching after 3 seconds of initialization completion, otherwise it may return empty
String did = await RangersApplogFlutterPlugin.getDeviceId();
```


<span id="fc4358a3"></span>
# 6. Validation of event tracking

Flutter is a cross\-platform UI framework, event tracking verification only supports native event tracking verification.

Flutter\-side event tracking verification ideas can be found in the general event tracking verification document: [General Event Tracking Verification Operation Guide](https://docs.byteplus.com/docs/DataFinder/General_Event_Tracking_Verification_Operation_Guide).
