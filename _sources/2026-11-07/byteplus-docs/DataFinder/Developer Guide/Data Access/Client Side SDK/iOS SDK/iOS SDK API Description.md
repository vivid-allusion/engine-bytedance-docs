---
title: "iOS SDK API Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/iOS_SDK_API_Description"
---

This article introduces a series of APIs provided by the iOS for you. You can call the corresponding API in combination with the event tracking planning for event tracking.

<span id="be192182"></span>
# Global API Description

<span id="d7a3a62d"></span>
## sharedTrackWithConfig


* **Function**: Initialize the singleton, call timing: 1. It must be called when the application is started, that is, in application: didFinishLaunchingWithOptions:; 2. It must be called in the main thread; 3. It must be called before other methods of the SDK are called.

* **Definition:**  + (void) sharedTrackWithConfig: (BDAutoTrackConfig \*) config

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |config |BDAutoTrackConfig |Yes | |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   BDAutoTrackConfig* config = [BDAutoTrackConfig configWithAppID:@"{{APPID}}" launchOptions:launchOptions];
   [BDAutoTrack sharedTrackWithConfig:config]; 
   ```
   

   `Swift`please refer to:

   ```Swift
   let config = BDAutoTrackConfig(appID: "{{APPID}}")
   BDAutoTrack.sharedTrack(with: config)
   ```
   


<span id="068d02d5"></span>
## sharedTrack


* **Function:**  If initialized, return the singleton initialized before; otherwise return nil. It doesn't initialize itself. Before calling this method, you must first call sharedTrackWithConfig.

* **Definition:**  + (instancetype) sharedTrack

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack sharedTrack];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.shared()
   ```
   


<span id="4c0d7a3c"></span>
## startTrack


* **Function:**  Start the SDK singleton, call timing: 1. It must be called when the application is started, that is, in application: didFinishLaunchingWithOptions:; 2. It must be called in the main thread.

* **Definition:**  + (void) gastTrack

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] startTrack];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.shared().start()
   ```
   


<span id="5ad8d06e"></span>
## trackWithConfig


* **Function:**  Initialize method, initialize an instance. The initialization interface can be called repeatedly and will return an instance. After returning, it is recommended to refer to this instance for easy use in the next report.

* **Definition:**  + (nullable instancetype) trackWithConfig: (BDAutoTrackConfig \*) config

* **Parameters:** 

   
   |Parameter name |type |Required |Explain |
   |---|---|---|---|
   |config |BDAutoTrackConfig |Yes | |
   

* **Example:** 

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
   


<span id="b1ced73c"></span>
## setRequestHostBlock


* **Function:**  Set a custom Host callback, set it once, no need to set it multiple times, if it is set multiple times, it will overwrite the previous initialization or the last set callback, if it is nil, it will empty the callback.

* **Definition:**  + (void) setRequestHostBlock: (nullable BDAutoTrackRequestHostBlock) requestHostBlock

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |requestHostBlock |BDAutoTrackRequestHostBlock |Yes | |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   BDAutoTrackRequestHostBlock block = ^NSString *(BDAutoTrackServiceVendor vendor, BDAutoTrackRequestURLType requestURLType) {
       return @"https://gator.volces.com";
   };
   [BDAutoTrack setRequestHostBlock:block];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setRequestHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
       return "https://gator.volces.com"
   }
   ```
   


<span id="99937276"></span>
## setCurrentUserUniqueID


* ### setCurrentUserUniqueID:uniqueID   <span id="setcurrentuseruniqueid-uniqueid"></span>

* **Function:**  Set user login status. Set user_unique_id value after initialization and the SDK will save it, so it only needs to be set when changes occur.

