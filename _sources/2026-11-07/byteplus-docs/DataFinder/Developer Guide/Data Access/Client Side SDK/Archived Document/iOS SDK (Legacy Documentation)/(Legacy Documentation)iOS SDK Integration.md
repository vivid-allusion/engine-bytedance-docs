---
title: "(Legacy Documentation)iOS SDK Integration"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">iOS SDK integration documentation has been revised, please check the new documentation: <a href="https://docs.byteplus.com/docs/DataFinder/iOS_SDK_Integration">iOS SDK Integration</a>.</div>


You can track events on the IOS client side through the IOS SDK. The following provides you with an introduction video to the process of IOS SDK integration. You can open the corresponding video, download the demo sample file, and then combine the detailed documentation to learn the operation of IOS SDK integration.


|**Example demo** |**Explanation video** |
|---|---|
|* SaaS：<br><br>   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60d44a61b7654e419af876cf742a0f1b~tplv-goo7wpa0wc-image.image" name="iosSDKDemoSaas.zip">iosSDKDemoSaas.zip</Attachment><br>   <br><br><br>The basic integration code has been made for you in the sample demo, and you can learn and rewrite it according to the documents and videos after downloading. |<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85c90c1c6cab46dead0055b013e50cae~tplv-goo7wpa0wc-image.image" controls></video><br> |


<span id="3821cf45"></span>
# Notes before operation


* SDK version: The current SDK version is being released in continuous iterations. You can go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to view the SDK version of each end. The latest version of the SDK is recommended. The code examples in this article use a version number as an example. When you actually use it, you need to modify the version number according to the actual SDK version you are using.

* Download the SDK package: When integrating the SDK, if you need to manually import the SDK, you need to go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to download the corresponding version of the SDK package.

* When using the iOS SDK, you can start by understanding the common data reporting strategy ( [Data reporting strategy](https://docs.byteplus.com/docs/DataFinder/DataFinder_Data_Access_Overview#1e80ed67)), supported preset events ( [Android-Side Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Android-Side_Preset_Events_and_Properties)), and iOS reporting process ( [6. Reference: Data reporting process and trigger timing](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration#7812dd61)).


<span id="d7b7f360"></span>
# 1. Integrated Growth Marketing Suite SDK

<span id="a327a7a6"></span>
## 1.1 Use CocoaPods to introduce the source

In the Podfile, add the source.

```objectivec
source 'https://github.com/volcengine/volcengine-specs.git'
```


<span id="9ddb7786"></span>
## 1.2 Introduction of the SDK

In the Podfile, import the SDK and execute `pod install --repo-update`to update the Pods.


* SaaS\-cloud native (including overseas Johor)/privatized environment

   ```objectivec
   pod 'RangersAppLog', '6.17.3', 
       :subspecs => [
           'Core',
           'UITracker',#full event tracking function(optional)
           'Log', #remove circle and real-time event tracking when you do not need them, refer to chapter 1.4(optional)
           'Picker', #remove circle function when you do not need them, refer to chapter 4.2(optional)
           'Unique' #To collect IDFA after authorization, remove it when you do not need it,  refer to chapter 4.8(optional)
       ]
   ```
   


<span id="382a3b21"></span>
## 1.3 Introduction of Debugging Tools \- DevTools Component (optional)

> 6.12.0 + Support

> Development and debugging phase integration, do not bring into the online environment.


`DevTools`is a component that assists developers or testers with in\-app event tracking verification and SDK access troubleshooting.


1. SDK subspecs Add `DevTools`


```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'DevTools', 
        ...
    ]
```



2. enable relevant functions


```objectivec
#import <RangersAppLog/BDAutoTrackDevTools.h>
//Configure to enable DevTool function
config.devToolsEnabled = YES;

//Add method after BDAutoTrack initialization to display floating button entry
[BDAutoTrackDevTools showFloatingEntryButton];
```


For detailed access documentation, please refer to [iOS event tracking power builder ](https://www.volcengine.com/docs/76880/1033613).

<span id="31a0f579"></span>
## 1.4 Real\-time event tracking and circling (optional)

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification), import the `Log`sublibrary, otherwise you can skip this step.

Note that in addition to introducing sublibraries, you need to complete the steps below `3. Configuring Scheme`.

<span id="8632f037"></span>
## 1.5 Manual introduction instructions

We recommend that you introduce the SDK through CocoaPods. If special circumstances require manual introduction, please refer to this section for manual introduction.


1. Please go to the [iOS SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main/iOS)to obtain the corresponding version of the SDK package.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">iOS offline package name is in <code><em>version number</em></code><code>.zip</code>format. For example: <code>6.17.0.zip</code>, where 6.17.0 is the SDK version number.   </div>
   

2. Copy the files under the installation package to the project folder and add them to the project in XCode. Add dependencies:

* libz.tbd

* libsqlite3.tbd

* CoreGraphics.framework

* Security.framework

* CoreTelephony.framework (read operator name)

* SystemConfiguration.framework (to determine network status)

* JavaScriptCore.framework

* WebKit.framework

* AdSupport.framework (no dependencies without full event tracking or circling)

* AppTrackingTransparency framework (Unique modules do not need dependencies)


Build Settings \- \> Header Search Paths Add Headers folder path:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b276b14c3f320bc20485b05e62fae60.png) </span>

Build Settings \- \> Linking \- \> Other Linker Flags Add \-ObjC:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ae74616943fe217fb6c0dc04bb025c5.png) </span>

<span id="46951be9"></span>
# 2. Initialization, Growth Marketing Suite SDK

Description:


1. SDK initialization: SDK initialization does not obtain personal information. It is recommended that you initialize the SDK after the user agrees to the Privacy Policy in your app; before the user agrees to the Privacy Policy, you should avoid dynamically applying for sensitive device permissions involving the user's personal information, and you should avoid collecting and reporting personal information privately. When your app does not provide services to users, do not request services related to the SDK.

