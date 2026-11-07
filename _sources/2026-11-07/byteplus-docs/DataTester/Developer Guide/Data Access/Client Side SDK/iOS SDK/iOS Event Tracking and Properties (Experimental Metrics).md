---
title: "iOS Event Tracking and Properties (Experimental Metrics)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/iOS-Event-Tracking-and-Properties-Experimental-Metrics"
---

<span id="5127a779"></span>
# 1. Users and user attributes

Attention:

> Before reporting events and attributes, read the data format documentation: [Supported Data Formats (Custom Events/Properties)](https://docs.byteplus.com/docs/DataTester/Supported-Data-Formats-Custom-Events-Properties).


<span id="4c74b13c"></span>
## 1.1 Login state change call

> Versions after the 6.13.0 allow calls prior to gastTrack to set the initialized login state.

> 6.13.0 previous versions only took effect after the SDK was launched.


<span id="c85f5f21"></span>
### 1.1.1 Account login

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

`Objective-C`Please refer to:

```objectivec
#import <RangersAppLog/RangersAppLog.h>
// Set the ID of your account system and ensure its uniqueness
[BDAutoTrack setCurrentUserUniqueID:@"{{USER_UNIQUE_ID}}"];
```


`Swift`please refer to:

```swift
BDAutoTrack.setCurrentUserUniqueID("{{USER_UNIQUE_ID}}")
```


If you have obtained a settable uuid when initializing the SDK, such as a logged\-in user, please call the settings during initialization. After initialization, there is no need to call repeated settings again.

`Objective-C`Please refer to:

```objectivec
// set uuid when initializing
config.initialUserUniqueID = @"{{USER_UNIQUE_ID}}";
```


`Swift`please refer to:

```swift
// set uuid when initializing
config.initialUserUniqueID = "{{USER_UNIQUE_ID}}"
```


<span id="8abd9c6d"></span>
### 1.1.2 Account Logout

Called when the account is logged out.

`Objective-C`Please refer to:

```objectivec
[BDAutoTrack clearUserUniqueID];
```


`Swift`please refer to:

```swift
BDAutoTrack.clearUserUniqueID();
```


<span id="3225a5e6"></span>
## 1.2 Setting user properties

<span id="33d12881"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.

`Objective-C`Please refer to:

```objectivec
// Example: set user property with property name key and property value value
NSDictionary *profileDict = @{@"key": @("value")};
[BDAutoTrack profileSet:profileDict];
```


`Swift`please refer to:

```swift
// Example: set user property with property name key and property value value
let profileDict: [AnyHashable: Any] = [
    "key": "value"
]
BDAutoTrack.profileSet(profileDict)
```


<span id="8d814bf4"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

`Objective-C`Please refer to:

```objectivec
// Example: Set the user property with the property name key_once and the property value value_once
NSDictionary *profileDict = @{@"key_once": @("value_once")};
[BDAutoTrack profileSetOnce:profileDict];
```


`Swift`please refer to:

```swift
// Example: Set the user property with the property name key_once and the property value value_once
let profileDict: [AnyHashable: Any] = [
    "key_once": "value_once"
]
BDAutoTrack.profileSetOnce(profileDict)
```


<span id="4432324f"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.

`Objective-C`Please refer to:

```objectivec
// Example: Set the user property with the property name key and the property value 1
[BDAutoTrack profileIncrement:@{@"key": @(1)}];
```


`Swift`please refer to:

```swift
// Example: Set the user property with the property name key and the property value 1
let profileDict: [AnyHashable: Number] = [
    "key": 1
]
BDAutoTrack.profileIncrement(profileDict)
```


<span id="47ff05f3"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.

`Objective-C`Please refer to:

```objectivec
// Example: Set a user property with the property name 'key'. Originally, there was a property value. Now the property value has been added as 'value_append’.
[BDAutoTrack profileAppend:@{
    @"key": @[@"value_append"]
}];
```


`Swift`please refer to:

```swift
// Example: Set a user property with the property name 'key'. Originally, there was a property value. Now the property value has been added as 'value_append’.
BDAutoTrack.profileAppend([["key"]:["value_append"]])
```


<span id="a3fef7bc"></span>
### 1.2.5 profileUnset

Delete the user's attributes.

`Objective-C`Please refer to:

```objectivec
// Example: delete user property, property name is key
[BDAutoTrack profileUnset:@"key"];
```


`Swift`please refer to:

```swift
// Example: delete user property, property name is key
BDAutoTrack.profileUnset("key")
```


<span id="96ce81ab"></span>
# 2. Obtain experimental parameters

Tester usually sends a shunt request to the shunt service after the SDK is initialized. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.


* Please note the prerequisite for this step: the experiment and associated parameters have been created according to the demand side of the experiment.

* Note that each time ABTestConfigValueForKey is called, an exposure event is reported by default abtest_exposure


The value of ABTest needs to be notified by the BDAutoTrackNotificationABTestSuccess to get the correct value, otherwise the value may not be obtained. Note: Set the callback before initialization and then call initialization.

Callback method when successfully pulling experimental parameters:

```objectivec
#import <RangersApplog/BDAutoTrack.h>
#import <RangersAppLog/BDAutoTrackNotifications.h>

// Set monitor
[[NSNotificationCenter defaultCenter] addObserver:self
                                        selector:@selector(onABTestSuccess:) 
                                            name:BDAutoTrackNotificationABTestSuccess object:nil];
                                            

// Get experimental parameters after recalling success
- (void)onABTestSuccess:(NSNotification *)noti {
    NSLog(@"%@",noti.userInfo);    
    // after recalling success, you can start to get value
    NSNumber newColor = [BDAutoTrack ABTestConfigValueForKey:@"btnColor" defaultValue:@(0)];
    if(newColor == 0){
        // A version branch
    } else {
        // B version branch
    }
}
objective-c
```


Sync method, can block waiting for local cache file read, this method is designed to facilitate business immediately after initialization to obtain the cached AB test data, may take a long time.

```objectivec
/*! @abstract If local cache is loaded, then it is same as `ABTestConfigValueForKey:defaultValue:`. If local cache is unloaded, it will block and wait for its loading to complete.
 @discussion The local cache is usually loaded within 30-100ms after initialization.
 */
- (nullable id)ABTestConfigValueSyncForKey:(NSString *)key defaultValue:(nullable id)defaultValue;
- (nullable NSString *)abVidsSync;
- (nullable NSString *)allAbVids;
- (nullable NSDictionary *)allABTestConfigsSync;
```


If you want to pull the experimental shunt results in real time, you can manually trigger the experimental configuration update through the pullABTestConfigs method  **(multiple calls within 10 seconds will only trigger one request).** 

```plaintext
[BDAutoTrack pullABTestConfigs];//This feature requires version 6.7.0 or above
// After successful acquisition, it will be sent BDAutoTrackNotificationABTestSuccess notification
// A BDAutoTrackNotificationABTestSuccess notification will be received 
// if the test configs are correctly pulled
```


<span id="0f3e7fba"></span>
# 3. Events and event attributes (reporting experimental metrics)

<span id="ca5fd230"></span>
## 3.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:

`Objective-C`Please refer to:

```objectivec
// Example: reporting event, which does not include property
// Placed in the corresponding position of business logic
[BDAutoTrack eventV3:@"event" params: nil];
```


`Swift`please refer to:

```swift
// Example: reporting event, which does not include property
// Placed in the corresponding position of business logic
BDAutoTrack.eventV3("event", params: nil)
```


Code event tracking for reporting events and corresponding properties, as follows:

`Objective-C`Please refer to:

```objectivec
// Example: reporting event, which includes teo properties
//      a string type property, with property name key_string, and property value value_string
//      a int type property, with property name key_int, and property value 10
// Placed in the corresponding position of business logic
[BDAutoTrack eventV3:@"event" 
             params:@{@"key_string":@"value_string",
                      @"key_int": @(10)}];
```


`Swift`please refer to:

```swift
// Example: reporting event, which includes two properties
//      a string type property, with property name key_string, and property value value_string
//      a int type property, with property name key_int, and property value 10
// Placed in the corresponding position of business logic
BDAutoTrack.eventV3("event", params: ["key_string": "value_string",
                                      "key_int": 10])
```


<span id="f762fff9"></span>
## 3.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="8927e459"></span>
### 3.2.1 set public properties

`Objective-C`Please refer to:

```objectivec
/* 
 * Example: set custom public property with property name key_public and property value value_public
 * Please note that about custom “public property”：
 * 1. The reporting mechanism is to submit with each log sending, and the default log sending frequency is 1 minute.
 *    So if you continuously modify custom public properties within one minute, the last modification before sending the log shall prevail; 
 * 2. It is not recommended to make frequent modifications, such as modifying once per second.
 */
[BDAutoTrack setCustomHeaderValue:@"value_public" forKey:@"key_public"];
```


`Swift` please refer to:

```swift
/* 
 * Example: set custom public property with property name key_public and  property value value_public
 * Please note that about custom “public property”：
 * 1. The reporting mechanism is to submit with each log sending, and the default log sending frequency is 1 minute.
 *    So if you continuously modify custom public properties within one minute, the last modification before sending the log shall prevail; 
 * 2. It is not recommended to make frequent modifications, such as modifying once per second.
 */
BDAutoTrack.setCustomHeaderValue { () -> [String : Any] in
            return ["key_public":"value_public"]
}
```


<span id="a9f7f4be"></span>
### 3.2.2 Remove Public Attributes

`Objective-C`Please refer to:

```objectivec
// Example: Removing a public property named key_public
[BDAutoTrack removeCustomHeaderValueForKey:@"key_public"];
```


`Swift`please refer to:

```swift
// Example: Removing a public property named key_public
BDAutoTrack.removeCustomHeaderValueForKey("key_public");
```


<span id="5c7ec879"></span>
# 4. Obtain platform ID and notification

<span id="23851255"></span>
## 4.1 Obtaining the platform generated ID

`Objective-C`Please refer to:

```objectivec
#import <RangersApplog/BDAutoTrackNotifications.h>
// set monitoring before Initializing sdk
 [[NSNotificationCenter defaultCenter] addObserver:self
                                            selector:@selector(onRegisterSuccess:)
                                                name:BDAutoTrackNotificationRegisterSuccess object:nil];
//SDK initializing code
//and set recalling after SDK Initialization
- (void)onRegisterSuccess:(NSNotification *)noti  {
    // Please start retrieving after 3 seconds of initialization completion, otherwise it may return empty
    NSString *dids = [noti.userInfo objectForKey:kBDAutoTrackNotificationRangersDeviceID];
    NSString *ssids = [noti.userInfo objectForKey:kBDAutoTrackNotificationSSID]; 
    NSLog(@"onRegisterSuccess.dids：%@", dids); // get device bddid
    NSLog(@"onRegisterSuccess.ssids：%@", ssids); // get SSID
}
```


`Swift`please refer to:

```swift
// Please start retrieving after 3 seconds of initialization completion, otherwise it may return empty
NotificationCenter.default.addObserver(self, selector: #selector(onRegisterSuccess), name: NSNotification.Name(rawValue: BDAutoTrackNotificationRegisterSuccess), object: nil)

func onRegisterSuccess(noti: Notification) {
    let did = noti.userInfo[kBDAutoTrackNotificationRangersDeviceID]
    let ssid = noti.userInfo[kBDAutoTrackNotificationSSID]
    print("onRegisterSuccess.dids：\(did)")
    print("onRegisterSuccess.ssids：\(ssid)")
}
```


<span id="e7f03ae5"></span>
## 4.2 Obtaining the SDK version number

`Objective-C`Please refer to:

```objectivec
// SDK version format is X.X.X
[BDAutoTrack sdkVersion]
```


`Swift`please refer to:

```swift
BDAutoTrack.sdkVersion()
```


<span id="b718552a"></span>
## 4.3 Obtaining the Experimental Version ID

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">AB test must call the API to obtain experimental parameters (see the <strong>++Getting Experimental Parameters ++</strong>section for details). You can use this API to obtain the Version IDs (vids) of all user exposures or hit experiments, which do not report abtest_exposure exposures.</div>


```JSON
[BDAutoTrack.sharedTrack abExposedVids]; 
```


<span id="1ec024dd"></span>
## 4.4 Obtaining various notifications

The SDK provides methods for obtaining various notifications. Each notification is described in the `BDAutoTrackNotifications h`header file.

```objectivec
// SDK registration successful notification
BDAutoTrackNotificationRegisterSuccess
//SDK registration failed notification
BDAutoTrackNotificationRegisterFailure
// activation successful notification 
BDAutoTrackNotificationActiveSuccess
// SDK ABTest configuration pulls successful notification
BDAutoTrackNotificationABTestSuccess
// Notification when SDK ABTestVid changes 
BDAutoTrackNotificationABTestVidsChanged
```


<span id="5703b790"></span>
# 5. Default public attribute fields

The SDK collects the following information by default and makes it public to users.


|Field name |Field type |Parameter name |
|---|---|---|
|os |string |Equipment system, the corresponding product attributes are os_name. |
|os_version |string |operating system version |
|app_version |string |App version |
|app_version_minor |string |Second version number, App four\-digit version number, set [OKApplicationInfo sharedInstance] .buildVersion = @"1.2.3.4"; |
|channel |string |Download channel (can be overwritten after setting), the corresponding product attribute is app_channel. |
|device_model |string |Equipment model |
|region |string |Operating system country |
|language |string |system language |
|sdk_version |string |SDK version |
|timezone |int |Time zone, such as 8 |
|tz_offset |int |Time zone offset, corresponding to an in\-product attribute of tz_offset, for example 28800. |
|tz_name |string |Time zone name, such as Asia/Shanghai. |
|carrier |string |operator |
|resolution |string |resolution |
|device_brand |string |Equipment brand |
|access |string |network type |


<span id="cf836abf"></span>
# 6. Game tracking event reporting interface

If you have ever used BytePlus' game growth analysis product (which has been removed from the shelves), in order to improve your event tracking efficiency, the SDK provides a built\-in interface, you only need to pass in the specified parameters according to the prompts.

```objectivec
#import "BDAutoTrack+GameTrack.h" //Please introduce the correct header file first

/**
 Advertising button Click: gt_ad_button_click
 ad_type           string  Advertising types: incentive videos, screen inserts, banners, etc., directly using Chinese characters or English for identification
 ad_position_type  string  Type of advertising placement: Access by category provided
 ad_position       string  Advertising placements: revival, doubling, trial buff、 Reward items, new items, CD reductions, etc. can be directly identified using Chinese characters or English
 Trigger condition: When the user clicks on the button of each advertisement slot in the app.
 */
- (void)adButtonClickEventWithADType:(NSString *)adType
                        positionType:(NSString *)positionType
                            position:(NSString *)position
                         otherParams:(nullable NSDictionary *)otherParams;

/**
 Advertisement begins to display: gt_ad_show
ad_type            string  Advertising types: incentive videos, screen inserts, banners, etc., directly using Chinese characters or English for identification
 ad_position_type  string  Type of advertising placement: Access by category provided
 ad_position       string  Advertising placements: revival, doubling, trial buff、 Reward items, new items, CD reductions, etc. can be directly identified using Chinese characters or English
 Triggering condition: When the user clicks and watches the advertisement. The CSJ advertisement has a callback, which can be obtained directly.
 */
- (void)adShowEventWithADType:(NSString *)adType
                 positionType:(NSString *)positionType
                     position:(NSString *)position
                  otherParams:(nullable NSDictionary *)otherParams;

/**
 advertisement display ends: gt_ad_show_end
 ad_type           string  Advertising types: incentive videos, screen inserts, banners, etc., directly using Chinese characters or English for identification
 ad_position_type  string  Type of advertising placement: Access by category provided
 ad_position       string  Advertising placements: revival, doubling, trial buff、 Reward items, new items, CD reductions, etc. can be directly identified using Chinese characters or English
 result            string  Advertisement viewing results: skip, success, failure, etc., marked in English, skip marked as skip, success marked as success, failure marked as fail
 Triggering condition: When the user finishes watching the advertisement.
 */
- (void)adShowEndEventWithADType:(NSString *)adType
                    positionType:(NSString *)positionType
                        position:(NSString *)position
                          result:(NSString *)result
                     otherParams:(nullable NSDictionary *)otherParams;

/**
 (Overall Level) Upgrade and Experience:gt_levelup
 lev         int Current player level
 get_exp     int gain experience
 method      string  Ways to gain experience: Successfully passing levels, guiding completion, receiving rewards, etc., marked with Chinese characters or English
 aflev       int If the user's experience does not result in an upgrade, then lev=aflev; if it results in an upgrade, then lev<aflev
 Triggering condition: When the user gains experience or changes their level.
 */
- (void)levelUpEventWithLevel:(NSInteger)level
                          exp:(NSInteger)exp
                       method:(NSString *)method
                   afterLevel:(NSInteger)afterLevel
                  otherParams:(nullable NSDictionary *)otherParams;

/**
 Start gameplay: gt_start_play
 ectype_name  string  Label the level name based on the nature and gameplay of the challenge
 Trigger condition: When the user starts playing.
 */
- (void)startPlayEventWithName:(NSString *)ecTypeName
                   otherParams:(nullable NSDictionary *)otherParams;

/**
 Ending gameplay: gt_end_play
 ectype_name string  Label the level name based on the nature and gameplay of the challenge
 result      string  The results of the gameplay: incomplete, successful, failed, etc., are marked in English Incomplete is marked as incomplete, successful is marked as successful, and failed is marked as fail
 duration    int Time consumption, in seconds
 Trigger condition: When the user ends the gameplay, it includes quitting midway, completing but failing, and completing and succeeding.
 */
- (void)endPlayEventWithName:(NSString *)ecTypeName
                      result:(NSString *)result
                     duration:(NSInteger)duration
                  otherParams:(nullable NSDictionary *)otherParams;

/**
 Get game coins:gt_get_coins
 coin_type   string    Currency types: Yuanbao, Tieyuan, Gold Coin, Silver Coin, etc., identified using text or English
 method      string    Ways to obtain: Watch motivational videos, successfully pass levels, receive activity rewards, etc., and use text or English to mark them
 coin_num    int       Obtain quantity
 Trigger condition: When the user obtains game currency, resulting in an increase in game currency
 */
- (void)getCoinsEventWitType:(NSString *)coinType
                      method:(NSString *)method
                  coinNumber:(NSInteger)number
                 otherParams:(nullable NSDictionary *)otherParams;

/**
 Consuming game coins:gt_cost_coins
 coin_type   string    Currency types: Yuanbao, Tieyuan, Gold Coin, Silver Coin, etc., identified using text or English
 method      string    Consumption methods: resurrection, purchasing props, unlocking levels, etc., marked with text or English
 coin_num    int       Consumption quantity
 Trigger condition: When the user consumes game currency, resulting in a decrease in game currency.
 */
- (void)costCoinsEventWitType:(NSString *)coinType
                       method:(NSString *)method
                   coinNumber:(NSInteger)number
                  otherParams:(nullable NSDictionary *)otherParams;

/**
 Internal purchase recharge related:purchase
 content_type    string  Internal purchase recharge content type
 content_name    string  Internal purchase recharge content name
 content_id      string  Internal purchase recharge content id
 content_num     int     Internal purchase recharge content quantity
 payment_channel string  Payment channels: such as Alipay, WeChat, etc.
 currency        string  Payment currency type
 is_success      string  Is the payment successful
 currency_amount int     Payment amount, the unit is Yuan
 Trigger condition: When the user completes the internal purchase recharge and obtains the corresponding in-game currency and items
 */
- (void)purchaseEventWithContentType:(NSString *)contentType
                         contentName:(NSString *)contentName
                           contentID:(NSString *)contentID
                          contentNum:(NSInteger)contentNum
                             channel:(NSString *)channel
                            currency:(NSString *)currency
                           isSuccess:(NSString *)isSuccess
                      currencyAmount:(NSInteger)currencyAmount
                         otherParams:(nullable NSDictionary *)otherParams;

/**
 Initialization information: gt_init_info
 lev         int     player level
 coin_type   string  Types of currency obtained
 coin_left   int     The remaining amount of currency on the user's body
 role_id     string  player role id-cp side
 Trigger condition: The user starts the game and reports upon completion of initialization
 */
- (void)gameInitInfoEventWithLevel:(NSInteger)level
                          coinType:(NSString *)coinType
                          coinLeft:(NSInteger)coinLeft
                       otherParams:(nullable NSDictionary *)otherParams;
```


<span id="3560908f"></span>
# 7. View exposure event capture

> This feature is supported after 6.10.0 +.


When a component appears within the visible range of the screen, an exposure event is automatically triggered.

<span id="f4fb5b5f"></span>
## 7.1 Component access

<span id="eb4eb399"></span>
#### 7.1.1 CocoaPod introduces `Exposure`

> File\-mode integration requires the introduction of corresponding library files.


```objectivec
pod 'RangersAppLog', 'SDK_VERSION',
    :subspecs => [
    ...
    'Exposure',
    ...
]
```


<span id="053b9e9a"></span>
#### 7.1.2 header file reference

```objectivec
//Introduce header files for related functional settings
//modular method integrate @import RangersAppLog;
#import <RangersAppLog/BDAutoTrackExposure.h>
```


<span id="fe1c7653"></span>
## 7.2 Function switch


* `Objective-C`Please refer to:

   ```objectivec
   config.exposureEnabled = YES; // global feature control switch YES|NO. The default is YES.
   ```
   

* `Swift`please refer to:

   ```swift
   config.exposureEnabled = true
   ```
   


<span id="33464f78"></span>
## 7.3 Exposure Configuration Settings

Sets the minimum area ratio of the main screen view that the component triggers exposure.

Default is:


* 0: Indicates that 1 pixel is used to enter the screen to trigger exposure.

* (0~ 1): Floating\-point numbers indicate that 0~ 100% will trigger exposure.


`Objective-C`Please refer to:

```objectivec
// BDAutoTrackConfig global setting. For independent configuration of components, set in BDViewExposureData.
[config.exposureConfig areaRatio:0.5];
```


`Swift`please refer to:

```swift
config.exposureConfig.areaRatio(0.5)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function only determines exposure based on the main window, and does not yet support the calculation of sub\-view occlusion.</div>


<span id="2fa71470"></span>
## 7.4 Monitoring component exposure

Exposure monitoring of component instances.


* `Objective-C`Please refer to:

   ```objectivec
   BDViewExposureData *opt = [BDViewExposureData new];
   opt.eventName = @"view_did_exposure"; // If not configured, for event tracking, use bav2b_exposure
   opt.properties = @{};   // user custom parameter
   opt.config = [[BDViewExposureConfig defaultConfig] areaRatio:0.5];
   
   // Enable detection for views
   // view user's view object instance
   // opt event tracking and configuration
   [[BDAutoTrack sharedTrack] observeViewExposure:YOUR_VIEW
                                         withData:opt];
                                         
   // stop detecting views  
   [[BDAutoTrack sharedTrack] disposeViewExposure:YOUR_VIEW];
   ```
   

* `Swift`please refer to:

   ```swift
   let opt = BDViewExposureData()
   opt.eventName = "view_did_exposure"
   opt.properties = [:]
   opt.config = BDViewExposureConfig.default().areaRatio(0.5)
   BDAutoTrack.shared().observeViewExposure(YOUR_VIEW, with: opt)
   
   BDAutoTrack.shared().disposeViewExposure(YOUR_VIEW)
   ```
   


<span id="fe35c611"></span>
## 7.5 Functional debugging

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

```swift
config.exposureConfig.enableVisualDiagnosis(true)
```


<span id="b4bba5a7"></span>
# 8. Full event tracking

After turning on the full event tracking event collection switch, page events and View click events will be collected by default.

<span id="b44baff1"></span>
## 8.1 Function enabled

According to the differences in integration methods, the corresponding subspec module or static library file is introduced into the project.


* `Objective-C`Please refer to:

   ```objectivec
   // enable full event tracking collection, the default is YES
   config.autoTrackEnabled = YES;
   // enable WebView full event tracking collection, the default is YES
   config.H5AutoTrackEnabled = YES;
   ```
   

* `Swift`please refer to:

   ```swift
   config.autoTrackEnabled = true
   config.H5AutoTrackEnabled = true
   ```
   


<span id="9730db27"></span>
### 8.1.1 Function switch based on event type

> This section is supported in version 6.11.0 +.


Configuration of event types that allow full event tracking, as defined in `< BDCommonEnumDefine.h >`.


* BDAutoTrackDataTypePage \- Page View Events

* BDAutoTrackDataTypeClick \- user click event

* BDAutoTrackDataTypePageLeave \- End of Page View Event


`Objective-C`Please refer to:

```objectivec
config.autoTrackEventType = BDAutoTrackDataTypeAll;
```


`Swift`please refer to:

```swift
config.autoTrackEventType = BDAutoTrackDataType.all
```


<span id="bbb57dbd"></span>
## 8.2 Custom Page View Event Properties

> Please set the parameter value in the init method, otherwise the parameter value may be empty when the page view event is first triggered.


Customize the parameters of the page view event through the `UIViewController`extension API.

```objectivec
/*! @abstract manually configured PageTitle
 @discussion If configured, collect when page switches
 @discussion If configured, the View in this VC will be collected when clicked
 */
@property (nonatomic, copy) NSString *bdAutoTrackPageTitle;
 /*! @abstract manually configured PageID
 @discussion If configured, collect when page switches
 @discussion If configured, the View in this VC will be collected when clicked
 */
@property (nonatomic, copy) NSString *bdAutoTrackPageID;
 /*! @abstract manually configured PagePath
 @discussion If configured, collect when page switches
 @discussion If configured, the View in this VC will be collected when clicked
 */
@property (nonatomic, copy) NSString *bdAutoTrackPagePath;
 /*! @abstract manually configured extra information
 @discussion If configured, collect when page switches
 @discussion If configured, the View in this VC will be collected when clicked
 */
@property (nonatomic, copy) NSDictionary<NSString*, NSString *> *bdAutoTrackExtraInfos;
 /*! @abstract Custom collecting attribute, the same key will cover  params that are default collected
 @discussion If configured, collect when page switches
 @discussion If configured, the View in this VC will be collected when clicked
 */
@property (nonatomic, copy) NSDictionary<NSString*, NSObject *> *bdAutoTrackPageProperties;
```


<span id="0ebff333"></span>
## 8.3 Custom Click Event Properties

Customize the parameters of the click event through `UIView`and `UIBarButtonItem`extension APIs.

```objectivec
/*! @abstract this one corresponds to newly added element_id field, bdAutoTrackViewID corresponds to element_manual_key field
 @discussion If configured, will be collected when being clicked
 */
@property (nonatomic, copy) NSString *bdAutoTrackElementID;
 
/*! @abstract manually configured ViewID
 @discussion If configured, will be collected when being clicked,and can uniquely identify this View
 */
@property (nonatomic, copy) NSString *bdAutoTrackViewID;
 
/*! @abstract manually configured ViewContent
 @discussionIf configured, will be collected when being clicked
 */
@property (nonatomic, copy) NSString *bdAutoTrackViewContent;
 
/*! @abstract manually configured extra information
 @discussion If configured, will be collected when being clicked
 */
@property (nonatomic, copy) NSDictionary<NSString*, NSString *> *bdAutoTrackExtraInfos;
 
/*! @abstract Custom collecting attribute, the same key will cover  params that are default collected
 @discussion If configured, will be collected when being clicked
 */
@property (nonatomic, copy) NSDictionary<NSString*, NSObject *> *bdAutoTrackViewProperties;
 
/*! @abstract custom collecting developing
 @discussion If set to YES, the buried point will be ignored when clicked
 */
@property (nonatomic, assign) BOOL bdAutoTrackIgnoreClick;
```


<span id="0eac49cd"></span>
## 8.4 Ignoring specific full event tracking events

<span id="213a51b2"></span>
### 8.4.1 Ignore specific page view events

```objectivec
/*! @abstract Ignore browsing tracking automatically collected in UIViewController
    @discussion Ignoring the scope as its own class does not affect inheritance relationships, for example: BViewController inherited from AViewController. If all ignored, then passing @[[AViewController class],[BViewController class]] is required.
    @param controllerClasses pass in the class name that needs to be ignored @[[TestViewController class], [UserViewController class]]
 */
- (void)ignoreAutoTrackPage:(NSArray<Class> *)controllerClasses;
```



* `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] ignoreAutoTrackPage:@[YOUR_ViewController.class]];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.shared().ignorePage([YOUR_ViewController.classForCoder()])
   ```
   


<span id="53fd4e7a"></span>
### 8.4.2 Ignore specific control click events

```objectivec
/*! @abstract Ignore the click event tracking automatically collected in the control
    @discussion Ignore the scope as its own class
    @param viewClasses pass in the class name that needs to be ignored @[[AButton class], [ALabel class]]
 */
