---
title: "iOS SDK Integration"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/iOS-SDK-Integration"
---

<span id="一、-概述"></span>
# Overview

"A/B Testing" does not provide a separate SDK on the iOS client side, but relies on RangersAppLog iOS SDK The RangersAppLog SDK has two main and A/B Test related interfaces:


* Experimental group shunt interface

* Event tracking report interface


<span id="9937ce4b"></span>
# Notes before operation


* SDK version: The current SDK version is being released in continuous iterations. You can go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to view the SDK version of each end. The latest version of the SDK is recommended. The code examples in this article use a version number as an example. When you actually use it, you need to modify the version number according to the actual SDK version you are using.

* Download the SDK package: When integrating the SDK, if you need to manually import the SDK, you need to go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to download the corresponding version of the SDK package.


<span id="二、集成说明"></span>
# 1. Integrated SDK

<span id="_1-1-使用cocoapods引入source源"></span>
### 1.1 Use CocoaPods to introduce the source

In the Podfile, add the source.

```objectivec
source 'https://github.com/volcengine/volcengine-specs.git'
```


<span id="_1-2-引入sdk"></span>
### 1.2 Introduction of the SDK

In the Podfile, import the SDK and execute `pod install --repo-update`to update the Pods.

```objectivec
pod 'RangersAppLog', '6.13.1', 
    :subspecs => [
        'Host/CN', 
        'Core',
        'UITracker',
        'OneKit',
        'Log', #Can be removed if there is no need for real-time event tracking point detection, refer to chapter 1.3
        'Picker', #Can be removed if there is no need for real-time event tracking point detection, refer to chapter 4.2
        'Unique' #Used for collecting IDFA、IDFV after authorization. Can be removed if there is no need for collection, refer to chapter 4.7
    ]
```


<span id="_1-3-实时埋点检测和圈选功能-可选"></span>
### 1.3 Real\-time event tracking and circling (optional)

To use real\-time event tracking or circling, import the `Log`sublibrary. Otherwise, this step can be skipped.

Note that in addition to introducing sublibraries, you need to complete the steps below `3. Configuring Scheme`.

<span id="_1-4-反作弊风控子库-可选"></span>
### 1.4 Anti\-cheat risk control sublibrary (optional)

If you want to use the ad monitoring function, in order to make its anti\-cheat identification more accurate, please add the `VolMetaSecML`risk control sub\-library. Otherwise, this step can be skipped.

```objectivec
pod 'VolMetaSecML', '[4.3.0.5](http://4.3.0.5)-bugfix' #Anti cheating risk control sub library
```


<span id="_1-5-手动引入须知"></span>
### 1.5 Manual introduction instructions

We recommend that you introduce the SDK through CocoaPods. If special circumstances require manual introduction, please read this section. If you want to use the latest, you can contact ByteDance customer service or technical students to obtain the latest offline package.

Please go to the [iOS SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main/iOS)to obtain the corresponding version of the SDK package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">iOS offline package name is in <code><em>version number</em></code><code>.zip</code>format. For example: <code>6.16.6.zip</code>, where 6.16.6 is the SDK version number.</div>


Copy all the files from the RangersAppLog folder to the project folder and add them to the project in xcode. Add dependencies:


* libz.tbd

* libsqlite3.tbd

* CoreGraphics.framework

* CoreFoundation.framework

* Foundation.framework

* UIKit.framework

* Security.framework

* CoreTelephony.framework (read operator name)

* SystemConfiguration.framework (to determine network status)

* JavaScriptCore.framework (no need to rely on full event tracking or circling)

* WebKit.framework (no need to rely on the full event tracking, circle function and H5 pass function)

* AdSupport.framework (no dependencies without full event tracking or circling)


At the same time, you need to add other linker flags, as shown below:


* `-ObjC`

* Or `- force_load $ (PROJECT_DIR)/yourpath/RangersAppLog.framework/Versions/A/RangersAppLog`


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da053c13da40f5714e013b047ba0ac23.png) </span>

Note: If you use the manual import SDK method, you need to configure the header search when importing the file below, and you can directly import the file after configuration.