2. SDK startup: After the SDK is launched, information acquisition and event reporting will begin. Please proceed with the "SDK startup" step according to the required functional scenarios. For specific methods, please refer to [Control data sending after Applog initialization ](https://www.volcengine.com/docs/6287/75274).

3. It is recommended to "SDK start" as soon as possible after "SDK initialization". You can also control the timing of "SDK launch" by yourself, but because some event information before SDK launch cannot be obtained, it may affect the effect of SDK functions.


<span id="293c8938"></span>
## 2.1 Get the appid.


* In the SaaS\-cloud native scenario, you can find the corresponding application in "Project Center" \> "Project Management" \> "Project Details", click "Access Data", and view the application ID (APPID) and APP URL of the application in the application details. For details, please refer to [Project Management](https://docs.byteplus.com/docs/DataFinder/Project_Management__).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c52873d5e5ef4d7da390c4c102215d88~tplv-goo7wpa0wc-image.image) </span>


<span id="f8ddad3e"></span>
## 2.2 Obtain the data upload address

When reporting data access, you need to confirm your data reporting address according to the current environment type and terminal type. If the reporting address is set incorrectly, you will not be able to check the reported data in the future.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Please confirm the type of environment you are currently using before reporting data, and configure the reporting address according to the type of environment. To view the current environment type see <a href="https://docs.byteplus.com/docs/DataFinder/SaaS_Cloud-Native_Privatized_Environments">SaaS Cloud\-Native & Privatized Environments</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you are using a SaaS\-cloud native environment, you also need to confirm the region where your service is located, and report the address according to the region configuration (usually your service will be in Southeast Asia \- Johor region, and some users may use other regions). SaaS\-cloud native users see the region where the service is located <a href="https://docs.byteplus.com/docs/DataFinder/Supported_Regions">Supported Regions</a>.</div>



<span id="e23814ba"></span>
### SaaS\-cloud\-native


|End type |SaaS\-cloud native environment<br><br>(Overseas: Southeast Asia \- Johor) |Overseas BytePlus environment<br><br>(The following SG refers to Singapore) |
|---|---|---|
|iOS |* https://gator.uba.ap\-southeast\-1.bytepluses.com |After introducing: 'Host/SG', no configuration required |


<span id="efe0616b"></span>
### Privatized environment

In the private deployment scenario, you need to obtain the data upload address for your own planning and configuration when deploying the private environment. If you are unsure of this address, please contact your project manager or customer success manager.

<span id="1940e7f6"></span>
## 2.3 Initializing the SDK

<span id="f8450101"></span>
### 2.3.1 SaaS \- Cloud Native

If you are using the Saas cloud native deployment version, please refer to the following code to initialize the SDK. The initialization code must be executed on the main thread.


* `Objective-C`Please refer to:

   ```objectivec
   #import <RangersAppLog/BDAutoTrack.h>
   #import <RangersAppLog/BDAutoTrackConfig.h>
   #import <RangersAppLog/BDAutoTrackURLHostItemCN.h>
   // If Unique sublib is used, then header file is dependent.
   #import <RangersAppLog/BDAutoTrack+IDFA.h>
   
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
       /* Starting SDK initialization */
       // Parameter APPID: refer to 2.1 to acquire
       BDAutoTrackConfig*config = [BDAutoTrackConfig configWithAppID:@"{{APPID}}" launchOptions:launchOptions];
       // set channel. iOS usually uses the App Store as the default channel, which can be set through the following code.
       config.channel = @"App Store"; 
   
       // set data report address. You need to configure report address according to the region where the DataFinder service is used. For details, refer to the section "2.2Obtain the data upload address" above.
       config.serviceVendor = BDAutoTrackServiceVendorPrivate;
       BDAutoTrackRequestHostBlock block =
           ^NSString *(BDAutoTrackServiceVendor vendor, BDAutoTrackRequestURLType requestURLType) {
               return @"https://gator.volces.com";
           };
       [BDAutoTrack setRequestHostBlock:block];
       
       config.autoTrackEnabled = YES; // Full event tracking switch, YES means turn on，NO means turn off
       config.showDebugLog = NO; // YES:means turn on log, refer to 4.3 to configure Logger, NO:means turn off log
       config.logNeedEncrypt = YES; // encryption switch, YES means turn on, NO means turn off
       [BDAutoTrack sharedTrackWithConfig:config];
       /* Ending SDK initialization */
       
       // If Unique sublib is used, then IDFA dedicated domain names need to be configured.
       [BDAutoTrack.sharedTrack setRequestIDFAHostBlock:^NSString * _Nullable(BDAutoTrackServiceVendor  _Nonnull vendor, BDAutoTrackRequestURLType requestURLType) {
           return @"https://gator-tracking.datafinder.volces.com";
       }];
       
       // If current login status needs to be set since 6.13.0+
       // [[BDAutoTrack sharedTrack] setCurrentUserUniqueID:@"current login status UUID"]; 
       // after authorization
       [[BDAutoTrack sharedTrack] startTrack]; //SDK starts
   }
   ```
   

* `Swift`please refer to:

   ```Swift
   import RangersAppLog
       func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
           /* Initialize the SDK to start */
           //Parameter APPID: refer to Section 2.1 to obtain
           let config = BDAutoTrackConfig(appID: "{{APPID}}")
           //Set the channel, iOS the general default App Store channel
           config.channel = "App Store"
           //Set the data upload address. You need to configure the upload address according to the region where the DataFinder service is used. For details, see the above section, Get the data upload address.
           config.serviceVendor = .private
           BDAutoTrack.setRequestHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
               return "https://gator.volces.com"
           }
           
           config.autoTrackEnabled = true //Full event tracking switch, true on, false off
           config.showDebugLog = false //true: to turn on the log, you need to refer to 4.3 to set the Logger, false: to turn off the log
           config.logNeedEncrypt = true //Encryption switch, true on, false off
           BDAutoTrack.sharedTrack(with: config)
           /* End of initialization SDK */  
   
           //If using the Unique sublibrary, you need to configure the idfa dedicated domain name
           BDAutoTrack.shared().setRequestIDFAHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
               return "https://gator-tracking.datafinder.volces.com"
           }
           
           //If you need to set the current login state since 6.13.0 +
           // BDAutoTrack.shared().setCurrentUserUniqueID("uuid")
           BDAutoTrack.shared().start() //SDK launch
           return true
       }
   ```
   


<span id="2e9f8e73"></span>
### 2.3.2 Privatization version

If you use the private deployment version, please refer to the following code to initialize the SDK. The initialization code must be executed on the main thread.


* `Objective-C`Please refer to:

   ```objectivec
   #import <RangersAppLog/BDAutoTrack.h>
   #import <RangersAppLog/BDAutoTrackConfig.h>
   #import <RangersAppLog/BDAutoTrackURLHostItemCN.h>
   // If Unique sublib is used, then header file is dependent.
   #import <RangersAppLog/BDAutoTrack+IDFA.h>
   
   - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
       /* Starting SDK initialization */
       // Parameter APPID: refer to 2.1 to acquire
       BDAutoTrackConfig*config = [BDAutoTrackConfig configWithAppID:@"{{APPID}}" launchOptions:launchOptions];
       // set channel. iOS usually uses the App Store as the default channel, which can be set through the following code.
       config.channel = @"App Store"; 
       
       // set privatization data report address, refer to section 2.2 to acquire, {{REPORT_URL}} such as https://yourdomain.com, note that “/” should not be added after domain name
       config.serviceVendor = BDAutoTrackServiceVendorPrivate;
       BDAutoTrackRequestHostBlock block =
           ^NSString *(BDAutoTrackServiceVendor vendor, BDAutoTrackRequestURLType requestURLType) {
               return @"{{REPORT_URL}}";
           };
       [BDAutoTrack setRequestHostBlock:block];
       
       config.autoTrackEnabled = YES; // Full event tracking switch, YES means turn on，NO means turn off
       config.showDebugLog = NO; // YES:means turn on log, refer to 4.3 to configure Logger, NO:means turn off log
       config.logNeedEncrypt = YES; // encryption switch, YES means turn on, NO means turn off
       [BDAutoTrack sharedTrackWithConfig:config]; //SDK initialization
       /* Ending SDK initialization */
       
       // If Unique sublib is used, then IDFA dedicated domain names need to be configured.
       [BDAutoTrack.sharedTrack setRequestIDFAHostBlock:^NSString * _Nullable(BDAutoTrackServiceVendor  _Nonnull vendor, BDAutoTrackRequestURLType requestURLType) {
           return @"{{IDFA_REPORT_URL}}";
       }];
       
       // If current login status needs to be set since 6.13.0+
       // [[BDAutoTrack sharedTrack] setCurrentUserUniqueID:@"current login status UUID"]; 
       // after authorization
       [[BDAutoTrack sharedTrack] startTrack]; //SDK starts
   }
   ```
   

* `Swift`please refer to:

   ```Swift
   import RangersAppLog
       func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
           /* Initialize the SDK to start */
           //Parameter APPID: refer to Section 2.1 to obtain
           let config = BDAutoTrackConfig(appID: "{{APPID}}")
           //Set the channel, iOS the general default App Store channel
           config.channel = "App Store"
           
           //Set the private deployment data upload address, refer to Section 2.2 to obtain, {{REPORT_URL}} For example https://yourdomain.com, be careful not to add "/" after the domain name
           config.serviceVendor = .private
           BDAutoTrack.setRequestHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
               return "{{REPORT_URL}}"
           }
           
           config.autoTrackEnabled = true //Full event tracking switch, true on, false off
           config.showDebugLog = false //true: to turn on the log, you need to refer to 4.3 to set the Logger, false: to turn off the log
           config.logNeedEncrypt = true //Encryption switch, true on, false off
           BDAutoTrack.sharedTrack(with: config)
           /* End of initialization SDK */ 
           
           //If using the Unique sublibrary, you need to configure the idfa dedicated domain name
           BDAutoTrack.shared().setRequestIDFAHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
               return "{{IDFA_REPORT_URL}}"
           }
           
           //If you need to set the current login state since 6.13.0 +
           // BDAutoTrack.shared().setCurrentUserUniqueID("uuid")
           //After authorization
           BDAutoTrack.shared().start() //SDK launch
           return true
       }
   ```
   


<span id="39895991"></span>
## 2.4 Multi\-instance initialization (optional)

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


<span id="10ed1e35"></span>
# 3. Configuration Scheme (optional)

To use [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)OR , configure Scheme, otherwise you can skip this step.

<span id="645f39b0"></span>
## 3.1 Obtaining URL Scheme

"Application List" \- \> "Details" of the access application \- \> "URL Scheme" to view your scheme, usually in the form of `rangersapplog.xxxxx.`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f0f0d7dd6254793b59ab215afdda162~tplv-goo7wpa0wc-image.image) </span>

<span id="875b3c68"></span>
## 3.2 Adding the URL Scheme

Add the URL Scheme to your project.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18335d4c69334b5487dfbdef2b4ee2aa~tplv-goo7wpa0wc-image.image) </span>

