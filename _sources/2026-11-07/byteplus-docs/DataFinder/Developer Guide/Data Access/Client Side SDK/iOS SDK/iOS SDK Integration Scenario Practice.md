---
title: "iOS SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/iOS_SDK_Integration_Scenario_Practice"
---

<span id="2a9ad500"></span>
# Manually import the SDK description

We recommend that you introduce the SDK through CocoaPods. If special circumstances require manual introduction, please refer to this section for manual introduction.


1. Please go to the [iOS SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main/iOS)to obtain the corresponding version of the SDK package.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">iOS offline package name is \* <code>version number</code>\* <code>.zip</code>format. For example: <code>6.17.0.zip</code>, where 6.17.0 is the SDK version number.</div>



2. Copy the files under the installation package to the project folder and add them to the project in XCode. Add dependencies:

* Libz.tbd, **required for offline integration**

* Libsqlite3.tbd, **required for offline integration**

* CoreGraphics.framework, **required dependencies for offline integration**

* Security.framework, **offline integration required dependencies**

* SystemConfiguration.framework, **required for offline integration**

* JavaScriptCore.framework, **offline integration required dependencies**

* WebKit.framework, **required dependencies for offline integration**

* CoreTelephony.framework, **offline integration required dependencies**

* AdSupport.framework, **optional dependency for offline integration, only required when introducing a Unique library, which is only required when purchasing Tracer as an additional attribution business**

* AppTrackingTransparency framework, **offline integration optional dependency, only when the introduction of Unique library, the library is only required when the purchase of Tracer for attribution business, and the dependency needs 14 + version to use, please do a good job when the introduction of dependencies configuration**


Build Settings \- \> Header Search Paths Add Headers folder path:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b276b14c3f320bc20485b05e62fae60.png) </span>

Build Settings \- \> Linking \- \> Other Linker Flags Add \-ObjC:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ae74616943fe217fb6c0dc04bb025c5.png) </span>

<span id="d79309ce"></span>
# Initialize related configuration

<span id="232a8578"></span>
## Full event tracking settings switch

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The full event tracking switch is on by default. After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.</div>



* <div data-tips="true" data-tips-type="warning">SaaS\-cloud native and privatization scenarios: Go to Project Center \> Project Management \> SDK Settings and make sure the full event tracking switch is turned on.</div>



`Objective-C`Please refer to:

```objectivec
//Open the upload of the full event tracking event
config.autoTrackEnabled = YES; //Full event tracking switch, YES on, NO off
```


`Swift`please refer to:

```Swift
//Open the upload of the full event tracking event
config.autoTrackEnabled = true //Full event tracking switch, true on, false off
```


<span id="049d0bfb"></span>
## Enable circling event tracking

Introducing the `Picker sublibrary`enables circling event tracking. Instead, removing the `Picker sublibrary`turns off the circled event tracking. Subspecs Add `Picker`

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'Picker'
    ]
```


<span id="605f16a9"></span>
## View log print

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Log printing is turned off by default, and it is recommended that the online production package be turned off.</div>


`Objective-C`Please refer to:

```objectivec
//Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
config.showDebugLog = NO; //YES: open log, NO: close log
```


`Swift`please refer to:

```Swift
//Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
config.showDebugLog = false //true: open log, false: close log
```


<span id="db939140"></span>
## Encryption setting switch

Encryption settings are enabled by default. You can turn off encryption during the debug phase to facilitate joint debugging.

`Objective-C`Please refer to:

```objectivec
//Encryption setting switch, it is recommended to turn on the online version.
config.logNeedEncrypt = YES; //YES: Encryption turned on, NO: Encryption turned off
```


`Swift`please refer to:

```Swift
//Encryption setting switch, it is recommended to turn on the online version.
config.logNeedEncrypt = true //true: open encryption, false: close encryption
```


<span id="b6d37428"></span>
### State Secret SM2

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">State secret SM2 algorithm request encryption <strong>only privatized version support</strong> , the minimum version supported: 6.15.0.</div>


Introduce the national secret SM2 sublibrary, subspecs add `Encryptor/SM2`

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'Encryptor/SM2' #Only privatized versions are supported
    ]
```


`Objective-C`Please refer to:

```objectivec
#import "BDAutoTrackEncryptorSM2.h"

//Set SM2 encryption
NSString * const publicKey = @"your public key";
[BDAutoTrackEncryptorSM2 setPublickKey:publicKey];
config.encryptionType = BDAutoTrackEncryptionTypeCstcSM2;
```


`Swift`please refer to:

```Swift
//Set SM2 encryption
let publicKey = "your public key"
BDAutoTrackEncryptorSM2.setPublickKey(publicKey)
config.encryptionType = .cstcSM2
```