* **Definition:**  + (BOOL) setCurrentUserUniqueID: (nullable NSString \*) uniqueID

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |uniqueID |NSString |Yes, but nil | |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] setCurrentUserUniqueID:@"{{USER_UNIQUE_ID}}"]; 
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setCurrentUserUniqueID("{{USER_UNIQUE_ID}}")
   ```
   

* ### setCurrentUserUniqueID:uniqueID:type   <span id="setcurrentuseruniqueid-uniqueid-type"></span>

* **Function:**  Set user login status and user type. user_unique_id values and types are set after initialization, and the SDK saves them, so you only need to set them when changes occur.

* **Definition:**  + (BOOL) setCurrentUserUniqueID: (nullable NSString \*) uniqueID withType: (nullable NSString \*) type;

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |uniqueID |NSString |Yes, but nil | |
   |type |NSString |Yes, but nil | |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] setCurrentUserUniqueID:@"{{USER_UNIQUE_ID}}" withType:@"{{USER_UNIQUE_ID类型}}"]; 
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setCurrentUserUniqueID("{{USER_UNIQUE_ID}}", withType:"{{USER_UNIQUE_ID类型}}")
   ```
   


<span id="627f01f3"></span>
## clearUserUniqueID


* **Function:**  Exit the user login state.

* **Definition:**  + (void) clearUserUniqueID

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack clearUserUniqueID];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.clearUserUniqueID()
   ```
   


<span id="b2d173ef"></span>
## eventV3


* **Function:**  Report the event, it can only be called after initialization.

* **Definition:**  + (BOOL) eventV3: (NSString \*) event params: (nullable NSDictionary \*) params

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |event |NSString |Yes |Event name, cannot be nil or empty string |
   |params |NSDictionary |Yes, but nil |Event parameters. It can be empty or nil. If it is not empty, it needs to be serialized into json. **It is recommended that custom attributes do not exceed 50kb to avoid affecting the overall data reporting. If the data exceeds 50kb, all custom attributes will be discarded and adjusted to error messages**<br><br>Example of an adjusted error event:<br><br>{<br><br>"params":{<br><br>"description":"event param too large"<br><br>},<br><br>"Event": original event event name,<br><br>} |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   BDAutoTrackRequestHostBlock block = ^NSString *(BDAutoTrackServiceVendor vendor, BDAutoTrackRequestURLType requestURLType) {
       return @"https://gator.volces.com";
   };
   [BDAutoTrack setRequestHostBlock:block];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setRequestHostBlock {(vendor: BDAutoTrackServiceVendor, requestURLType:BDAutoTrackRequestURLType) -> String? in
       return "https://gator.volces.com"
   }
   ```
   


<span id="c939db2b"></span>
## setCustomHeaderValue


* **Role:**  Set custom public properties (non\-persistent).

* **Definition:**  + (void) setCustomHeaderValue: (nullable id) value forKey: (NSString \*) key

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |value |id |Yes, but nil |Custom report value, generally need to pass NSString or number, or nil |
   |key |NSString |Yes |Custom report key |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack setCustomHeaderValue:@"value_public" forKey:@"key_public"];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setCustomHeaderValue { () -> [String: Any] in
       return ["key_public":"value_public"]
   }
   ```
   


<span id="237d27fa"></span>
## removeCustomHeaderValueForKey


* **What:**  Removes custom public properties.

* **Definition:**  + (void) removeCustomHeaderValueForKey: (NSString \*) key

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |NSString |Yes |Custom report key |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack setCustomHeaderValue:@"value_public" forKey:@"key_public"];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setCustomHeaderValue { () -> [String: Any] in
       return ["key_public":"value_public"]
   }
   ```
   


<span id="59fc82b5"></span>
# BDAutoTrackConfig API Description

<span id="f8805806"></span>
## configWithAppID


* **Function:**  Get a config object according to the App ID.