<span id="bb6aeaef"></span>
## 3.3 Rewriting callback methods

Please use real\-time event tracking to detect or circle the device version of the event function as needed, and add processing of URLs.

Add URL handling in the `AppDelegate`callback.

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


In version iOS 13 +, using `UISceneSession`requires adding URL processing to the `UISceneDelegate`callback method.


* `Objective-C`Please refer to:

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
   

* `Swift`please refer to:

   ```Swift
   import RangersAppLog
   func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {  
       //Parameter APPID: refer to Section 2.1 to obtain
       if(BDAutoTrackSchemeHandler.shared().handle(url, appID: "{{APPID}}", scene: nil)) {
          return true
       }      
       return false
   }
   ```
   


<span id="2d3b7121"></span>
# 4. Initialize the basic configuration

The following are the common initialization basic configuration, `config`refers to the initialization of the `BDAutoTrackConfig`.

<span id="d3d87ef9"></span>
## 4.1 Full event tracking setting switch

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The full event tracking switch is on by default. After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.</div>



* <div data-tips="true" data-tips-type="warning">SaaS\-cloud native and privatization scenarios: Go to Project Center \> Project Management \> SDK Settings and make sure the full event tracking switch is turned on.</div>


* `Objective-C`Please refer to:

   ```objectivec
   //Open the upload of the full event tracking event
   config.autoTrackEnabled = YES; //Full event tracking switch, YES on, NO off
   ```
   