<span id="64e89584"></span>
## Set APP Language and APP Region

`Objective-C`Please refer to:

```objectivec
//Modify language and region, set APP Language and APP Region
[BDAutoTrack setAppLauguage:@"zh/en/jp/fr"];
[BDAutoTrack setAppRegion:@"cn"];
```


`Swift`please refer to:

```Swift
//Modify language and region, set APP Language and APP Region
BDAutoTrack.setAppLauguage("zh/en/jp/fr")
BDAutoTrack.setAppRegion("cn")
```


<span id="7292320b"></span>
## Turn off device IDFA acquisition

The acquisition of the device IDFA is done through the `Unique`sublibrary. Introducing the `Unique`sublibrary opens the collection, removing the `Unique`sublibrary closes the collection.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SaaS\-cloud native and privatized 4.4.0 versions and above also support turning off sensitive field collection in the DataFinder console. You can turn off IDFA field collection in Project Management \> SDK Settings, see <a href="https://www.volcengine.com/docs/84129/1261714">Project Management\-SDK Settings </a>for details.</div>


```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        #'Unique', #Removing this Unique will turn off IDFA collection
    ]
```


<span id="83a6ea47"></span>
## Turn on screen orientation capture

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This section is supported after 6.11.0 +.</div>


Introducing the DeviceOrientation sublibrary. Subspecs Add `DeviceOrientation`

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'DeviceOrientation' Screen orientation capture
    ]
```


Screen orientation information is automatically brought into the `params`of each event tracking. The interface documentation is as follows:

```objectivec
/*! @abstract Whether to capture the screen direction, the default does not capture (NO) */
@property (nonatomic) BOOL screenOrientationEnabled;
```


`Objective-C`Please refer to:

```objectivec
config.screenOrientationEnabled = YES;
```


`Swift`please refer to:

```Swift
config.screenOrientationEnabled = true
```


<span id="2df73bf8"></span>
## Set GPS coordinates

Introducing the Location sublibrary. Subspecs Add `Location`

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'Location' #GPS acquisition
    ]
```


GPS information is automatically brought into each event tracking `params`:

```objectivec
/*! @abstract Whether to collect GPS, not by default (NO) */
@property (nonatomic) BOOL trackGPSLocationEnabled;
```


`Objective-C`Please refer to:

```objectivec
config.trackGPSLocationEnabled = YES;
```


`Swift`please refer to:

```Swift
config.trackGPSLocationEnabled = true
```


You can also manually set the GPS by yourself. After manual setting, the SDK will no longer use the automatically collected GPS information:

```objectivec
@interface BDAutoTrack
...
+ (void)setGPSLocation:(enum BDAutoTrackGeoCoordinateSystem)geoCoordinateSystem longitude:(double)longitude latitude:(double)latitude;
...
@end

//WGS84 Earth coordinate system
//GCJ02 Mars coordinate system
//BD09 Baidu coordinate system
//BDCS Beidou coordinate system
typedef NS_ENUM(NSInteger, BDAutoTrackGeoCoordinateSystem) {
    BDAutoTrackGeoCoordinateSystemWGS84 = 1 << 0,
    BDAutoTrackGeoCoordinateSystemGCJ02 = 1 << 1,
    BDAutoTrackGeoCoordinateSystemBD09  = 1 << 2,
    BDAutoTrackGeoCoordinateSystemBDCS  = 1 << 3
};
```


`Objective-C`Please refer to:

```objectivec
[BDAutoTrack setGPSLocation:BDAutoTrackGeoCoordinateSystemWGS84 longitude:116.3683244 latitude:39.915085];
```


`Swift`please refer to:

```Swift
BDAutoTrack.setGPSLocation(BDAutoTrackGeoCoordinateSystem.WGS84, longitude: 116.3683244, latitude: 39.915085)
```


<span id="05e6b833"></span>
## Activate crash capture

Introducing the Exception sublibrary. Subspecs Add `Exception`

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'Exception' #Collapse collection
    ]