For example:

```json
#import "BDAutoTrack.h"
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1baf26397d70140da4cdf25f0735e204.png) </span>

<span id="_2-初始化sdk"></span>
## 2. Initialize the SDK

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The SDK will collect customer information during initialization. Please ensure that you have been authorized by the user before collecting user information. The recommended operations are as follows:</div>



1. <div data-tips="true" data-tips-type="tip">Initialize the SDK after authorization. All information will not be collected before authorization, but some preset events will not be collected;</div>



<span id="_2-1-获取appid"></span>
### 2.1 Get the appid

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="_2-2-获取数据上送地址"></span>
### 2.2 Obtain the data upload address

The private deployment version needs to get the data upload address.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="_2-3-初始化sdk-saas版本"></span>
### 2.3 Initializing the SDK

<span id="b1fcd481"></span>
### 2.3.1 Privatization version

If you use the private deployment version, please refer to the following code to initialize the SDK.

`Objective-C`Please refer to:

```objectivec
#import <RangersAppLog/BDAutoTrack.h>
#import <RangersAppLog/BDAutoTrackConfig.h>
#import <RangersAppLog/BDAutoTrackURLHostItemCN.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    /* Initialize SDK begins */
    // Parameter APPID: refer to chapter 2.1
    BDAutoTrackConfig*config = [BDAutoTrackConfig configWithAppID:@"{{APPID}}" launchOptions:launchOptions];
    // Set channel. For iOS, the default channel is App Store.
    config.channel = @"App Store"; 
    
    // Set private deployment data reporting address. Refer to chapter 2.2. {{REPORT_URL}} for example: https://yourdomain.com, note that do not add "/" after domain name
    config.serviceVendor = BDAutoTrackServiceVendorPrivate;
    BDAutoTrackRequestHostBlock block =
        ^NSString *(BDAutoTrackServiceVendor vendor, BDAutoTrackRequestURLType requestURLType) {
            return @"{{REPORT_URL}}";
        };
    [BDAutoTrack setRequestHostBlock:block];
    config.abEnable = YES; //enable AB testing, the default is YES
    config.autoTrackEnabled = YES; // Full event tracking switch. YES indicates enabled, while NO indicates disabled.
    config.showDebugLog = NO; // YES:open log, need to refer to chapter 4.3 to set Logger, NO: close log
    config.clearABCacheOnUserChange = YES;//By default, after switching users, A/B configuration information needs to be retrieved again. If you want to disable it, set the clearABCacheOnUserChange configuration to NO.
    config.logNeedEncrypt = YES; // encryption switch，YES indicates turn on，NO indicates turn off
    [BDAutoTrack sharedTrackWithConfig:config]; //SDK initialization
    /* Initialize SDK ends */
    
    [[BDAutoTrack sharedTrack] startTrack]; //SDK start
```


`Swift`please refer to:

```swift
import RangersAppLog
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        /* Initialize the SDK to start */
        //Parameter APPID: refer to Section 2.1 to obtain
        let config = BDAutoTrackConfig(appID: "{{APPID}}")
        //Set the channel, iOS the general default App Store channel
        config.channel = "App Store"
        
        //Set the private deployment data upload address, refer to Section 2.2 to obtain, {{REPORT_URL}} For example https://yourdomain.com, be careful not to add "/" after the domain name
        BDAutoTrack.setRequestHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
            return "{{REPORT_URL}}"
        }
        config.abEnable = true //Open ab test, default to true
        config.autoTrackEnabled = true //Full event tracking switch, true on, false off
        config.showDebugLog = false //true: to turn on the log, you need to refer to 4.3 to set the Logger, false: to turn off the log
        config.clearABCacheOnUserChange = true//By default, switch the user to get the A/B configuration information again. If you want to close it, set the clearABCacheOnUserChange configuration item to false.
        config.logNeedEncrypt = true //Encryption switch, true on, false off
        BDAutoTrack.sharedTrack(with: config)
        /* End of initialization SDK */  
        
        BDAutoTrack.shared().start() //SDK launch
        return true
    }