* `Swift`please refer to:

   ```Swift
   //Open the upload of the full event tracking event
   config.autoTrackEnabled = true //Full event tracking switch, true on, false off
   ```
   


<span id="3d50d607"></span>
## 4.2 Turn on event tracking

In the introduction of Section 1.2, the `Picker sublibrary`was introduced to enable circling event tracking. Instead, removing the `Picker sublibrary`turns off the circled event tracking.

<span id="2e7be575"></span>
## 4.3 View log printing

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Log printing is turned off by default, and it is recommended that the online production package be turned off.</div>



* `Objective-C`Please refer to:

   ```objectivec
   //Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
   config.showDebugLog = NO; //YES: open log, NO: close log
   ```
   

* `Swift`please refer to:

   ```Swift
   //Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
   config.showDebugLog = false //true: open log, false: close log
   ```
   


<span id="1ea26661"></span>
## 4.4 Encryption setting switch

Encryption settings are enabled by default. You can turn off encryption during the debug phase to facilitate joint debugging.


* `Objective-C`Please refer to:

   ```objectivec
   //Encryption setting switch, it is recommended to turn on the online version.
   config.logNeedEncrypt = YES; //YES: Encryption turned on, NO: Encryption turned off
   ```
   

* `Swift`please refer to:

   ```Swift
   //Encryption setting switch, it is recommended to turn on the online version.
   config.logNeedEncrypt = true //true: open encryption, false: close encryption
   ```
   


<span id="f40cd71f"></span>
### 4.4.1 secret SM2

State secret SM2 algorithm request encryption **only privatized version support** , the minimum version supported: 6.15.0.

Introduce the National Secret SM2 sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'Encryptor/SM2', #only privatization supported
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
   


<span id="2187f465"></span>
## 4.5 Set APP Language and APP Region


* `Objective-C`Please refer to:

   ```objectivec
   //Modify language and region, set APP Language and APP Region
   [BDAutoTrack setAppLauguage:@"zh/en/jp/fr"];
   [BDAutoTrack setAppRegion:@"cn"];
   ```
   

* `Swift`please refer to:

   ```Swift
   //Modify language and region, set APP Language and APP Region
   BDAutoTrack.setAppLauguage("zh/en/jp/fr")
   BDAutoTrack.setAppRegion("cn")
   ```
   


<span id="fccf2ddc"></span>
## 4.6 Open the embedded H5 page

After opening the embedded H5 page, the events generated on the embedded H5 page will be reported through the iOS SDK, not the js SDK, and the `user_unique_id`and public attributes set by the iOS side will be reused, but the uuid on the web side setting/update side when opening is also supported (if you need to support the update of multi\-caliber from the web side, you need to use the new version of the SDK)/public attributes.

Please note that the open function also needs to integrate the js SDK on the H5 page and turn on the open switch of js, please refer to [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_)Section 3.4. After getting through, the H5 full event tracking function is blocked by default. If you still want to collect H5 full event tracking, you need to check Section 4.7: Native collection of H5 full event tracking.


* `Objective-C`Please refer to:

   ```objectivec
   //Turn on the embedded H5 open switch
   config.enableH5Bridge = YES;
   ```
   

* `Swift`please refer to:

   ```Swift
   //Turn on the embedded H5 open switch
   config.enableH5Bridge = true;
   ```
   


After the switch is turned on, the whitelist must be configured. Only the domain names configured in the whitelist take effect. The whitelist can be added by wild\-card, and `*`means wild\-card.


* `Objective-C`Please refer to:

   ```objectivec
   //Embedded H5 page whitelist configuration
   //Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
   config.H5BridgeAllowedDomainPatterns = @[@"www.volcengine.com",@"*.bytedance.*"];
   
   //There are many whitelists for adaptation www.bytedance.com, please configure the whitelist according to the business scenario, for example:
   //www.bytedance.com or * .bytedance. * or *.*.* .
   ```
   

* `Swift`please refer to:

   ```Swift
   //Embedded H5 page whitelist configuration
   //Example: If you need to get through www.volcengine.com and www.bytedance.com two H5 pages
   config.h5BridgeAllowedDomainPatterns = ["www.volcengine.com", "*.bytedance.*"]
   ```
   


When getting through, the in\-terminal SDK user information is used by default, but it also supports the H5 side to update the in\-terminal SDK user information through the Web SDK.

iOS 6.17.2 version of the new ban to get through the embedded H5 page prohibits H5 update App user information, in order to avoid H5 multi\-use update user information code is not easy to remove, thereby destroying the original user information in the end of the SDK when getting through.

