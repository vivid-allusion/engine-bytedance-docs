---
title: "iOS SDK Event Tracking and Properties"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/iOS_SDK_Event_Tracking_and_Properties"
---

> Before reporting events and attributes, please read the [Supported Data Formats and Event/Property Classification](https://docs.byteplus.com/docs/DataFinder/Supported_Data_Formats_and_Event_Property_Classification)introduction.


<span id="_1-用户与用户属性"></span>
# 1. Users and user attributes

<span id="_1-1-登录态变化调用"></span>
## 1.1 Login state change call

> Versions after the 6.13.0 allow calls prior to gastTrack to set the initialized login state.

> 6.13.0 previous versions only took effect after the SDK was launched.


<span id="_1-1-1-账户登录"></span>
### 1.1.1 Account login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.


* `Objective-C`Please refer to:

   ```objectivec
   #import <RangersAppLog/RangersAppLog.h>
   //Set the ID of your account system and ensure its uniqueness
   [BDAutoTrack setCurrentUserUniqueID:@"{{USER_UNIQUE_ID}}"];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.setCurrentUserUniqueID("{{USER_UNIQUE_ID}}")
   ```
   


<span id="_1-1-2-账户登出"></span>
### 1.1.2 Account Logout

Called when the account is logged out.


* `Objective-C`Please refer to:

   ```objectivec
   [BDAutoTrack clearUserUniqueID];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.clearUserUniqueID()
   ```
   


<span id="_1-2-设置用户属性"></span>
## 1.2 Setting user properties

<span id="_1-2-1-profileset"></span>
### 1.2.1 profileSet

Set user properties, override if they exist, and create if they don't.


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Set the user property, the property name is key, and the property value is value
   NSDictionary *profileDict = @{@"key": @("value")};
   [BDAutoTrack profileSet:profileDict];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Set the user property, the property name is key, and the property value is value
   let profileDict: [AnyHashable: Any] = [
       "key": "value"
   ]
   BDAutoTrack.profileSet(profileDict)
   ```
   


<span id="_1-2-2-profilesetonce"></span>
### 1.2.2 profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Set a user property with the property name key_once and the property value value_once
   NSDictionary *profileDict = @{@"key_once": @("value_once")};
   [BDAutoTrack profileSetOnce:profileDict];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Set a user property with the property name key_once and the property value value_once
   let profileDict: [AnyHashable: Any] = [
       "key_once": "value_once"
   ]
   BDAutoTrack.profileSetOnce(profileDict)
   ```
   


<span id="_1-2-3-profileincrement"></span>
### 1.2.3 profileIncrement

Set the properties of the numeric type to accumulate.


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Set the user property, the property name is key, and the property value is 1
   [BDAutoTrack profileIncrement:@{@"key": @(1)}];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Set the user property, the property name is key, and the property value is 1
   let profileDict: [AnyHashable: Number] = [
       "key": 1
   ]
   BDAutoTrack.profileIncrement(profileDict)
   ```
   


<span id="_1-2-4-profileappend"></span>
### 1.2.4 profileAppend

Set the user properties of the List type to be continuously added to the List.


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
   [BDAutoTrack profileAppend:@{
       @"key": @[@"value_append"]
   }];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
   BDAutoTrack.profileAppend([["key"]:["value_append"]])
   ```
   


<span id="_1-2-5-profileunset"></span>
### 1.2.5 profileUnset

Delete the user's attributes.


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Delete a user attribute named key
   [BDAutoTrack profileUnset:@"key"];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Delete a user attribute named key
   BDAutoTrack.profileUnset("key")
   ```
   


<span id="_2-事件与事件属性"></span>
# 2. Events and event properties

<span id="_2-1-上报代码埋点"></span>
## 2.1 Reporting code event tracking

User behavior logs are in the form of event + attribute params. Events typically correspond to multiple attributes, or they can only have events without attributes. Code event tracking schemes are typically designed by data analysts or product operations.

Code event tracking that only reports events, as follows:


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Report an event that does not contain properties
   //placed in the corresponding position of business logic
   [BDAutoTrack eventV3:@"event" params:nil];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Report an event that does not contain properties
   //placed in the corresponding position of business logic
   BDAutoTrack.eventV3("event", params: nil)
   ```
   


Code event tracking for reporting events and corresponding properties, as follows:


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Report an event, which contains two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //. A property of type int, the property name key_int, the property value is 10
   //placed in the corresponding position of business logic
   [BDAutoTrack eventV3:@"event" 
                params:@{@"key_string":@"value_string",
                         @"key_int": @(10)}];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Report an event, which contains two properties
   //A property of type string, the property name is key_string, and the property value is value_string
   //. A property of type int, the property name key_int, the property value is 10
   //placed in the corresponding position of business logic
   BDAutoTrack.eventV3("event", params: ["key_string": "value_string",
                                         "key_int": 10])
   ```
   


<span id="_2-2-事件公共属性"></span>
## 2.2 Event public properties

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="_2-2-1-设置公共属性"></span>
### 2.2.1 set public properties


* `Objective-C`Please refer to:

   ```objectivec
   /* * Example: Set a custom public property with the property name key_public and the property value value_public * Please note about customizing "public properties": * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail; * 2. High-frequency modifications are not recommended, such as once per second. */
   [BDAutoTrack setCustomHeaderValue:@"value_public" forKey:@"key_public"];
   ```
   

* `Swift`please refer to:

   ```swift
   /* * Example: Set a custom public property with the property name key_public and the property value value_public * Please note about customizing "public properties": * 1. The reporting mechanism is to submit with each log sending. The default log sending frequency is 1 minute. Therefore, if you modify the custom public properties continuously within one minute, the last modification before the log is sent shall prevail; * 2. High-frequency modifications are not recommended, such as once per second. */
   BDAutoTrack.setCustomHeaderValue { () -> [String : Any] in
               return ["key_public":"value_public"]
   }
   ```
   


<span id="_2-2-2-移除公共属性"></span>
### 2.2.2 Remove Public Attributes


* `Objective-C`Please refer to:

   ```objectivec
   //Example: Remove a public property named key_public
   [BDAutoTrack removeCustomHeaderValueForKey:@"key_public"];
   ```
   

* `Swift`please refer to:

   ```swift
   //Example: Remove a public property named key_public
   BDAutoTrack.removeCustomHeaderValueForKey("key_public");
   ```
   


<span id="_3-获取平台id与通知"></span>
# 3. Obtain platform ID and notification

<span id="_3-1-获取平台生成id"></span>
## 3.1 Obtaining the platform generated ID


* `Objective-C`Please refer to:

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
   

* `Swift`please refer to:

   ```swift
   NotificationCenter.default.addObserver(self, selector: #selector(onRegisterSuccess), name: NSNotification.Name(rawValue: BDAutoTrackNotificationRegisterSuccess), object: nil)
   
   func onRegisterSuccess(noti: Notification) {
       let did = noti.userInfo[kBDAutoTrackNotificationRangersDeviceID]
       let ssid = noti.userInfo[kBDAutoTrackNotificationSSID]
       print("onRegisterSuccess.dids：\(did)")
       print("onRegisterSuccess.ssids：\(ssid)")
   }
   ```
   


<span id="_3-2-获取sdk版本号"></span>
## 3.2 Obtaining the SDK version number


* `Objective-C`Please refer to:

   ```objectivec
   //The SDK version number format is X.X.X
   [BDAutoTrack SDKVersion];
   ```
   

* `Swift`please refer to:

   ```swift
   BDAutoTrack.sdkVersion()
   ```
   


<span id="_3-3-获取各类通知"></span>
## 3.3 Obtaining various notifications

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


<span id="_4-默认公共属性字段"></span>
# 4. Default public attribute fields

The SDK collects the following information by default and as a public user attribute, it can be grouped and filtered in the growth analysis (DataFinder).


|Field name |Field type |Parameter name |
|---|---|---|
|os |string |Equipment system, the corresponding product attributes are os_name. |
|os_version |string |operating system version |
|app_version |string |App version |
|app_version_minor |string |Secondary version number, App four\-digit version number, set [OKApplicationInfo sharedInstance] .buildVersion = @" 1.2.3.4 "; |
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
|access |string |network type |


<span id="_5-游戏数据埋点上报接口"></span>
# 5. Game tracking event reporting interface

If you have used BytePlus's game growth analysis product (which has been removed from the shelves) and are currently using the growth analysis (DataFinder) product, in order to improve your event tracking efficiency, the SDK provides a built\-in interface, you only need to pass in the specified parameters according to the prompts.

```objectivec
#import "BDAutoTrack+GameTrack.h" //Please import the correct header file first

/** Ad button clicks: gt_ad_button_click ad_type string Advertising type: incentive video, interstitial screen, banner, etc., directly using Chinese characters or English for identification ad_position_type string Advertising point type: Access by category provided ad_position string Advertising points: resurrection, doubling, trial, buff, reward props, new props, minus CD, etc., directly use text or English to identify Trigger condition: When the user clicks the button of each advertising space in the app. */
- (void)adButtonClickEventWithADType:(NSString *)adType
                        positionType:(NSString *)positionType
                            position:(NSString *)position
                         otherParams:(nullable NSDictionary *)otherParams;

/** Ad starts showing: gt_ad_showad_type string Advertising type: incentive video, interstitial screen, banner, etc., directly using Chinese characters or English for identification ad_position_type string Advertising point type: Access by category provided ad_position string Advertising points: resurrection, doubling, trial, buff, reward props, new props, minus CD, etc., directly use text or English to identify Trigger condition: When a user clicks and watches an advertisement. Pangolin ads have callbacks that can be obtained directly. */
- (void)adShowEventWithADType:(NSString *)adType
                 positionType:(NSString *)positionType
                     position:(NSString *)position
                  otherParams:(nullable NSDictionary *)otherParams;

/** End of display: gt_ad_show_end ad_type string Advertising type: incentive video, interstitial screen, banner, etc., directly using Chinese characters or English for identification ad_position_type string Advertising point type: Access by category provided ad_position string Advertising points: resurrection, doubling, trial, buff, reward props, new props, minus CD, etc., directly use text or English to identify Results string Advertisement viewing results: skip, success, failure, etc., identified in English. Skip marked as skip, success marked as success, failure as fail Trigger condition: When the user finishes viewing the ad. */
- (void)adShowEndEventWithADType:(NSString *)adType
                    positionType:(NSString *)positionType
                        position:(NSString *)position
                          result:(NSString *)result
                     otherParams:(nullable NSDictionary *)otherParams;

/** Upgrades and experience: gt_levelup Lev int current player level Gain experience get_exp int Method string How to get experience: successfully pass the customs, complete the guidance, receive rewards, etc., use Chinese characters or English to identify Aflev int Level after the user gains experience. If gaining experience does not result in an upgrade, then lev = aflev. If it results in an upgrade, then lev < aflev. Trigger condition: When the user gains experience or the level changes. */
- (void)levelUpEventWithLevel:(NSInteger)level
                          exp:(NSInteger)exp
                       method:(NSString *)method
                   afterLevel:(NSInteger)afterLevel
                  otherParams:(nullable NSDictionary *)otherParams;

/** Start playing: gt_start_play ectype_name string For the nature of the game, mark the name of the level Trigger condition: When the user starts playing. */
- (void)startPlayEventWithName:(NSString *)ecTypeName
                   otherParams:(nullable NSDictionary *)otherParams;

/** End game: gt_end_play ectype_name string For the nature of the game, mark the name of the level Result string The result of the gameplay: unfinished, successful, failed, etc., marked in English. Uncompleted is marked as uncompleted, success is marked as success, and failure is marked as fail. Duration int elapsed time in seconds Trigger conditions: When the user ends the gameplay, it covers exit halfway, complete but fail, and complete and succeed. */
- (void)endPlayEventWithName:(NSString *)ecTypeName
                      result:(NSString *)result
                     duration:(NSInteger)duration
                  otherParams:(nullable NSDictionary *)otherParams;

/** Earn game currency: gt_get_coins coin_type string Currency type: ingot, tied yuan, gold coin, silver coin, etc., use text or English to identify Method string How to get it: watch incentive videos, pass customs successfully, activity rewards, etc., use text or English to identify Get quantity coin_num int Trigger condition: When the user obtains game coins, resulting in an increase in game coins */
- (void)getCoinsEventWitType:(NSString *)coinType
                      method:(NSString *)method
                  coinNumber:(NSInteger)number
                 otherParams:(nullable NSDictionary *)otherParams;

/** Consume game currency: gt_cost_coins coin_type string Currency type: ingot, tied yuan, gold coin, silver coin, etc., use text or English to identify Method string Consumption path: resurrection, purchase props, unlock levels, etc., use text or English to identify coin_num int consumption Trigger condition: When the user consumes game coins, resulting in a decrease in game coins. */
- (void)costCoinsEventWitType:(NSString *)coinType
                       method:(NSString *)method
                   coinNumber:(NSInteger)number
                  otherParams:(nullable NSDictionary *)otherParams;

/** Internal purchase recharge related: purchase content_type string internal purchase top-up content type content_name string internal purchase top-up content name content_id string internal purchase recharge content id content_num int internal purchase payment_channel string Payment channels: such as Alipay, WeChat, etc Currency string Payment currency type is_success string Whether the payment was successful Amount paid currency_amount int, in yuan Trigger condition: When the user completes the internal purchase recharge and gets the corresponding in-game currency and props */
- (void)purchaseEventWithContentType:(NSString *)contentType
                         contentName:(NSString *)contentName
                           contentID:(NSString *)contentID
                          contentNum:(NSInteger)contentNum
                             channel:(NSString *)channel
                            currency:(NSString *)currency
                           isSuccess:(NSString *)isSuccess
                      currencyAmount:(NSInteger)currencyAmount
                         otherParams:(nullable NSDictionary *)otherParams;

/** Initialization information: gt_init_info Lev int player level coin_type string Get the type of currency coin_left amount of currency left on the int user role_id string player character id-cp side Trigger conditions: The user starts the game and reports when the initialization is complete */
- (void)gameInitInfoEventWithLevel:(NSInteger)level
                          coinType:(NSString *)coinType
                          coinLeft:(NSInteger)coinLeft
                       otherParams:(nullable NSDictionary *)otherParams;
```


<span id="_6-视图曝光事件采集"></span>
# 6. View exposure event capture

> This feature is supported after 6.10.0 +.

> When a component appears within the visible range of the screen, an exposure event is automatically triggered.


<span id="_6-1-组件接入"></span>
## 6.1 Component access

<span id="_6-1-1-cocoapod-引入-exposure"></span>
#### 6.1.1 CocoaPod introduces `Exposure`

> File\-mode integration requires the introduction of corresponding library files.


```objectivec
pod 'RangersAppLog', 'SDK_VERSION',
    :subspecs => [
    ...
    'Exposure',
    ...
]
```


<span id="_6-1-2-头文件引用"></span>
#### 6.1.2 header file reference

```objectivec
//relevant function settings are introduced into the header file
//modular integration @import RangersAppLog;
#import <RangersAppLog/BDAutoTrackExposure.h>
```


<span id="_6-2-功能开关"></span>
## 6.2 Function switch


* `Objective-C`Please refer to:

   ```objectivec
   config.exposureEnabled = YES; //Global function control switch YES | NO. Default is on
   ```
   

* `Swift`please refer to:

   ```swift
   config.exposureEnabled = true
   ```
   


<span id="_6-3-曝光配置设置"></span>
## 6.3 Exposure Configuration Settings

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

```swift
config.exposureConfig.areaRatio(0.5)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function only determines exposure based on the main window, and does not yet support the calculation of sub\-view occlusion.</div>


<span id="_6-4-监控组件曝光"></span>
## 6.4 Monitoring component exposure

Exposure monitoring of component instances.


* `Objective-C`Please refer to:

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
   

* `Swift`please refer to:

   ```swift
   let opt = BDViewExposureData()
   opt.eventName = "view_did_exposure"
   opt.properties = [:]
   opt.config = BDViewExposureConfig.default().areaRatio(0.5)
   BDAutoTrack.shared().observeViewExposure(YOUR_VIEW, with: opt)
   
   BDAutoTrack.shared().disposeViewExposure(YOUR_VIEW)
   ```
   


<span id="_6-5-功能调试"></span>
## 6.5 Functional debugging

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


<span id="_7-全埋点事件"></span>
# 7. Full event tracking

After turning on the full event tracking event collection switch, page events and View click events will be collected by default.


* Application scenario

   
   |Typical scene |Ccene description |
   |---|---|
   |user behavior analysis |Understand the user's behavior path in the application, such as which buttons the user clicks, which pages the user browses, and how long the user spends on a particular page. |
   |A/B Testing |Help evaluate the impact of different versions of a feature or interface on user behavior. For example, compare the click through rate of two different interface layouts and test the impact of different functional implementations on user usage. |
   |problem diagnosis |It helps to quickly identify and locate problems in the application. For example, users frequently log out or crash on a certain page, and the usage of certain features suddenly decreases. |
   |Operational activity effect evaluation |Help evaluate the effectiveness of various operational activities, such as promotions, push notifications, and more. For example: click through rate and conversion rate of a push notification, engagement and effectiveness of a promotion. |
   

* Full event tracking capability support

   
   |Capability support |Capability description |
   |---|---|
   |page visit |* UIViewController Life Cycle<br><br>* UITabBarController toggle<br><br>* UIPageViewController switch<br><br>* UINavigationController switch |
   |click |* sendAction events triggered by UIButton, etc<br><br>* UIAlertAction click event<br><br>* UITableViewCell, UICollectionView click event<br><br>* UIGestureRecognizer Click, Long Press |
   |exposure |UIView and Subclass Exposure |
   

* Full event tracking preset event list and reporting mechanism

   
   |Full event tracking event list |Event description |Event triggering mechanism |
   |---|---|---|
   |bav2b_page |page view event | |
   |$bav2b_page_leave |page leave | |
   |bav2b_click |element click event | |
   |bav2b_beat |page heartbeat event | |
   |$bav2b_slide |Slide event | |
   


See below for a detailed description of each preset event and the associated event properties.

<span id="_7-1-功能开启"></span>
## 7.1 Function enabled

<span id="d3f4cd90"></span>
### 7.1.1 Full event tracking switch

You can introduce the corresponding subspec module or static library file into the project to turn on the full event tracking switch depending on the integration method.


* `Objective-C`Please refer to:

   ```objectivec
   //Enable full event tracking, the default is YES
   config.autoTrackEnabled = YES;
   //Enable WebView full event tracking, the default is YES
   config.H5AutoTrackEnabled = YES;
   ```
   

* `Swift`please refer to:

   ```swift
   config.autoTrackEnabled = true
   config.H5AutoTrackEnabled = true
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">trackEventEnabled is the event reporting master switch, the default is YES.</div>


* <div data-tips="true" data-tips-type="tip">Priority: trackEventEnabled \> autoTrackEnabled \> H5AutoTrackEnabled</div>



<span id="b335bd4a"></span>
### 7.1.2 preset event list and reporting logic


|Full event tracking event list |Event description |Event triggering mechanism |
|---|---|---|
|bav2b_page |page visit |Trigger the report after the page is opened |
|$bav2b_page_leave |page leave |Trigger a report after leaving the page |
|bav2b_click |View element click event |Trigger a report after clicking on a page element |


Of which:


* bav2b_page: Contains source page related attributes (refer_page_xx), when the application is cold start, such attribute values will be empty, and the page will be filled with source page information in the new page after the page jump.

* $bav2b_page_leave: Record a duration event with when the page is entered as the key, and record the current entry time. Extract the duration event when the page exits, subtract the page entry time from the current time, and the median difference is the length of the dwell time.


For more detailed descriptions of each preset event and related event properties, see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties).

<span id="_7-1-1-基于事件类型功能开关"></span>
### 7.1.3 Function switch based on event type

> This section is supported in version 6.11.0 +.

> Allows full event tracking event type configuration, as defined in `< BDCommonEnumDefine.h >`.


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


<span id="ceac4db3"></span>
### 7.1.4 DataFinder console open

After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.

<span id="_7-2-自定义页面浏览事件属性"></span>
## 7.2 Customizing Page View Event Properties

> Please set the parameter value in the init method, otherwise the parameter value may be empty when the page view event is first triggered.

> Customize the parameters of the page view event through the `UIViewController`extension API.


```objectivec
/*! @abstract Manually set PageTitle @Discussion If set, it will be collected when the page is switched. @Discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackPageTitle;
 /*! @abstract Manually set PageID @Discussion If set, it will be collected when the page is switched. @Discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackPageID;
 /*! @abstract Manually set PagePath @Discussion If set, it will be collected when the page is switched. @Discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackPagePath;
 /*! @abstract Manually set extra information @Discussion If set, it will be collected when the page is switched. @Discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSString *> *bdAutoTrackExtraInfos;
 /*! @Abstract Custom collection properties, the same key will override the default collection params @Discussion If set, it will be collected when the page is switched. @Discussion If set, the View in this VC will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSObject *> *bdAutoTrackPageProperties;
```


<span id="_7-3-自定义点击事件属性"></span>
## 7.3 Custom Click Event Properties

Customize the parameters of the click event through `UIView`and `UIBarButtonItem`extension APIs.

```objectivec
/*! @Abstract This corresponds to the newly added element_id field, and bdAutoTrackViewID corresponds to the element_manual_key field @Discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackElementID;
 
/*! @abstract Manually set ViewID @Discussion If set, it will be collected when clicked, which can uniquely mark the View. */
@property (nonatomic, copy) NSString *bdAutoTrackViewID;
 
/*! @abstract Manually set ViewContent @Discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSString *bdAutoTrackViewContent;
 
/*! @abstract Manually set extra information @Discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSString *> *bdAutoTrackExtraInfos;
 
/*! @Abstract Custom collection properties, the same key will override the default collection params @Discussion If set, it will be collected when clicked. */
@property (nonatomic, copy) NSDictionary<NSString*, NSObject *> *bdAutoTrackViewProperties;
 
/*! @abstract custom collection development @Discussion If you set YES, event tracking will be ignored when clicked */
@property (nonatomic, assign) BOOL bdAutoTrackIgnoreClick;
```


<span id="_7-4-忽略特定全埋点事件"></span>
## 7.4 Ignoring specific all\-event tracking events

<span id="_7-4-1-忽略特定页面浏览事件"></span>
### 7.4.1 Ignore specific page view events

```objectivec
/*! @Abstract Ignore the automatically collected browsing event tracking in UIViewController    @Discussion ignores that the scope is its own class, which does not affect the inheritance relationship. For example, BViewController inherits from AViewController. If both are ignored, you need to pass in @[[AViewController class], [BViewController class]]    @Param controllerClasses pass in the class name to be ignored @[[TestViewController class], [UserViewController class]] */
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
   


<span id="_7-4-2-忽略特定控件点击事件"></span>
### 7.4.2 Ignore specific control click events

```objectivec
/*! @Abstract Ignore auto-collected click event tracking in controls    @Discussion ignore scope to own class    @Param viewClasses pass in the class name to be ignored @[[AButton class], [ALabel class]] */
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
   


<span id="_7-5-手动触发全埋点事件采集"></span>
## 7.5 Manually trigger full event tracking event collection

<span id="_7-5-1-手动触发页面浏览事件"></span>
### 7.5.1 Manually trigger page view events

```objectivec
/*! * @abstract code triggers page view event tracking report * @param controller can pass UIViewController and objects that implement the BDAutoTrackable protocol * @result is successful */
- (BOOL)trackPage:(id<BDAutoTrackable>)controller;

/*! * @abstract code triggers page view event tracking report * @param controller can pass UIViewController * @param params user-defined parameters for [NSJSONSerialization isValidJSONObject:] validation * @result is successful */
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
   


<span id="_7-5-2-手动触发点击事件"></span>
### 7.5.2 Manually trigger click events

```objectivec
/*! * @abstract code trigger click event tracking report * @Param view can pass control objects such as UIView, as well as objects that implement the BDAutoTrackable protocol * @result is successful */
- (BOOL)trackClick:(id<BDAutoTrackable>)view;
 
/*! * @abstract code trigger click event tracking report * @Param view can pass control objects such as UIView, as well as objects that implement the BDAutoTrackable protocol * @param params user-defined parameters for [NSJSONSerialization isValidJSONObject:] validation * @result is successful */
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
   


<span id="_8-采集时长事件"></span>
# 8. Collection time events

> This section is supported after 6.10.2 +.

> Events with time attributes can use the duration event capture interface, such as capturing video playback duration events. Example:


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