```


`Objective-C`Please refer to:

```objectivec
//Currently only NSException crashes are supported
config.trackCrashEnabled = YES;
```


`Swift`please refer to:

```Swift
//Currently only NSException crashes are supported
config.trackCrashEnabled = true
```


<span id="130ebd04"></span>
## Turn off clipboard acquisition

Clipboard collects the ALink function used for advertising monitoring products. When this function module is turned on, the collection of clipboard information is turned on, and the collection of clipboard is disabled when it is turned off.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After turning off clipboard collection, the Alink attribution of ad monitoring may be affected. Please confirm whether the ad monitoring related functions are used before closing.</div>


* <div data-tips="true" data-tips-type="tip">iOS system from version 16, getting clipboard information will trigger a pop\-up window, so if you turn on the clipboard capture switch, when the ALink function collects the clipboard when the SDK is started, the pop\-up window will be triggered. It is recommended that you evaluate the timing of obtaining a clipboard based on the actual business situation.</div>



`Objective-C`Please refer to:

```objectivec
//Enable the DeferredALink function
//Turn off this function will not collect clipboard information
config.enableDeferredALink = NO;
```


`Swift`please refer to:

```Swift
//Enable the DeferredALink function
//Turn off this function will not collect clipboard information
config.enableDeferredALink = false;
```


<span id="c984e5ef"></span>
# Events and properties, event public properties

<span id="82a7bf0f"></span>
## report an incident

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:

`Objective-C`Please refer to:

```objectivec
//Example: Report an event that does not contain properties
//placed in the corresponding position of business logic
[BDAutoTrack eventV3:@"event" params:nil];
```


`Swift`please refer to:

```Swift
//Example: Report an event that does not contain properties
//placed in the corresponding position of business logic
BDAutoTrack.eventV3("event", params: nil)
```


Code event tracking for reporting events and corresponding properties, as follows:

`Objective-C`Please refer to:

```objectivec
//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//. A property of type int, the property name key_int, the property value is 10
//placed in the corresponding position of business logic
[BDAutoTrack eventV3:@"event" 
             params:@{@"key_string":@"value_string",
                      @"key_int": @(10)}];
```


`Swift`please refer to:

```Swift
//Example: Report an event, which contains two properties
//A property of type string, the property name is key_string, and the property value is value_string
//. A property of type int, the property name key_int, the property value is 10
//placed in the corresponding position of business logic
BDAutoTrack.eventV3("event", params: ["key_string": "value_string",
                                      "key_int": 10])