* **Definition:**  + (instancetype) configWithAppID: (NSString \*) appID launchOptions: (nullable NSDictionary < id, id \> \*) launchOptions

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |appID |NSString |Yes |AppID obtained when registering the app |
   |launchOptions |NSDictionary<id,id\> |Yes, but nil |Application startup options, generally directly pass the `launchOptions`parameter of `application: didFinishLaunchingWithOptions:`to |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   BDAutoTrackConfig*config = [BDAutoTrackConfig configWithAppID:@"{{APPID}}" launchOptions:launchOptions];
   ```
   

   `Swift`please refer to:

   ```Swift
   let config = BDAutoTrackConfig(appID: "{{APPID}}", launchOptions:launchOptions)
   ```
   


<span id="0daa2e24"></span>
# AB test API Description

The SDK provides AB test capabilities and a range of methods: ABTestConfigValueForKey, ABTestConfigValueSyncForKey: key: defaultValue, abVidsSync, allAbVids, allABTestConfigsSync.

<span id="79c73ebc"></span>
## Open AB test

To use the function, you need to turn on the corresponding parameters when initializing the SDK settings:

`Objective-C`Please refer to:

```objectivec
//Open ab test, default to YES
config.abEnable = YES; 
```


`Swift`please refer to:

```Swift
//Open ab test, default to true
config.abEnable = true;
```


The SDK will send a shunt request to the shunt service after initialization. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Prerequisites for this step: The experiment and related parameters have been created according to the demand side of the experiment, see <a href="https://www.volcengine.com/docs/6287/65809#_4-1-%E5%88%9B%E5%BB%BA%E5%AE%9E%E9%AA%8C">Creating an Experiment </a>for details.</div>


* <div data-tips="true" data-tips-type="warning">Each time ABTestConfigValueForKey is called, an exposure event is reported by default abtest_exposure</div>



AB test configured value needs to be notified by the BDAutoTrackNotificationABTestSuccess before the correct value can be obtained, otherwise the value may not be obtained. Note: Set the callback before initialization and then call initialization.

Callback method when successfully pulling experimental parameters:

```objectivec
#import <RangersApplog/BDAutoTrack.h>
#import <RangersAppLog/BDAutoTrackNotifications.h>

//set the monitor
[[NSNotificationCenter defaultCenter] addObserver:self
                                        selector:@selector(onABTestSuccess:)
                                            name:BDAutoTrackNotificationABTestSuccess object:nil];

//Get experimental parameters after successful callback
- (void)onABTestSuccess:(NSNotification *)noti {
    NSLog(@"%@",noti.userInfo);
    //The meaning here is that after the callback is successful, you can start getting the value
    NSNumber newColor = [BDAutoTrack ABTestConfigValueForKey:@"btnColor" defaultValue:@(0)];
    if(newColor == 0){
        //A version branch
    } else {
        //B version branch
    }
}
```


<span id="fcc01dd4"></span>
## ABTestConfigValueForKey、ABTestConfigValueSyncForKey


* **Function:**  Get the configuration value of the AB test, which can only be called after initialization.

* **Definition:** 

   * (nullable id)ABTestConfigValueForKey:(NSString \*)key defaultValue:(nullable id)defaultValue

   * (nullable id)ABTestConfigValueSyncForKey:(NSString \*)key defaultValue:(nullable id)defaultValue

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |key |NSString |Yes |AB test configured key |
   |defaultValue |id |Yes, but nil |Default value, if not configured, or not enabled AB test returns the default value |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack ABTestConfigValueForKey:@"btnColor" defaultValue:@(0)];
   [BDAutoTrack ABTestConfigValueSyncForKey:@"btnColor" defaultValue:@(0)];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.abTestConfigValue(forKey: "btnColor", defaultValue: 0)
   BDAutoTrack.abTestConfigValueSync(forKey: "btnColor", defaultValue: 0)
   ```
   


<span id="b65f217f"></span>
## abVids、abVidsSync


* **Function:**  Get the exposed AB test configuration vids, which can only be called after initialization.

* **Definition:** 

   * (nullable NSString \*)abVids

   * (nullable NSString \*)abVidsSync

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack abVids];
   [BDAutoTrack abVidsSync];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.abVids()
   BDAutoTrack.abVidsSync()
   ```
   


<span id="d9a359e3"></span>
## allAbVids、allAbVidsSync


* **Function:**  Get all vids configured by AB test, which can only be called after initialization.

* **Definition:** 

   * (nullable NSString \*)allAbVids

   * (nullable NSString \*)allAbVidsSync

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack allAbVids];
   [BDAutoTrack allAbVidsSync];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.allAbVids()
   BDAutoTrack.allAbVidsSync()
   ```
   


<span id="77d4da3b"></span>
## allABTestConfigs、allABTestConfigsSync


* **Function:**  Get all the configuration items of the AB test, which can only be called after initialization.