- (void)ignoreAutoTrackClick:(NSArray<Class> *)viewClasses;
```



* `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] ignoreAutoTrackClick:@[YOUR_VIEW.class]];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.shared().ignoreClick([YOUR_VIEW.classForCoder()])
   ```
   


<span id="4660a4b1"></span>
## 8.5 Manually trigger full event tracking event collection

<span id="cfc3e79b"></span>
### 8.5.1 Manually trigger page view events

```objectivec
/*!
 *  @abstract Code triggers page browsing event tracking reporting
 *  @param controller Can pass UIViewController and objects that implement BDAutoTrackable protocol
 *  @result Whether it is successful
 */
- (BOOL)trackPage:(id<BDAutoTrackable>)controller;

/*!
 *  @abstract Code triggers page browsing event tracking reporting
 *  @param controller can pass UIViewController
 *  @param params user custom parameter, performing [NSJSONSerialization isValidJSONObject:] verification
 *  @result Whether it is successful
 */
- (BOOL)trackPage:(id)controller withParameters:(nullable NSDictionary<NSString *,id> *)params;
```



* `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] trackPage:YOUR_VIEWCONTROLLER_INSTANCE];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.shared().trackPage(YOUR_VIEWCONTROLLER_INSTANCE)
   ```
   


<span id="d88bdfd4"></span>
### 8.5.2 Manually trigger click events

```objectivec
/*!
 *  @abstract Code triggers click event tracking reporting
 *  @param view Can pass UIView and objects that implement BDAutoTrackable protocol
 *  @result Whether it is successful
 */
- (BOOL)trackClick:(id<BDAutoTrackable>)view;
 
/*!
 *  @abstract Code triggers click event tracking reporting
 *  @param view Can pass UIView and objects that implement BDAutoTrackable protocol
 *  @param params user custom parameter, performing [NSJSONSerialization isValidJSONObject:] verification
 *  @result Whether it is successful
 */
- (BOOL)trackClick:(id<BDAutoTrackable>)view withParameters:(nullable NSDictionary<NSString *,id> *)params;
```



* `Objective-C`Please refer to:

   ```objectivec
   [[BDAutoTrack sharedTrack] trackClick:YOUR_COMPONENT];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.shared().trackClick(YOUR_COMPONENT)
   ```
   


<span id="5d2a9e21"></span>
# 9. Collection time events

> This section is supported after 6.10.2 +.


Events with time attributes can use the duration event capture interface, such as capturing video playback duration events. Example:

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