```


<span id="69a09656"></span>
### 2.5 Multi\-instance initialization (optional)

Multi\-instance initialization means that the SDK supports event tracking to multiple applications (multiple appids) in apps with the same package name, and the event tracking data is isolated from each other, and each appid corresponds to a separate instance. Usage scenarios such as:


* When the third\-party SDK relies on the growth marketing suite SDK to do event tracking generated within the SDK;

* In the same app or system, associate multiple event tracking apps (multiple appids), share, and grow the marketing suite SDK.


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

```swift
let config1 = BDAutoTrackConfig.init(appID: "{{APPID_1}}", launchOptions: launchOptions)
let tracker1 = BDAutoTrack.init(config: config1);
tracker1!.start()

let config2 = BDAutoTrackConfig.init(appID: "{{APPID_2}}", launchOptions: launchOptions)
let tracker2 = BDAutoTrack.init(config: config2);
tracker2!.start()
```


<span id="_3-配置scheme-可选"></span>
## 3. Configuration Scheme (optional)

To use [real-time event tracking](https://www.volcengine.com/docs/6285/66054) or [circle events](https://www.volcengine.com/docs/6285/66197), configure Scheme. Otherwise, this step can be skipped.

<span id="_3-1-获取url-scheme"></span>
### 3.1 Obtaining URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3fc47667b264d36bad9a4f9df2f3863~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-添加url-scheme"></span>
### 3.2 Adding URL Schemes

Add the URL Scheme to your project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a1060c0ae5424ed8995e649e647697f1~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-重写回调方法"></span>
### 3.3 Rewriting callback methods

Please use real\-time event tracking to detect or circle the device version of the event function as needed, and add processing of URLs.

If you use a device under iOS 13, override UIApplicationDelegate callback method.

```objectivec
#import <RangersAppLog/BDAutoTrackSchemeHandler.h>
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey, id> *)options {
    //Parameter APPID: refer to Section 2.1 to obtain
    if ([[BDAutoTrackSchemeHandler sharedHandler] handleURL:url appID:@"appid" scene:nil]) {
        return YES;
    }
    // ……
    return NO;
}
```


If you use devices iOS 13 and above, override the UISceneDelegate callback method.

`Objective-C`Please refer to:

```objectivec
#import <RangersAppLog/BDAutoTrackSchemeHandler.h>
- (void)scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts {
    for (UIOpenURLContext *context in URLContexts) {
        NSURL *URL = context.URL;
        //Parameter APPID: refer to Section 2.1 to obtain
        if ([[BDAutoTrackSchemeHandler sharedHandler] handleURL:URL appID:@"{{APPID}}" scene:scene]) {
            continue;
        }
        /// ……
    }
}
```


`Swift`please refer to:

```swift
import RangersAppLog
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {  
    //Parameter APPID: refer to Section 2.1 to obtain
    if(BDAutoTrackSchemeHandler.shared().handle(url, appID: "{{APPID}}", scene: nil)) {
       return true
    }      
    return false
}
```


<span id="_4-初始化基本配置"></span>
## 4. Initialize the basic configuration

The following are the common initialization basic configuration, `config`refers to the initialization of the `BDAutoTrackConfig`.

<span id="dcf33356"></span>
### 4.1 Full event tracking settings switch

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">⚠️ Note that the full event tracking switch is turned on by default.</div>


`Objective-C`Please refer to:

```objectivec
// Enable the upload of full event tracking point events
config.autoTrackEnabled = YES; // Full event tracking switch. YES indicates enabled, while NO indicates disabled.
```


`Swift`please refer to:

```plain
// Enable the upload of full event tracking point events
config.autoTrackEnabled = true // Full event tracking switch, true indicates turn on, false indicates turn off
```


<span id="f370bbe7"></span>
### 4.2 Turn on event tracking

In the introduction of Section 1.2, the `Picker sublibrary`was introduced to enable circling event tracking. Instead, removing the `Picker sublibrary`turns off the circled event tracking.

<span id="1a0b9237"></span>
### 4.3 View log printing

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">⚠️ Please note that log printing is turned off by default, and it is recommended that production packages be turned off online.</div>


`Objective-C`Please refer to:

```objectivec
// Output log in console, which can be used for observing user behavior logs reporting, and it is recommended to turn off when go online.
config.showDebugLog = NO; // YES: enable log, NO: disable log
config.logger = ^(NSString * _Nullable log) {NSLog(@"%@",log);}; // Set Logger when enabling log
```


`Swift`please refer to:

```plain
// Output log in console, which can be used for observing user behavior logs reporting, and it is recommended to turn off when go online.
config.showDebugLog = false // true: enable log, false: disable log
config.logger = { (log) inprint(log ?? "log is nil")} // Set Logger when enabling log
```


<span id="65aaa3ea"></span>
### 4.4 AB setting switch

`Objective-C`Please refer to:

```objectivec
// AB features switch
config.abEnable = YES; //enable AB testing, the default is YES
```


`Swift`please refer to:

```swift
//AB function switch
config.abEnable = true; //Open ab test, default to true
```


<span id="ed787be0"></span>
### 4.5 Encryption setting switch

Encryption settings are enabled by default. You can turn off encryption during the debug phase to facilitate joint debugging.

`Objective-C`Please refer to:

```objectivec
// Encryption setting switch. For online version, it is recommended to turn on.
config.logNeedEncrypt = YES; // YES: turn on, NO: turn off
```


`Swift`please refer to:

```swift
//Encryption setting switch, it is recommended to turn on the online version.
config.logNeedEncrypt = true //true: open encryption, false: close encryption
```


<span id="746c7cd7"></span>
### 4.5.1 Secret SM2

State secret SM2 algorithm request encryption **only privatized version support** , the minimum version supported: 6.15.0.

Introduce the National Secret SM2 sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'Encryptor/SM2',
        ...
    ]
```