```java
//On by default, support off
config.useBridgeUpdateUUIDEnabled = YES;
```


<span id="f738d14a"></span>
## 4.7 Native acquisition H5 full event tracking

When the webview page is embedded in the native side, by turning on the following switch, the h5 page full event tracking event can be collected from the native side full event tracking event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The use of this switch does not require integration of the js SDK within the h5 page, and is independent of the js SDK full event tracking feature.</div>



* `Objective-C`Please refer to:

   ```objectivec
   //Embedded H5 page full event tracking event
   config.H5AutoTrackEnabled = YES; //YES: Turn on h5 full event tracking event, NO: Turn off h5 full event tracking event
   ```
   

* `Swift`please refer to:

   ```Swift
   //Embedded H5 page full event tracking event
   config.H5AutoTrackEnabled = true; //true: turn on h5 full event tracking event, false: turn off h5 full event tracking event
   ```
   


<span id="1162bc26"></span>
## 4.8 Turn off device IDFA acquisition

The acquisition of the device IDFA is done through the `Unique`sublibrary. In the introduction SDK in Section 1.2, the introduction of the `Unique`sublibrary will turn on the collection, and the removal of the `Unique`sublibrary will turn off the collection.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SaaS\-cloud native and privatized 4.4.0 versions and above also support turning off sensitive field collection in the DataFinder console, you can turn off IDFA field collection in Project Management \> SDK Settings, see details <a href="https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings">Project Management \- SDK Settings</a>.</div>


<span id="6a2bf5c3"></span>
## 4.9 Turn on screen orientation capture

> This section is supported after 6.11.0 +.


Introducing the DeviceOrientation sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'DeviceOrientation', #collect screen orientation
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
   


<span id="c2dc7e1c"></span>
## 4.10 Setting GPS coordinates

Introducing the Location sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'Location', #GPS collecting
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
   


<span id="e59b41ad"></span>
## 4.11 Turn on crash acquisition

Introducing the Exception sublibrary:

```objectivec
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        ...
        'Exception', #crash collecting
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
   //Currently only NSException crashes are supported
   config.trackCrashEnabled = true
   ```
   


<span id="9e7913ad"></span>
## 4.12 Turn off clipboard acquisition

Clipboard collects the ALink function used for advertising monitoring products. When this function module is turned on, the collection of clipboard information is turned on, and the collection of clipboard is disabled when it is turned off.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After turning off clipboard collection, the Alink attribution of ad monitoring may be affected. Please confirm whether the ad monitoring related functions are used before closing.</div>


* <div data-tips="true" data-tips-type="tip">iOS system from version 16, getting clipboard information will trigger a pop\-up window, so if you turn on the clipboard capture switch, when the ALink function collects the clipboard when the SDK is started, the pop\-up window will be triggered. It is recommended that you evaluate the timing of obtaining a clipboard based on the actual business situation.</div>


* `Objective-C`Please refer to:

   ```objectivec
   //turn on DeferredALink function
   //turn this function off will stop collecting clipboard information
   config.enableDeferredALink = NO;
   
   ```
   

* `Swift`please refer to:

   ```Swift
   //Enable the DeferredALink function
   //Turn off this function will not collect clipboard information
   config.enableDeferredALink = false;
   ```
   


<span id="363f18e6"></span>
# 5. Introduction to other functions

<span id="79db3b38"></span>
## 5.1 Cloud control capabilities

Note: This feature is only available in SaaS cloud native version or privatized version V4.4.0 or above, and is supported by SDK6.15.0 or above.

DataFinder supports sending SDK settings through the server level, including reporting timing, full event tracking switch, etc. [Project Management - SDK Settings](https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings).

<span id="7812dd61"></span>
# 6. Reference: Data reporting process and trigger timing

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">SaaS\-cloud native, privatized environment supports setting the basic settings of Android, iOS, web, and Mini Program platform SDKs in the DataFinder console, including whether to enable full event tracking, event tracking report timing, and so on. The following is the default reporting process and mechanism on the end, you can also configure and adjust it in the DataFinder console, see details <a href="https://docs.byteplus.com/docs/DataFinder/Project_Management_-_SDK_Settings">Project Management \- SDK Settings</a>.</div>