```


<span id="f6430819"></span>
## event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

Public property storage logic is non\-persistent, set as needed.

<span id="e1f7faa7"></span>
### Set public properties

`Objective-C`Please refer to:

```objectivec
/* * Example: Set a custom public property with the property name key_public and the property value value_public * Please note about customizing "public properties": * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail; * 2. High-frequency modifications are not recommended, such as once per second. */
[BDAutoTrack setCustomHeaderValue:@"value_public" forKey:@"key_public"];
```


`Swift`please refer to:

```Swift
/* * Example: Set a custom public property with the property name key_public and the property value value_public * Please note about customizing "public properties": * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail; * 2. High-frequency modifications are not recommended, such as once per second. */
BDAutoTrack.setCustomHeaderValue { () -> [String : Any] in
            return ["key_public":"value_public"]
}
```


<span id="faf87c35"></span>
### Remove public attributes

`Objective-C`Please refer to:

```objectivec
//Example: Remove a public property named key_public
[BDAutoTrack removeCustomHeaderValueForKey:@"key_public"];
```


`Swift`please refer to:

```Swift
//Example: Remove a public property named key_public
BDAutoTrack.removeCustomHeaderValueForKey("key_public");
```


<span id="ab3f43a1"></span>
## Default Public Property Field

The SDK collects the following information by default and as a public user attribute, it can be grouped and filtered in the growth analysis (DataFinder).


|Field name |Field type |Parameter name |
|---|---|---|
|os |string |Equipment system, the corresponding product attributes are os_name. |
|os_version |string |operating system version |
|app_version |string |App version |
|app_version_minor |string |Secondary version number, App four\-digit version number, set [OKApplicationInfo sharedInstance] .buildVersion = @"1.2.3.4"; |
|channel |string |Download channel (can be overwritten after setting), the corresponding product attribute is app_channel. |
|device_model |string |Equipment model |
|region |string |Operating system country |
|language |string |system language |
|sdk_version |string |SDK version |
|timezone |int |Time zone, such as 8 |
|tz_offset |int |Time zone offset, corresponding to an in\-product attribute of tz_offset, such as 28800. |
|tz_name |string |Time zone name, such as Asia/Shanghai. |
|carrier |string |operator |
|resolution |string |resolution |
|device_brand |string |Equipment brand |
|access |string | |


<span id="9a42dd8b"></span>
# user_unique_id and user attributes

<span id="9c02a701"></span>
## user login settings

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Versions after the 6.13.0 allow calls prior to gastTrack to set the initialized login state.</div>


<div data-tips="true" data-tips-type="warning">6.13.0 previous versions only took effect after the SDK was launched.</div>


<span id="fa0eaf3e"></span>
### user login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

`Objective-C`Please refer to:

```objectivec
#import <RangersAppLog/RangersAppLog.h>
//Set the ID of your account system and ensure its uniqueness
[BDAutoTrack setCurrentUserUniqueID:@"{{USER_UNIQUE_ID}}"];
```


`Swift`please refer to:

```Swift
BDAutoTrack.setCurrentUserUniqueID("{{USER_UNIQUE_ID}}")
```


<span id="df89e22c"></span>
### user logout

Called when the account is logged out.

`Objective-C`Please refer to:

```objectivec
[BDAutoTrack clearUserUniqueID];
```


`Swift`please refer to:

```Swift
BDAutoTrack.clearUserUniqueID()
```


<span id="d4d81dd9"></span>
## Set user properties

<span id="68c6bb44"></span>
### profileSet

Set user properties, override if they exist, and create if they don't.

`Objective-C`Please refer to:

```objectivec
//Example: Set the user property, the property name is key, and the property value is value
NSDictionary *profileDict = @{@"key": @("value")};
[BDAutoTrack profileSet:profileDict];
```


`Swift`please refer to:

```Swift
//Example: Set the user property, the property name is key, and the property value is value
let profileDict: [AnyHashable: Any] = [
    "key": "value"
]
BDAutoTrack.profileSet(profileDict)
```


<span id="5033d8b5"></span>
### profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

`Objective-C`Please refer to:

```objectivec
//Example: Set a user property with the property name key_once and the property value value_once
NSDictionary *profileDict = @{@"key_once": @("value_once")};
[BDAutoTrack profileSetOnce:profileDict];
```


`Swift`please refer to:

```Swift
//Example: Set a user property with the property name key_once and the property value value_once
let profileDict: [AnyHashable: Any] = [
    "key_once": "value_once"
]
BDAutoTrack.profileSetOnce(profileDict)
```


<span id="171ab082"></span>
### profileIncrement

Set the properties of the numeric type to accumulate.

`Objective-C`Please refer to:

```objectivec
//Example: Set the user property, the property name is key, and the property value is 1
[BDAutoTrack profileIncrement:@{@"key": @(1)}];
```


`Swift`please refer to:

```Swift
//Example: Set the user property, the property name is key, and the property value is 1
let profileDict: [AnyHashable: Number] = [
    "key": 1
]
BDAutoTrack.profileIncrement(profileDict)
```


<span id="4279eefb"></span>
### profileAppend

Set the user properties of the List type to be continuously added to the List.

`Objective-C`Please refer to:

```objectivec
//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
[BDAutoTrack profileAppend:@{
    @"key": @[@"value_append"]
}];
```


`Swift`please refer to:

```Swift
//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
BDAutoTrack.profileAppend([["key"]:["value_append"]])
```


<span id="62632b09"></span>
### profileUnset

Delete the user's attributes.

`Objective-C`Please refer to:

```objectivec
//Example: Delete a user attribute named key
[BDAutoTrack profileUnset:@"key"];
```


`Swift`please refer to:

```Swift
//Example: Delete a user attribute named key
BDAutoTrack.profileUnset("key")
```


<span id="98068314"></span>
# Get platform ID and notifications

<span id="8565a50f"></span>
## Get the platform generation ID

`Objective-C`Please refer to:

```objectivec
#import <RangersApplog/BDAutoTrackNotifications.h>
//Set listening before initializing the SDK
 [[NSNotificationCenter defaultCenter] addObserver:self
                                            selector:@selector(onRegisterSuccess:)
                                                name:BDAutoTrackNotificationRegisterSuccess object:nil];