* `Objective-C`Please refer to:


```objectivec
#import "BDAutoTrackEncryptorSM2.h"

//Set SM2 encryption
NSString * const publicKey = @"your public key";
[BDAutoTrackEncryptorSM2 setPublickKey:publicKey];
config.encryptionType = BDAutoTrackEncryptionTypeCstcSM2;
```



* `Swift`please refer to:


```Swift
//Set SM2 encryption
let publicKey = "your public key"
BDAutoTrackEncryptorSM2.setPublickKey(publicKey)
config.encryptionType = .cstcSM2
```


<span id="0b172c55"></span>
### 4.6 **Switch User Clear AB Information Switch**

`Objective-C`Please refer to:

```xml
//By default, after switching users, A/B configuration information needs to be retrieved again. If you want to disable it, set the clearABCacheOnUserChange configuration to NO.
config.clearABCacheOnUserChange = YES;
```


`Swift`please refer to:

```xml
//By default, after switching users, A/B configuration information needs to be retrieved again. If you want to disable it, set the clearABCacheOnUserChange configuration to false.
config.clearABCacheOnUserChange = true
```


<span id="ace20cdb"></span>
### 4.7 Setting APP Language and APP Region

`Objective-C`Please refer to:

```objectivec
// Modify language and region, set APP Language and APP Region
[BDAutoTrack setAppLauguage:@"zh/en/jp/fr"];
[BDAutoTrack setAppRegion:@"cn"];
```


`Swift`please refer to:

```swift
//Modify language and region, set APP Language and APP Region
BDAutoTrack.setAppLauguage("zh/en/jp/fr")
BDAutoTrack.setAppRegion("cn")
```


<span id="e74a096b"></span>
### 4.8 Open the embedded H5 page

After opening the embedded H5 page, the events generated on the embedded H5 page will be reported through the iOS SDK, not the js SDK, and the `user_unique_id`and public properties set by the iOS side will be reused.

Please note that the open function also needs to integrate the js sdk on the H5 page, and turn on the open switch of js. Please refer to Section 3.6 of the Web/JS SDK Integration Development Guide.

`Objective-C`Please refer to:

```objectivec
// Enable embedding H5 switch
config.enableH5Bridge = YES;
```


`Swift`please refer to:

```swift
//Turn on the embedded H5 open switch
config.enableH5Bridge = true;
```


After the switch is turned on, the whitelist must be configured. Only the domain names configured in the whitelist take effect. The whitelist can be added by wild\-card, and `*`means wild\-card.

`Objective-C`Please refer to:

```objectivec
// Embedding H5 page whitelist configuration
// Example: If you need to connect www.volcengine.com and www.bytedance.com, these two H5 page
config.H5BridgeAllowedDomainPatterns = @[@"www.volcengine.com",@"*.bytedance.*"];

// There are multiple whitelists that can be adapted to www.bytedance.com. Please configure the whitelist according to your business scenario, for example:
// www.bytedance.com or *.bytedance.* or *.*.* all can be achieved.
```


`Swift`please refer to:

```swift
//Embedded H5 page whitelist configuration
//Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
config.h5BridgeAllowedDomainPatterns = ["[www.volcengine.com](http://www.volcengine.com/)", "*.bytedance.*"]
```


<span id="dd9dc2a7"></span>
### 4.9 Native acquisition H5 full event tracking

When the webview page is embedded in the native side, by turning on the following switch, the h5 page full event tracking event can be collected from the native side full event tracking event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">⚠️Please note that the use of this switch does not require integration with the JDK within the H5 page and is independent of the JDK full event tracking feature.</div>


`Objective-C`Please refer to:

```objectivec
//full event tracking event of embedding H5 page
config.H5AutoTrackEnabled = YES; // YES: enable H5 full event tracking event，NO: disable H5 full event tracking event
```


`Swift`please refer to:

```swift
//Embedded H5 page full event tracking event
config.H5AutoTrackEnabled = true; //true: turn on h5 full event tracking event, false: turn off h5 full event tracking event
```


<span id="16dac827"></span>
### 4.10 Turn off device IDFA and IDFV acquisition

The acquisition of device IDFA and IDFV is completed through the `Unique`sub\-library. In the introduction SDK in Section 1.2, the introduction of the `Unique`sublibrary turns on the acquisition, and the removal of the `Unique`sublibrary turns off the acquisition.

<span id="5a8d7204"></span>
### 4.11 Turn on screen orientation capture

> This section is supported after 6.11.0 +.


Introducing the DeviceOrientation sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'DeviceOrientation', #screen orientation collection
        ...
    ]
```


Screen orientation information is automatically brought into the `params`of each event tracking. The interface documentation is as follows:

```objectivec
/*! @Abstract Whether to capture the screen direction, the default does not capture (NO) */
@property (nonatomic) BOOL screenOrientationEnabled;
```



* Objective\-C Please refer to:


```objectivec
config.screenOrientationEnabled = YES;
```



* For Swift, please refer to:


```Swift
config.screenOrientationEnabled = true
```


<span id="c2c423c7"></span>
### 4.12 Setting GPS coordinates

Introducing the Location sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'Location', #GPS collection
        ...
    ]
```


GPS information is automatically brought into each event tracking `params`:

```objectivec
/*! @Abstract Whether to collect GPS, not by default (NO) */
@property (nonatomic) BOOL trackGPSLocationEnabled;
```



* `Objective-C`Please refer to:


```objectivec
config.trackGPSLocationEnabled = YES;
```



* `Swift`please refer to:


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



* `Objective-C`Please refer to:


```objectivec
[BDAutoTrack setGPSLocation:BDAutoTrackGeoCoordinateSystemWGS84 longitude:116.3683244 latitude:39.915085];
```



* `Swift`please refer to:


```Swift
BDAutoTrack.setGPSLocation(BDAutoTrackGeoCoordinateSystem.WGS84, longitude: 116.3683244, latitude: 39.915085)
```


<span id="890b7d19"></span>
### 4.13 Turn on crash acquisition

Introducing the Exception sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'Exception', #crash collection
        ...
    ]
```



* `Objective-C`Please refer to:


```objectivec
//Currently only NSException crashes are supported
config.trackCrashEnabled = YES;
```



* `Swift`please refer to:


```Swift
// Currently, only NSException crashes are supported.
config.trackCrashEnabled = true
```
