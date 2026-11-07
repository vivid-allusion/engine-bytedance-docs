---
title: "Android SDK Debugging and Data Verification"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Android-SDK-Debugging-and-Data-Verification"
---

<span id="_1-检查项验证"></span>
# 1. Check item verification

(1) Whether the SDK is introduced can be introduced in two ways: remote introduction and offline introduction. Remote introduction is recommended. If it is remote introduction, check whether the app\-level gradle file is introduced into the SDK in the dependencies.

(2) Check whether the maven repository is added to the repositories of allprojects in the project\-level gradle

(3) If you use the full event tracking function, determine whether the maven repository is added to the repositories of buildscript in the project\-level gradle and whether the dependencies are increased.

(4) If you use real\-time event tracking monitoring or circling function, you need to do the following verification: [Why real-time event tracking and circling cannot be entered](https://docs.volcengine.com/docs/6285/106883?lang=en#why-real-time-event-tracking-and-circling-cannot-be-entered).

(5) Verify whether the version numbers of plugin, sdk, and scheme are consistent

(6) Check whether the initialization code is integrated

(7) Check whether the appid is the appid you want to upload the app to.

(8) Check whether the channel field after the appid has a value. This field is required and means channels, such as oppo, vivo, huawei and other channels.

(9) Check whether the data reporting address is set correctly. If it is a private deployment, you need to configure the data upload address of the private deployment. When doing data reporting, you need to ensure that the mobile phone and computer can access this address. The machine can ping the domain name.

(10) Check whether the ab switch is turned on: config.setAbEnable (**true**)

(11) Check whether the experimental code calls the getabcofig method

(12) After the above inspection and verification, you can call the relevant APIs, such as diversion, user, event and other APIs to report

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

(1) See the two Applog related logs marked in the picture to prove that the sdk initialization was successful (provided that the log switch needs to be turned on during initialization)

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_052aa5c3bb5cf54a692db47c04518a7e.png) </span>

(2) Get the ssid by getting the ssid api. Since the id service will request the ssid after the sdk is initialized, please get it after 3 seconds after the initialization is completed;

```bash
// Please start retrieving after 3 seconds of initialization completion, otherwise it may return empty
String ssid = AppLog.getSsid(); // acquire SSID
```


(3) After obtaining the ssid, add the ssid to any version of the whitelist for testing, and click the "Save" button in the lower right corner.

Whitelist function description (please refer to this document for details: [User Testing Whitelist](https://docs.byteplus.com/docs/DataTester/User-Testing-Whitelist)).

[1] The whitelist function is mainly used to test and debug experiments/features. Users who add the whitelist will be forced to hit the experiment, which is convenient for testing the effect of the experimental version and the control version during the testing process.

[2] The whitelist needs to add the shunt id. The client side experimental shunt id is ssid, and the decisionid used for the server level experimental shunt id (that is, the first id of the code). Generally, we recommend using uuid, so we will also see that some whitelists are uuid.

(4) Run the app to see if the experimental parameter in the log is the version value corresponding to adding the whitelist. If the experiment is missed, the default value will be returned.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68043eb4d2fa4ee4893510e87efa9e01~tplv-goo7wpa0wc-image.image) </span>

If the default value is returned, it needs to be checked.

[1] Whether to save the ssid after adding it.

[2] Whether the ssid was added correctly, and whether the running ssid is the ssid that added the whitelist.

[3] abtest_config interface returns whether it is 200.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_624dda65f752c15e8d5e4b6c7e40dcf5.jpg) </span>

[4] If none of the above is true, determine whether the code to obtain the experimental parameters is executed before initialization.

(5) If the experimental parameters are obtained normally, then the entire experimental debugging is completed.

<span id="_3-数据验证"></span>
# 3. Data validation

<span id="_3-1-埋点验证功能验证"></span>
## 3.1 Event tracking verification function verification

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you buy the private deployment version of AB separately, only the supertube permission can be used. If other members need to verify, you can use the capture package. Those who buy AB and finder at the same time can be used normally.</div>


Function description: [https://www.volcengine.com/docs/6285/66054](https://www.volcengine.com/docs/6285/66054)

It needs to be integrated according to the relevant requirements of real\-time event tracking. When the integration is successful, in System Management \- Data Management \- General Events, click Verify Event Tracking, and select Mobile End.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1335bffc0fa421c9431828a1b1c1a46~tplv-goo7wpa0wc-image.image) </span>

After scanning the code, you will see the reported behavior data in real time. The left side is the real\-time behavior, and the right side is the attribute information of the corresponding behavior.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95b6e88736b44295a3608bd6135447e9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-抓包验证"></span>
## 3.2 Packet capture verification

Configure the packet capture tool, select the interface corresponding to the data reporting address, view the event_v3 interface in the app_log, and also see the results returned by the abtest_config interface through the packet capture.

Private deployment needs to select the corresponding data reporting address.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdf8d2a07d65441cbce350a80f6acd8c~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-系统验证"></span>
## 3.3 System verification

In Metrics Management \- Data Management Verify that the reported custom events and custom properties exist in the event list, event properties, and user properties list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76c92f4fa82c431cb6a08963838e7d5b~tplv-goo7wpa0wc-image.image) </span>

In the global settings \- audience management \- user scrutiny, view the detailed behavior of the reported user. When the user scrutinizes the verification data, the entire integration and reporting will be verified.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/524427db105143e39b0b227e34916461~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/625210f6c22747beb27906f042cf2cb1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c8cf1ede22040abb67786dc073ead59~tplv-goo7wpa0wc-image.image) </span>