* **Definition:** 

   * (nullable NSDictionary \*)allABTestConfigs

   * (nullable NSDictionary \*)allABTestConfigsSync

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack allABTestConfigs];
   [BDAutoTrack allABTestConfigsSync];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.allABTestConfigs()
   BDAutoTrack.allABTestConfigsSync()
   ```
   


<span id="4d051d99"></span>
## setExternalABVersion


* **Function:**  Set up additional vids. If you want to clear the last setting, pass nil directly; each setting will overwrite the last setting.

* **Definition:**  + (void) setExternalABVersion: (nullable NSString \*) versions

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |versions |NSString |Yes, but nil |Format such as @"1, 2, 3". It is separated by commas, with numbers between them. |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack setExternalABVersion:@"1111,2222,3333"];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.setExternalABVersion("1111,2222,3333")
   ```
   


<span id="f10bd60b"></span>
## pullABTestConfigs

This method requires 6.7.0 above version. Normal cold start, switching users, timing 10 minutes will automatically request AB test configuration.


* **Function:**  Manually trigger pull AB test configuration request. If you want to pull the experimental shunt results in real time, you can manually trigger the experimental configuration update through this method. Note: multiple calls within 10 seconds will only trigger one request. A BDAutoTrackNotificationABTestSuccess notification is sent when the acquisition is successful.

* **Definition:**  + (void) pullABTestConfigs

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack pullABTestConfigs];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.pullABTestConfigs()
   ```
   


<span id="86c82366"></span>
# User Attributes Features API Description

Provides the ability to set user properties and provides a series of methods: profileSet, profileSetOnce, profileUnset, profileIncrement, profileAppend.

<span id="2eb3011d"></span>
## profileSet


* **Function:**  Set user properties, overwrite if they exist, and create if they don't exist.

* **Definition:**  + (void) profileSet: (NSDictionary \*) profileDict

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profileDict |NSDictionary |Yes |Parameter dictionary values can only be of the following types: string, integer, floating\-point, string array |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   NSDictionary *profileDict = @{@"key": @("value")};
   [BDAutoTrack profileSet:profileDict];
   ```
   

   `Swift`please refer to:

   ```Swift
   let profileDict: [AnyHashable: Any] = [
       "key": "value"
   ]
   BDAutoTrack.profileSet(profileDict)
   ```
   


<span id="f0fba200"></span>
## profileSetOnce


* **Function:**  Set user properties, do not set if they exist, create if they do not exist, suitable for first\-time related user properties, such as first access time. Unlike the profileSet interface, if a profile has been successfully set through the profileSetOnce interface, it is invalid to call the profileSetOnce interface again on the profile.

* **Definition:**  + (void) profileSetOnce: (NSDictionary \*) profileDict

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profileDict |NSDictionary |Yes |Parameter dictionary values can only be of the following types: string, integer, floating\-point, string array |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   NSDictionary *profileDict = @{@"key_once": @("value_once")};
   [BDAutoTrack profileSetOnce:profileDict];
   ```
   

   `Swift`please refer to:

   ```Swift
   let profileDict: [AnyHashable: Any] = [
       "key_once": "value_once"
   ]
   BDAutoTrack.profileSetOnce(profileDict)
   ```
   


<span id="958365b9"></span>
## profileIncrement


* **Function:**  Set the properties of the numeric type to accumulate.

* **Definition:**  + (void) profileIncrement: (NSDictionary < NSString \*, NSNumber \* \> \*) profileDict

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profileDict |NSDictionary |Yes |Can only increment integers (can be negative integers). If a floating\-point number is passed in, the SDK will ignore it. |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack profileIncrement:@{@"key": @(1)}];
   ```
   

   `Swift`please refer to:

   ```Swift
   let profileDict: [AnyHashable: Number] = [
       "key": 1
   ]
   BDAutoTrack.profileIncrement(profileDict)
   ```
   


<span id="8dc1f600"></span>
## profileAppend


* **Function:**  Set the user properties of the List type, which can be continuously added to the List.