//SDK initialization code part
//Then set the callback after SDK initialization
- (void)onRegisterSuccess:(NSNotification *)noti  {
    NSString *dids = [noti.userInfo objectForKey:kBDAutoTrackNotificationRangersDeviceID];
    NSString *ssids = [noti.userInfo objectForKey:kBDAutoTrackNotificationSSID]; 
    NSLog(@"onRegisterSuccess.dids：%@", dids); //get device bddid
    NSLog(@"onRegisterSuccess.ssids：%@", ssids); //Get SSID
}
```


`Swift`please refer to:

```Swift
NotificationCenter.default.addObserver(self, selector: #selector(onRegisterSuccess), name: NSNotification.Name(rawValue: BDAutoTrackNotificationRegisterSuccess), object: nil)

func onRegisterSuccess(noti: Notification) {
    let did = noti.userInfo[kBDAutoTrackNotificationRangersDeviceID]
    let ssid = noti.userInfo[kBDAutoTrackNotificationSSID]
    print("onRegisterSuccess.dids：\(did)")
    print("onRegisterSuccess.ssids：\(ssid)")
}
```


<span id="4fea37b9"></span>
## Get the SDK version number

`Objective-C`Please refer to:

```objectivec
//The SDK version number format is X.X.X
[BDAutoTrack SDKVersion];
```


`Swift`please refer to:

```Swift
BDAutoTrack.sdkVersion()
```


<span id="d93fd8a9"></span>
## Get various notifications

The SDK provides methods for obtaining various notifications. Each notification is described in the `BDAutoTrackNotifications h`header file.

```objectivec
//SDK registration success notification
BDAutoTrackNotificationRegisterSuccess
//SDK registration request failure notification
BDAutoTrackNotificationRegisterFailure
//Activation success notification
BDAutoTrackNotificationActiveSuccess
//SDK ABTest configuration pull success notification
BDAutoTrackNotificationABTestSuccess
//Notification when the SDK ABTestVid changes
BDAutoTrackNotificationABTestVidsChanged
```


<span id="c0f7654e"></span>
# H5 through the introduction

<span id="ada30984"></span>
## Open the embedded H5 page

After opening the embedded H5 page, the events generated on the embedded H5 page will be reported through the iOS SDK, not the js SDK, and the `user_unique_id`and public attributes set by the iOS side will be reused, but the uuid on the web side setting/update side when opening is also supported (if you need to support the update of multi\-caliber from the web side, you need to use the new version of the SDK)/public attributes.

Please note that the open function also needs to integrate the js SDK on the H5 page, and turn on the open switch of js, please refer to Section 3.4 of [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration). After getting through, the H5 full event tracking function is blocked by default. If you still want to collect H5 full event tracking, you need to check Section 4.7: Native collection of H5 full event tracking.

`Objective-C`Please refer to:

```objectivec
//Turn on the embedded H5 open switch
config.enableH5Bridge = YES;
```


`Swift`please refer to:

```Swift
//Turn on the embedded H5 open switch
config.enableH5Bridge = true;
```


After the switch is turned on, the whitelist must be configured. Only the domain names configured in the whitelist take effect. The whitelist can be added by wild\-card, and `*`means wild\-card.

`Objective-C`Please refer to:

```objectivec
//Embedded H5 page whitelist configuration
//Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
config.H5BridgeAllowedDomainPatterns = @[@"www.volcengine.com",@"*.bytedance.*"];

//There are many whitelists for adaptation www.bytedance.com, please configure the whitelist according to the business scenario, for example:
//www.bytedance.com or * .bytedance. * or *.*.* .
```


`Swift`please refer to:

```Swift
//Embedded H5 page whitelist configuration
//Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
config.h5BridgeAllowedDomainPatterns = ["www.volcengine.com", "*.bytedance.*"]
```


When getting through, the in\-terminal SDK user information is used by default, but it also supports the H5 side to update the in\-terminal SDK user information through the Web SDK.

iOS 6.17.2 version of the new ban to get through the embedded H5 page prohibits H5 update App user information, in order to avoid H5 multi\-use update user information code is not easy to remove, thereby destroying the original user information in the end of the SDK when getting through.

```objectivec
//On by default, support off
config.useBridgeUpdateUUIDEnabled = YES;
```


<span id="f30a6dde"></span>
## Native capture H5 full event tracking

When the webview page is embedded in the native side, by turning on the following switch, the h5 page full event tracking event can be collected from the native side full event tracking event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The use of this switch does not require integration of the JavaScript SDK within the h5 page and is independent of the JavaScript SDK full event tracking feature.</div>


`Objective-C`Please refer to:

```objectivec
//Embedded H5 page full event tracking event
config.H5AutoTrackEnabled = YES; //YES: Turn on h5 full event tracking event, NO: Turn off h5 full event tracking event
```


`Swift`please refer to:

```Swift
//Embedded H5 page full event tracking event
config.H5AutoTrackEnabled = true; //true: turn on h5 full event tracking event, false: turn off h5 full event tracking event
```


<span id="2ad2b8d3"></span>
# multi\-instance correlation

<span id="67b2c0c3"></span>
## multi\-instance initialization

Multi\-instance initialization means that the SDK supports event tracking to multiple applications (multiple appids) in apps with the same package name, and the event tracking data is isolated from each other, and each appid corresponds to a separate instance. Usage scenarios such as:


* When the third\-party SDK relies on the **Growth Marketing Suite SDK** to do event tracking generated internally in the SDK;

* When you associate multiple event tracking apps (multiple appids) in the same app or system and share the **Growth Marketing Suite SDK**.


`Objective-C`Please refer to:

```objectivec
BDAutoTrackConfig* config1 = [BDAutoTrackConfig configWithAppID:@"{{APPID_1}}" launchOptions:launchOptions];
BDAutoTrack *track1 = [BDAutoTrack trackWithConfig:config1];
[track1 startTrack];

BDAutoTrackConfig* config2 = [BDAutoTrackConfig configWithAppID:@"{{APPID_2}}" launchOptions:launchOptions];
BDAutoTrack *track2 = [BDAutoTrack trackWithConfig:config2];
[track2 startTrack];
```


`Swift`please refer to:

```Swift
let config1 = BDAutoTrackConfig.init(appID: "{{APPID_1}}", launchOptions: launchOptions)
let tracker1 = BDAutoTrack.init(config: config1);
tracker1!.start()

let config2 = BDAutoTrackConfig.init(appID: "{{APPID_2}}", launchOptions: launchOptions)
let tracker2 = BDAutoTrack.init(config: config2);
tracker2!.start()
```


<span id="5c3795fe"></span>
# Full event tracking scenario

After turning on the full event tracking event collection switch, page events and View click events will be collected by default.

**application scenario**


|Typical scene |Scene description |
|---|---|
|user behavior analysis |Understand the user's behavior path in the application, such as which buttons the user clicks, which pages the user browses, and how long the user spends on a particular page. |
|A/B Testing |Help evaluate the impact of different versions of a feature or interface on user behavior. For example, compare the click through rate of two different interface layouts and test the impact of different functional implementations on user usage. |
|problem diagnosis |It helps to quickly identify and locate problems in the application. For example, users frequently log out or crash on a certain page, and the usage of certain features suddenly decreases. |
|Operational activity effect evaluation |Help evaluate the effectiveness of various operational activities, such as promotions, push notifications, and more. For example: click through rate and conversion rate of a push notification, engagement and effectiveness of a promotion. |


**Full event tracking capability support**


|Capability support |Capability description |
|---|---|
|page visit |* UIViewController Life Cycle<br><br>* UITabBarController toggle<br><br>* UIPageViewController switch<br><br>* UINavigationController switch |
|click |* sendAction events triggered by UIButton, etc<br><br>* UIAlertAction click event<br><br>* UITableViewCell, UICollectionView click event<br><br>* UIGestureRecognizer Click, Long Press |
|exposure |UIView and Subclass Exposure |


**Full event tracking preset event list and reporting mechanism**


|Full event tracking event list |Event description |Event triggering mechanism |
|---|---|---|
|bav2b_page |page view event | |
|$bav2b_page_leave |page leave | |
|bav2b_click |element click event | |
|bav2b_beat |page heartbeat event | |
|$bav2b_slide |Slide event | |


See below for a detailed description of each preset event and the associated event properties.

<span id="155b98d8"></span>
## function on

<span id="715ed6d7"></span>
### Full event tracking switch

You can introduce the corresponding subspec module or static library file into the project to turn on the full event tracking switch depending on the integration method.

`Objective-C`Please refer to:

```objectivec
//Enable full event tracking, the default is YES
config.autoTrackEnabled = YES;
//Enable WebView full event tracking, the default is YES
config.H5AutoTrackEnabled = YES;
```


`Swift`please refer to:

```Swift
config.autoTrackEnabled = true
config.H5AutoTrackEnabled = true
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">trackEventEnabled is the event reporting master switch, the default is YES.</div>


* <div data-tips="true" data-tips-type="tip">Priority: trackEventEnabled \> autoTrackEnabled \> H5AutoTrackEnabled</div>



<span id="bbe4fd74"></span>
### Preset event list and reporting logic


|Full event tracking event list |Event description |Event triggering mechanism |
|---|---|---|
|bav2b_page |page visit |Trigger the report after the page is opened |
|$bav2b_page_leave |page leave |Trigger a report after leaving the page |
|bav2b_click |View element click event |Trigger a report after clicking on a page element |


Of which:


* bav2b_page: Contains source page related attributes (refer_page_xx), when the application is cold start, such attribute values will be empty, and the page will be filled with source page information in the new page after the page jump.

* $bav2b_page_leave: Record a duration event with when the page is entered as the key, and record the current entry time. Extract the duration event when the page exits, subtract the page entry time from the current time, and the median difference is the length of the dwell time.


For a more detailed description of each preset event and related event properties, see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties).