<span id="a5ebb1dc"></span>
## Event event upload

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMjU1cHgiIGhlaWdodD0iNDI1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMjU1IDQyNSI+PGRlZnMvPjxnPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSIxMjUwIiBoZWlnaHQ9IjQyMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjZTZlNmU2IiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxODIgMjAyIEwgMjAyIDIwMiBMIDE5MiAyMDIgTCAyMDUuNjMgMjAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjEwLjg4IDIwMiBMIDIwMy44OCAyMDUuNSBMIDIwNS42MyAyMDIgTCAyMDMuODggMTk4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMiIgeT0iMjIiIHdpZHRoPSIxNjAiIGhlaWdodD0iMzYwIiByeD0iMjQiIHJ5PSIyNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzMDIgMjAyIEwgMzIyIDIwMiBMIDMxMiAyMDIgTCAzMjUuNjMgMjAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzMwLjg4IDIwMiBMIDMyMy44OCAyMDUuNSBMIDMyNS42MyAyMDIgTCAzMjMuODggMTk4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMTIiIHk9IjE4MiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjAycHg7IG1hcmdpbi1sZWZ0OiAyMTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+RGF0YSByZXBvcnRpbmc8L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MiIgeT0iNjIiIHdpZHRoPSIxMDAiIGhlaWdodD0iMzAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzdweDsgbWFyZ2luLWxlZnQ6IDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNvbGQgc3RhcnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjUyIiB5PSIxMDIiIHdpZHRoPSIxMDAiIGhlaWdodD0iMzAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTE3cHg7IG1hcmdpbi1sZWZ0OiA1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5EZXZpY2UgcmVnaXN0cmF0aW9uIGNvbXBsZXRlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MiIgeT0iMTQyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjMwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE1N3B4OyBtYXJnaW4tbGVmdDogNTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VXNlciBzd2l0Y2hlcyB0byB0aGUgZnJvbnQgZW5kPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MiIgeT0iMTgyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjQwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogNTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGltZXI8YnIgLz4ob25jZSBldmVyeSA2MCBzZWNvbmRzKTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTIiIHk9IjIzMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNDdweDsgbWFyZ2luLWxlZnQ6IDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlVzZXIgc3dpdGNoZXMgdG8gdGhlIGJhY2sgZW5kPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1MiIgeT0iMjcyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjMwIiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI4N3B4OyBtYXJnaW4tbGVmdDogNTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Rmx1c2ggYWN0aXZlIHRyaWdnZXJpbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjgyIiB5PSIyODIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIxMDAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgdHJhbnNmb3JtPSJyb3RhdGUoOTAsMTAyLDMzMikiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzMnB4OyBtYXJnaW4tbGVmdDogNTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VGhlIGNvbGxlY3Rpb24gdGltZSBleGNlZWRzIHRoZSB0aHJlc2hvbGQgKDIwMCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjcyIiB5PSIzMiIgd2lkdGg9IjUwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA0OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQycHg7IG1hcmdpbi1sZWZ0OiA3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VHJpZ2dlciB0aW1lPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDQ3MiAyMDIgTCA0OTIgMjAyIEwgNDc3IDIwMiBMIDQ5MC42MyAyMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0OTUuODggMjAyIEwgNDg4Ljg4IDIwNS41IEwgNDkwLjYzIDIwMiBMIDQ4OC44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDAyIDI1MiBMIDQwMiAyOTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDIgMzAwLjg4IEwgMzk4LjUgMjkzLjg4IEwgNDAyIDI5NS42MyBMIDQwNS41IDI5My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDAyIDE1MiBMIDQ3MiAyMDIgTCA0MDIgMjUyIEwgMzMyIDIwMiBaIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogMzMzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48YnIgLz5kZXZpY2VfaWQgJmFtcDsgaW5zdGFsbCBJRDxiciAvPmNoZWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDU4NyAyMDIgTCA2MDcgMjAyIEwgNTkyIDIwMiBMIDYwNS42MyAyMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MTAuODggMjAyIEwgNjAzLjg4IDIwNS41IEwgNjA1LjYzIDIwMiBMIDYwMy44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ5NyIgeT0iMTgyIiB3aWR0aD0iOTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMDJweDsgbWFyZ2luLWxlZnQ6IDQ5OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5EYXRhIHBhY2thZ2luZzwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNzIyIDIwMiBMIDc0MiAyMDIgTCA3MjIgMjAyIEwgNzM1LjYzIDIwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc0MC44OCAyMDIgTCA3MzMuODggMjA1LjUgTCA3MzUuNjMgMjAyIEwgNzMzLjg4IDE5OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNjEyIiB5PSIxODIiIHdpZHRoPSIxMTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTA4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjAycHg7IG1hcmdpbi1sZWZ0OiA2MTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+Rmlyc3QgcmVxdWVzdDwvYj48YnIgLz5NYXggZXZlbnRzIGFtb3VudDogMjAwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDY2NyAyOTIgTCA2NjcgMzEyIEwgNjY3IDMwMiBMIDY2NyAzMTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NjcgMzIwLjg4IEwgNjYzLjUgMzEzLjg4IEwgNjY3IDMxNS42MyBMIDY3MC41IDMxMy44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzIyIDI3MiBMIDc4NyAyNzIgTCA3ODcgMjI4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzg3IDIyMy4xMiBMIDc5MC41IDIzMC4xMiBMIDc4NyAyMjguMzcgTCA3ODMuNSAyMzAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI2MTIiIHk9IjI1MiIgd2lkdGg9IjExMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNzJweDsgbWFyZ2luLWxlZnQ6IDYxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5TdWJzZXF1ZW50IHJlcXVlc3RzwqA8L2I+TWF4ZXZlbnRzIGFtb3VudDogMjAwPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MTIiIHk9IjMyMiIgd2lkdGg9IjExMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMDhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNDJweDsgbWFyZ2luLWxlZnQ6IDYxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5ObyBldmVudCB0ZXJtaW5hdGlvbjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gODMyIDIwMiBMIDg1MiAyMDIgTCA4MzIgMjAyIEwgODQ1LjYzIDIwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MC44OCAyMDIgTCA4NDMuODggMjA1LjUgTCA4NDUuNjMgMjAyIEwgODQzLjg4IDE5OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iNzQyIiB5PSIxODIiIHdpZHRoPSI5MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogNzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPkNvbXByZXNzaW9uICZhbXA7IGVuY3J5cHRpb248L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDk0MiAyMDIgTCA5NjIgMjAyIEwgOTQyIDIwMiBMIDk1NS42MyAyMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA5NjAuODggMjAyIEwgOTUzLjg4IDIwNS41IEwgOTU1LjYzIDIwMiBMIDk1My44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9Ijg1MiIgeT0iMTgyIiB3aWR0aD0iOTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMDJweDsgbWFyZ2luLWxlZnQ6IDg1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5EYXRhIHJlcG9ydGluZzwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTAzMiAxNTIgTCAxMDMyIDk4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTAzMiA5My4xMiBMIDEwMzUuNSAxMDAuMTIgTCAxMDMyIDk4LjM3IEwgMTAyOC41IDEwMC4xMiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTEwMiAyMDIgTCAxMTM1LjYzIDIwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDExNDAuODggMjAyIEwgMTEzMy44OCAyMDUuNSBMIDExMzUuNjMgMjAyIEwgMTEzMy44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMTAzMiAxNTIgTCAxMTAyIDIwMiBMIDEwMzIgMjUyIEwgOTYyIDIwMiBaIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogOTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5SZXNwb25zZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iOTg3IiB5PSI1MiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNzJweDsgbWFyZ2luLWxlZnQ6IDk4OHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5SZXRyeS9kZWNyZWFzZSBmcmVxdWVuY3k8L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMTQyIiB5PSIxODIiIHdpZHRoPSI5MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogMTE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5EZWxldGUgY2FjaGU8L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIxMTQyIiB5PSIyNTIiIHdpZHRoPSI5MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI3MnB4OyBtYXJnaW4tbGVmdDogMTE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5VcGRhdGUgY29uZmlndXJhdGlvbjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjExNDIiIHk9IjMxMiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzMycHg7IG1hcmdpbi1sZWZ0OiAxMTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPlJlcXVlc3QgdG8gaW5jcmVhc2UgZnJlcXVlbmN5PC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzU3IiB5PSIzMDIiIHdpZHRoPSI5MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyMnB4OyBtYXJnaW4tbGVmdDogMzU4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPldhaXQgdGlsbCBkZXZpY2UgcmVnaXN0ZXI8L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NjEiIHk9IjE4MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogNDYycHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlllczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzkyIiB5PSIyNjIiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNzJweDsgbWFyZ2luLWxlZnQ6IDM5M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5ObzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTAzNyIgeT0iMTEyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAxMDM4cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZhaWw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMTEyMiAyMDMgTCAxMTIyIDI3MiBMIDExMzUuNjMgMjcyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTE0MC44OCAyNzIgTCAxMTMzLjg4IDI3NS41IEwgMTEzNS42MyAyNzIgTCAxMTMzLjg4IDI2OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxMTIyLjEyIDIwMi42MiBMIDExMjIuMSAyNTcuNSBMIDExMjIgMjU3LjUgTCAxMTIyIDMzMiBMIDExMzUuNjMgMzMyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTE0MC44OCAzMzIgTCAxMTMzLjg4IDMzNS41IEwgMTEzNS42MyAzMzIgTCAxMTMzLjg4IDMyOC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxMTE1LjEyIDIwMi42MiBMIDExMTUuMSAyODIgTCA3MjguMzcgMjgyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzIzLjEyIDI4MiBMIDczMC4xMiAyNzguNSBMIDcyOC4zNyAyODIgTCA3MzAuMTIgMjg1LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxMDk5IiB5PSIxODMiIHdpZHRoPSI0MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTNweDsgbWFyZ2luLWxlZnQ6IDExMDBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+U3VjY2VzczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />


* **Event reporting trigger timing:** 

   * **Cold start:**  The first time the user opens the app or opens it again after the app is completely closed.

   * **Switch foreground:**  The application changes from the background to an active state where users can see and interact with it. For example, when using an app, you press the home button or switch to another app. When you return to the previous app, it switches from the background to the foreground.

   * **Switch background:**  The app goes from active to inactive, and while it's still running, you can't see it on the screen. For example, when using an APP, and then pressing the home button or switching to another APP, the APP enters the background.

   * **User Flush active trigger:**  active call \- (void) flush interface triggers the report. The SDK has a frequency limit and can be triggered at most once every 10 seconds.

   * **Device registration is complete:**  SDK internal logic, obtain the device ID for event reporting.

   * **Number of acquisition events exceeds threshold:**  default 200.

   * **Timer:**  Default 60s upload once.

* **Incident reporting pre\-check:** 

   * device_id & installID check (registration interface returns).

* **Data packaging:** 

   * The maximum number of events for the first request pack is 200.

   * After the first request is successful, more than 200 subsequent events will be packaged into the reporting process, and no more than 200 at a time.

* **Data reporting:** 

   * After the report is successful, delete the local database storage, update the local configuration, and try the frequency control upgrade.

   * After reporting the failure, retry the current request, and the status code 5xx will perform frequency control downgrade processing.

* **Request frequency control:** 

   * The total number of times the data is reported within a certain period of time is limited by the frequency control. After the frequency control is exceeded, even if a new reporting trigger is received, it will not be processed.

   * After the request fails, the status code is 5xx, which will reduce the current frequency control number.

   * After the request is successful, the previous frequency control attempt to reduce is resumed.