* **Definition:**  + (void) profileAppend: (NSDictionary \*) profileDict

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profileDict |NSDictionary |Yes |The value of the parameter dictionary can only be a string or a string array. |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack profileAppend:@{
       @"key": @[@"value_append"]
   }];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.profileAppend([["key"]:["value_append"]])
   ```
   


<span id="b3c52257"></span>
## profileUnset


* **Function:**  Delete the user's attributes.

* **Definition:**  + (void) profileUnset: (NSString \*) profileName

* **Parameters:** 

   
   |Parameter name |Type |Required |Explain |
   |---|---|---|---|
   |profileName |NSString |Yes |The name of the profile to unset |
   

* **Example:** 

   `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack profileUnset:@"key"];
   ```
   

   `Swift`please refer to:

   ```Swift
   BDAutoTrack.profileUnset("key")
   ```
   


<span id="3a47e9f2"></span>
# Element Exposure Function API Description

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is supported after 6.10.0 +.</div>


<div data-tips="true" data-tips-type="tip">When a component appears within the visible range of the screen, an exposure event is automatically triggered.</div>


<span id="02c4efa8"></span>
## Enable element exposure

<span id="655fb8aa"></span>
### **import module**

Introduce Exposure submodules, subspecs add `Exposure`

```Ruby
pod 'RangersAppLog', 'SDK-VERSION', 
    :subspecs => [
        # ...
        'Exposure'
    ]
```


<span id="ac55974d"></span>
### **header file import**

```objectivec
//introduce header files for related functional settings
//integrates by modular @import RangersAppLog;
#import <RangersAppLog/BDAutoTrackExposure.h>
```


<span id="537b0a93"></span>
### **enable function**

To use the function, you need to turn on the corresponding parameters when initializing the SDK settings:

`Objective-C`Please refer to:

```objectivec
//Global function control switch YES | NO. Default is on
config.exposureEnabled = YES; 
```


`Swift`please refer to:

```Swift
//Global function control switch YES | NO. Default is on
config.exposureEnabled = true;
```


<span id="bc5c6959"></span>
## Exposure Configuration Settings

Sets the minimum area ratio of the main screen view that the component triggers exposure.

Default is:


* 0: Indicates that 1 pixel is used to enter the screen to trigger exposure.

* (0~ 1): Floating\-point numbers indicate that 0~ 100% will trigger exposure.


`Objective-C`Please refer to:

```objectivec
//BDAutoTrackConfig global settings, component-independent configuration can be set in BDViewExposureData
[config.exposureConfig areaRatio:0.5];
```


`Swift`please refer to:

```Swift
config.exposureConfig.areaRatio(0.5)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function only determines exposure based on the main window, and does not yet support the calculation of sub\-view occlusion.</div>


<span id="a01a8bf8"></span>
## Monitoring component exposure

Exposure monitoring of component instances.

`Objective-C`Please refer to:

```objectivec
BDViewExposureData *opt = [BDViewExposureData new];
opt.eventName = @"view_did_exposure"; //If not set, event tracking takes bav2b_exposure
opt.properties = @{};   //user-defined parameters
opt.config = [[BDViewExposureConfig defaultConfig] areaRatio:0.5];

//Open the detection of the view
//view user's view object instance
//opt event tracking data and configuration
[[BDAutoTrack sharedTrack] observeViewExposure:YOUR_VIEW
                                      withData:opt];
                                      
//Stop the detection of the view
[[BDAutoTrack sharedTrack] disposeViewExposure:YOUR_VIEW];
```


`Swift`please refer to:

```Swift
let opt = BDViewExposureData()
opt.eventName = "view_did_exposure"
opt.properties = [:]
opt.config = BDViewExposureConfig.default().areaRatio(0.5)
BDAutoTrack.shared().observeViewExposure(YOUR_VIEW, with: opt)

BDAutoTrack.shared().disposeViewExposure(YOUR_VIEW)
```


<span id="b80713fb"></span>
## function debugging

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This switch is only used in the debugging stage, please do not turn it on in the online package.</div>


After turning on the visual debugging function, debug the component exposure function.


* Open the component that monitors exposure and generate a red border.

* The component triggers exposure, generating a translucent floating layer.


`Objective-C`Please refer to:

```objectivec
[config.exposureConfig enableVisualDiagnosis:YES];
```


`Swift`please refer to:

```Swift
config.exposureConfig.enableVisualDiagnosis(true)
```