<span id="96711d3b"></span>
### Event\-based function switch

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This section is supported in version 6.11.0 +.</div>


<div data-tips="true" data-tips-type="warning">Allows full event tracking event type configuration, as defined in <code>< BDCommonEnumDefine.h ></code>.</div>



* BDAutoTrackDataTypePage \- Page View Events

* BDAutoTrackDataTypeClick \- user click event

* BDAutoTrackDataTypePageLeave \- End of Page View Event


`Objective-C`Please refer to:

```objectivec
config.autoTrackEventType = BDAutoTrackDataTypeAll;
```


`Swift`please refer to:

```Swift
config.autoTrackEventType = BDAutoTrackDataType.all
```


<span id="2fadcd78"></span>
### DataFinder console on

After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.


* SaaS\-cloud native and privatization scenarios: Go to Project Center \> Project Management \> SDK Settings and make sure the full event tracking switch is turned on.


<span id="c6b755fe"></span>
## Custom page view event properties

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please set the parameter value in the init method, otherwise the parameter value may be empty when the page view event is first triggered.</div>


<div data-tips="true" data-tips-type="warning">Customize the parameters of the page view event through the <code>UIViewController</code>extension API.</div>


```objectivec
/*! @abstract Manually set PageTitle
 @discussion If set, it will be collected when the page is switched.
 @discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackPageTitle;
 /*! @abstract Manually set PageID
 @discussion If set, it will be collected when the page is switched.
 @discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackPageID;
 /*! @abstract Manually set PagePath
 @discussion If set, it will be collected when the page is switched.
 @discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackPagePath;
 /*! @abstract Manually set extra information
 @discussion If set, it will be collected when the page is switched.
 @discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSString *> *bdAutoTrackExtraInfos;
 /*! @abstract Custom collection properties, the same key will override the default collection params
 @discussion If set, it will be collected when the page is switched.
 @discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSObject *> *bdAutoTrackPageProperties;
```


