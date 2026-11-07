---
title: "iOS SDK Debugging and Data Validation"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/iOS-SDK-Debugging-and-Data-Validation"
---

<span id="_1-检查项验证"></span>
# 1. Check item verification

(1) Whether the SDK is introduced can be introduced remotely and offline. Remote introduction is recommended. If you need to introduce it manually, please download the SDK first, and then refer to the documentation to introduce it manually;

(2) Check if the source is added

(3) Check whether the SDK initialization code is integrated (4) Check whether the appid is the appid that you want to report to the application.

(5) Check whether the channel channel is configured, iOS the general default App Store channel

(6) Check whether the data reporting address is set correctly. If it is a private deployment, you need to configure the data upload address of the private deployment. When doing data reporting, you need to ensure that the mobile phone and computer can access this address. The machine can ping the domain name.

(7) Check whether the AB switch is turned on: config.abEnable = YES;

(8) Check whether to call the experimental API ABTestConfigValueForKey;

(9) If you use real\-time event tracking monitoring or circling function, you need to do the following verification: [Why real-time event tracking detection and circling cannot be entered](https://www.volcengine.com/docs/6285/106883).

(10) After the above inspection and verification, you can call the relevant APIs, such as diversion, user, event and other APIs to report.

<span id="_2-实验调试"></span>
# 2. Experimental debugging

<span id="_2-1-为什么要调试实验"></span>
## 2.1 Why Debug Experiments

Before the experiment is launched, it is necessary to ensure that the previous integration process is correct, and only after the experiment is launched can the scientific and effective results be guaranteed!

<span id="_2-2-开启调试状态"></span>
## 2.2 Turn on the debugging state

Make the experiment in the "debugging" state, as shown in the following figure:


* The experimental status is divided into three categories: debugging, running, and completed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/681e7dd34bad4e0a88b381afeb2334f5~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-开始调试验证"></span>
## 2.3 Start debugging and verification

(1) Turn on the log switch during initialization, and you can see the Track Launch event related information in the output to prove that the sdk initialization was successful.


* Objective\-c

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ae8e6a0a1fb7b062dce26c8f585e13e.png) </span>

* Swift

   ```Swift
   //Output logs in the console, which can be used to observe user behavior log reports. It is recommended to close it when online
   config.showDebugLog = true //true: open log, false: close log
   config.logger = { (log) inprint(log ?? "log is nil")} //Set Logger when opening log
   ```
   


(2) Get ssid by getting ssid api, because after sdk is initialized, it will go to the id service to get ssid, so add a 2s delay before getting ssid


* Objective\-c

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
   

* Swift

   ```Swift
   NotificationCenter.default.addObserver(self, selector: #selector(onRegisterSuccess), name: NSNotification.Name(rawValue: BDAutoTrackNotificationRegisterSuccess), object: nil)
   
   func onRegisterSuccess(noti: Notification) {
       let did = noti.userInfo[kBDAutoTrackNotificationRangersDeviceID]
       let ssid = noti.userInfo[kBDAutoTrackNotificationSSID]
       print("onRegisterSuccess.dids：\(did)")
       print("onRegisterSuccess.ssids：\(ssid)")
   }
   ```
   


(3) After obtaining the ssid, add the ssid to any version of the whitelist for testing, and click the "Save" button in the lower right corner.

Whitelist Function Description (Please refer to [User Testing Whitelist](https://docs.byteplus.com/docs/DataTester/User-Testing-Whitelist))


* The whitelist function is mainly used to test and debug experiments/features. Users who add the whitelist will be forced to hit the experiment, which is convenient for testing the effect of the experimental version and the control version during the testing process.

* The whitelist needs to add the shunt id. The client side experimental shunt id is ssid, and the decisionid used by the server level experimental shunt id (that is, the first id of the code). Generally, we recommend using uuid, so we will also see that some whitelists are uuid.


(4) Run the app to see if the experimental parameter returned in the lower right corner is the version value corresponding to adding the whitelist. If the experiment is missed, the default value will be returned.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68981cb9210f83c4bc0ec647b4134ab4.png) </span>

If the default value is returned, you need to check:


* Whether to save after ssid is added

* Is ssid added correctly? Is the running ssid a whitelisted ssid?

* abtest_config whether the interface is connected, search abtest_config in the log to see if the interface is connected

* If none of the above is true, determine whether the code that obtains the experimental parameters is executed before initialization


(5) If the experimental parameters are obtained normally, then the entire experimental debugging is OK.

<span id="_3-数据验证"></span>
# 3. Data validation

<span id="_3-1-埋点验证功能验证"></span>
## 3.1 Event tracking verification function verification

Note: If you buy the private deployment version of AB separately, only the supertube permission can be used. If other members need to verify, you can use the capture package, and those who buy AB and finder at the same time can use it normally.

Function description: [https://www.volcengine.com/docs/6285/66054](https://www.volcengine.com/docs/6285/66054)

It needs to be integrated according to the relevant requirements of real\-time event tracking. When the integration is successful, in System Management \- Data Management \- General Events, click Verify Event Tracking, and select Mobile End.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1335bffc0fa421c9431828a1b1c1a46~tplv-goo7wpa0wc-image.image) </span>

After scanning the code, you will see the reported behavior data in real time. The left side is the real\-time behavior, and the right side is the attribute information of the corresponding behavior.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3cc677f5c8195655ad0bd7927cded511.png) </span>

<span id="_3-2-抓包验证"></span>
## 3.2 Packet capture verification

Configure the packet capture tool, select the interface corresponding to the data reporting address, view the event_v3 interface in the app_log, or see the result returned by the abtest_config interface through the packet capture

Private deployment needs to select the corresponding data reporting addres

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdf8d2a07d65441cbce350a80f6acd8c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-系统验证"></span>
## 3.3 System verification

In Metrics Management \- Data Management Verify that the reported custom events and custom properties exist in the event list, event properties, and user properties list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76c92f4fa82c431cb6a08963838e7d5b~tplv-goo7wpa0wc-image.image) </span>

In the global settings \- audience management \- user details, view the detailed behavior of the reported user. When the user scrutinizes the verification data, the entire integration and reporting will be verified.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/524427db105143e39b0b227e34916461~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/625210f6c22747beb27906f042cf2cb1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c8cf1ede22040abb67786dc073ead59~tplv-goo7wpa0wc-image.image) </span>