<span id="257bcc8e"></span>
## Profile User Attributes Upload

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMDM1cHgiIGhlaWdodD0iNDI1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMDM1IDQyNSI+PGRlZnMvPjxnPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSIxMDMwIiBoZWlnaHQ9IjQyMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjZTZlNmU2IiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAxODIgMjAyIEwgMjAyIDIwMiBMIDE5MiAyMDIgTCAyMDUuNjMgMjAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjEwLjg4IDIwMiBMIDIwMy44OCAyMDUuNSBMIDIwNS42MyAyMDIgTCAyMDMuODggMTk4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMiIgeT0iMTEyIiB3aWR0aD0iMTYwIiBoZWlnaHQ9IjE4MCIgcng9IjI0IiByeT0iMjQiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzAyIDIwMiBMIDMyMiAyMDIgTCAzMTIgMjAyIEwgMzI1LjYzIDIwMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDMzMC44OCAyMDIgTCAzMjMuODggMjA1LjUgTCAzMjUuNjMgMjAyIEwgMzIzLjg4IDE5OC41IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjEyIiB5PSIxODIiIHdpZHRoPSI5MCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA4OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPkRhdGEgcmVwb3J0aW5nPC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTIiIHk9IjE1MiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNjdweDsgbWFyZ2luLWxlZnQ6IDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkNvbGQgc3RhcnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjUyIiB5PSIxOTIiIHdpZHRoPSIxMDAiIGhlaWdodD0iMzAiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjA3cHg7IG1hcmdpbi1sZWZ0OiA1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5Qcm9maWxlIG5ld2x5LWFkZDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTIiIHk9IjIzMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSIzMCIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyNDdweDsgbWFyZ2luLWxlZnQ6IDUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRldmljZcKgcmVnaXN0cmF0aW9uIGNvbXBsZXRlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3MiIgeT0iMTIyIiB3aWR0aD0iNTAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDQ4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTMycHg7IG1hcmdpbi1sZWZ0OiA3M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+VHJpZ2dlcmVkIHRpbWU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDcyIDIwMiBMIDUwNS42MyAyMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA1MTAuODggMjAyIEwgNTAzLjg4IDIwNS41IEwgNTA1LjYzIDIwMiBMIDUwMy44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDAyIDI1MiBMIDQwMiAyOTUuNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDIgMzAwLjg4IEwgMzk4LjUgMjkzLjg4IEwgNDAyIDI5NS42MyBMIDQwNS41IDI5My44OCBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNDAyIDE1MiBMIDQ3MiAyMDIgTCA0MDIgMjUyIEwgMzMyIDIwMiBaIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIwMnB4OyBtYXJnaW4tbGVmdDogMzMzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGZvbnQtd2VpZ2h0OiBib2xkOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48YnIgLz5kZXZpY2VfaWQgJmFtcDsgaW5zdGFsbCBJRDxiciAvPmNoZWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDYwMiAyMDIgTCA2MjIgMjAyIEwgNjAyIDIwMiBMIDYxNS42MyAyMDIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2MjAuODggMjAyIEwgNjEzLjg4IDIwNS41IEwgNjE1LjYzIDIwMiBMIDYxMy44OCAxOTguNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjUxMiIgeT0iMTgyIiB3aWR0aD0iOTAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMDJweDsgbWFyZ2luLWxlZnQ6IDUxM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Yj5Db21wcmVzc2lvbiAmYW1wOyBlbmNyeXB0aW9uPC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3MTIgMjAyIEwgNzMyIDIwMiBMIDcxMiAyMDIgTCA3MjUuNjMgMjAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzMwLjg4IDIwMiBMIDcyMy44OCAyMDUuNSBMIDcyNS42MyAyMDIgTCA3MjMuODggMTk4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI2MjIiIHk9IjE4MiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjAycHg7IG1hcmdpbi1sZWZ0OiA2MjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+RGF0YSByZXBvcnRpbmc8L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDgwMiAyNTIgTCA4MDIgMjg1LjYzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gODAyIDI5MC44OCBMIDc5OC41IDI4My44OCBMIDgwMiAyODUuNjMgTCA4MDUuNSAyODMuODggWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDg3MiAyMDIgTCA5MDUuNjMgMjAyIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gOTEwLjg4IDIwMiBMIDkwMy44OCAyMDUuNSBMIDkwNS42MyAyMDIgTCA5MDMuODggMTk4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDgwMiAxNTIgTCA4NzIgMjAyIEwgODAyIDI1MiBMIDczMiAyMDIgWiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMzhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMDJweDsgbWFyZ2luLWxlZnQ6IDczM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBmb250LXdlaWdodDogYm9sZDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+UmVzcG9uc2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijc0MiIgeT0iMjkyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMxMnB4OyBtYXJnaW4tbGVmdDogNzQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxiPldhaXQgdGlsbCBuZXh0IHVwbG9hZCBzaWduYWw8L2I+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI5MTIiIHk9IjE4MiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjAycHg7IG1hcmdpbi1sZWZ0OiA5MTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+RGVsZXRlIGNhY2hlPC9iPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzNTcgMzIyIEwgMjM0LjUgMzIyIEwgMjM0LjUgMjI4LjM3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjM0LjUgMjIzLjEyIEwgMjM4IDIzMC4xMiBMIDIzNC41IDIyOC4zNyBMIDIzMSAyMzAuMTIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIzNTciIHk9IjMwMiIgd2lkdGg9IjkwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDg4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzIycHg7IG1hcmdpbi1sZWZ0OiAzNThweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGI+V2FpdCB0aWxsIGRldmljZSByZWdpc3RlcjwvYj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjQ3MiIgeT0iMTcyIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTgycHg7IG1hcmdpbi1sZWZ0OiA0NzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+WWVzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzOTIiIHk9IjI2MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI3MnB4OyBtYXJnaW4tbGVmdDogMzkzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPk5vPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI4MDIiIHk9IjI2MiIgd2lkdGg9IjQwIiBoZWlnaHQ9IjIwIiBmaWxsPSJub25lIiBzdHJva2U9Im5vbmUiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDI3MnB4OyBtYXJnaW4tbGVmdDogODAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkZhaWw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9Ijg2OSIgeT0iMTgzIiB3aWR0aD0iNDAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDM4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTkzcHg7IG1hcmdpbi1sZWZ0OiA4NzBweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+U3VjY2VzczwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjUyIiB5PSIzMDIiIHdpZHRoPSI2MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMTJweDsgbWFyZ2luLWxlZnQ6IDI1M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5yZWdpc3RlcmVkPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" />


* **Trigger time for user attribute reporting:** 

   * **Cold start:**  The start\-up process when the user opens the app for the first time or opens it again after the app is completely closed

   * **New Profile:**  User actively calls the interface New Profile settings

   * **Device registration complete:**  SDK internal logic, get event reporting device identification

* Other processes: Similar to the Event reporting process, see the Event reporting process description above for details.