<span id="10ee2e7c"></span>
## custom click event properties

Customize the parameters of the click event through `UIView`and `UIBarButtonItem`extension APIs.

```objectivec
/*! @abstract This corresponds to the newly added element_id field, and bdAutoTrackViewID corresponds to the element_manual_key field
 @discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackElementID;
 
/*! @abstract Manually set ViewID
 @discussion If set, it will be collected when clicked, which can uniquely mark the View. */
@property (nonatomic, copy) NSString *bdAutoTrackViewID;
 
/*! @abstract Manually set ViewContent
 @discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackViewContent;
 
/*! @abstract Manually set extra information
 @discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSString *> *bdAutoTrackExtraInfos;
 
/*! @abstract Custom collection properties, the same key will override the default collection params
 @discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSObject *> *bdAutoTrackViewProperties;
 
/*! @abstract custom collection development
 @discussion If you set YES, event tracking will be ignored when clicked */
@property (nonatomic, assign) BOOL bdAutoTrackIgnoreClick;
```


<span id="4c13ac53"></span>
## Ignore specific full event tracking events

<span id="b3ee65b1"></span>
### Ignore specific page view events

```objectivec
/*! @abstract Ignore the automatically collected browsing event tracking in UIViewController
    @discussion ignores that the scope is its own class, which does not affect the inheritance relationship. For example, BViewController inherits from AViewController. If both are ignored, you need to pass in @[[AViewController class], [BViewController class]]
    @Param controllerClasses pass in the class name to be ignored @[[TestViewController class], [UserViewController class]] */
- (void)ignoreAutoTrackPage:(NSArray<Class> *)controllerClasses;
```


`Objective-C`Please refer to:

```objectivec
[[BDAutoTrack sharedTrack] ignoreAutoTrackPage:@[YOUR_ViewController.class]];
```


`Swift`please refer to:

```Swift
BDAutoTrack.shared().ignorePage([YOUR_ViewController.classForCoder()])
```


<span id="db9768c8"></span>
### Ignore specific control click events

```objectivec
/*! @abstract Ignore auto-collected click event tracking in controls
    @discussion ignore scope to own class
    @Param viewClasses pass in the class name to be ignored @[[AButton class], [ALabel class]] */
- (void)ignoreAutoTrackClick:(NSArray<Class> *)viewClasses;
```


`Objective-C`Please refer to:

```objectivec
[[BDAutoTrack sharedTrack] ignoreAutoTrackClick:@[YOUR_VIEW.class]];
```


`Swift`please refer to:

```Swift
BDAutoTrack.shared().ignoreClick([YOUR_VIEW.classForCoder()])
```


<span id="826d8a04"></span>
## Manually trigger full event tracking

<span id="c5297f86"></span>
### Manually trigger page view events

```objectivec
/*! * @abstract code triggers page view event tracking report
* @param controller can pass UIViewController and objects that implement the BDAutoTrackable protocol
* @result wherther success
 */
- (BOOL)trackPage:(id<BDAutoTrackable>)controller;

/*! * @abstract code triggers page view event tracking report
* @param controller can pass UIViewController
* @param params user-defined parameters for [NSJSONSerialization isValidJSONObject:] validation
* @result wherther success
*/
- (BOOL)trackPage:(id)controller withParameters:(nullable NSDictionary<NSString *,id> *)params;
```


`Objective-C`Please refer to:

```objectivec
[[BDAutoTrack sharedTrack] trackPage:YOUR_VIEWCONTROLLER_INSTANCE];
```


`Swift`please refer to:

```Swift
BDAutoTrack.shared().trackPage(YOUR_VIEWCONTROLLER_INSTANCE)
```


<span id="7bf099b8"></span>
### Manually trigger click events

```objectivec
/*! * @abstract code trigger click event tracking report
* @Param view can pass control objects such as UIView, as well as objects that implement the BDAutoTrackable protocol
* @result wherther success
 */
- (BOOL)trackClick:(id<BDAutoTrackable>)view;
 
/*! * @abstract code trigger click event tracking report
* @Param view can pass control objects such as UIView, as well as objects that implement the BDAutoTrackable protocol
* @param params user-defined parameters for [NSJSONSerialization isValidJSONObject:] validation
* @result wherther success
 */
- (BOOL)trackClick:(id<BDAutoTrackable>)view withParameters:(nullable NSDictionary<NSString *,id> *)params;
```


`Objective-C`Please refer to:

```objectivec
[[BDAutoTrack sharedTrack] trackClick:YOUR_COMPONENT];
```


`Swift`please refer to:

```Swift
BDAutoTrack.shared().trackClick(YOUR_COMPONENT)
```


<span id="8b5c2a70"></span>
# acquisition duration event

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This section is supported after 6.10.2 +.</div>


<div data-tips="true" data-tips-type="warning">Events with time attributes can use the duration event capture interface, such as capturing video playback duration events.</div>


```objectivec
//Called when the video starts playing
[[BDAutoTrack sharedTrack] startDurationEvent:@"play"];
 
//Called when the video is paused
[[BDAutoTrack sharedTrack] pauseDurationEvent:@"play"];
 
 //Called when the video continues to play
[[BDAutoTrack sharedTrack] resumeDurationEvent:@"play"];
 
//Called at the end of playback, a play event will be reported at this time, with a $event_duration attribute (the playback time is recorded, in milliseconds)
[[BDAutoTrack sharedTrack] stopDurationEvent:@"play" properties:@{@"moive_name":@"xxx"}];
```


<span id="2d06e283"></span>
# Other scenarios

<span id="f71b8160"></span>
## Cloud control capability

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This function is only available in SaaS cloud native version or privatized version V4.4.0 or above, and is supported by SDK6.15.0 or above.</div>


DataFinder supports sending SDK settings through the server level, including reporting timing, full event tracking switch, etc. For detailed documentation, please refer to: [Project Management - SDK Settings](https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings).

<span id="c9d03e59"></span>
## Real\-time event tracking and circling

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification) or [Circle Event](https://docs.byteplus.com/docs/DataFinder/Circle_Event), please import the `Log`sublibrary and add the `Log`subspecs.

Note that in addition to introducing sublibraries, you will need to complete the following steps to `configure Scheme`.

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'Log' #Real-time event tracking, circling events
    ]
```


<span id="e1985aa2"></span>
## Configuration Scheme

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification) or [Circle Event](https://docs.byteplus.com/docs/DataFinder/Circle_Event), configure Scheme, otherwise you can skip this step.

<span id="f16d52a5"></span>
### Get URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ffb6619272a543b6b3fdba77258d5d1c~tplv-goo7wpa0wc-image.image) </span>

<span id="d551c928"></span>
### Add URL Scheme

Add the URL Scheme to your project.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a7e1a46b5ed28fed194a631f2d5eef7.png) </span>

<span id="c61195a3"></span>
### Override callback method

Please use real\-time event tracking to detect or circle the device version of the event function as needed, and add processing of URLs.

Add URL handling in the `AppDelegate`callback.

```objectivec
#import <RangersAppLog/BDAutoTrackSchemeHandler.h>
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey, id> *)options {
    //Parameter APPID
    if ([[BDAutoTrackSchemeHandler sharedHandler] handleURL:url appID:@"appid" scene:nil]) {
        return YES;
    }
    // ……
    return NO;
}
```


In version iOS 13 +, using `UISceneSession`requires adding URL processing to the `UISceneDelegate`callback method.

`Objective-C`Please refer to:

```objectivec
#import <RangersAppLog/BDAutoTrackSchemeHandler.h>
- (void)scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts {
    for (UIOpenURLContext *context in URLContexts) {
        NSURL *URL = context.URL;
        //Parameter APPID
        if ([[BDAutoTrackSchemeHandler sharedHandler] handleURL:URL appID:@"{{APPID}}" scene:scene]) {
            continue;
        }
        /// ……
    }
}
```


`Swift`please refer to:

```Swift
import RangersAppLog
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {  
    //Parameter APPID
    if(BDAutoTrackSchemeHandler.shared().handle(url, appID: "{{APPID}}", scene: nil)) {
       return true
    }      
    return false
}
```
