---
title: "Web/JS SDK Debugging and Data Validation"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Web-JS-SDK-Debugging-and-Data-Validation"
---

<span id="_1-检查项验证"></span>
# 1. Check item verification

(1) Whether the SDK file is introduced and the initialization integration code is added

(2) Whether the appid is the appid to be reported to the application

(3) Whether the data reporting address is correct

Saas\-Domestic: See if the channel is cn.

Saas\-overseas: see if the channel is sg

Private deployment: init method to see channel_domain parameters are added, if there is added, to determine whether the channel_domain is configured for the data reporting address, the configuration of the data upload address can be accessed by the machine (channel_domain: 'https://xxxx.com').

(4) Whether to turn on the AB switch: enable_ab_test: true

(5) If it is a private deployment, determine the init method, whether to configure ab_channel_domain, and if so, determine whether ab_channel_domain is the data reporting address (ab_channel_domain: 'https://xxx.com')

(6) If it is a visual experiment, whether to turn on the visual switch: enable_ab_visual: true

(7) If it is a multi\-link experiment, whether to turn on the multi\-link experiment switch and set the mask layer: enable_multilink: true, multilink_timeout_ms: 1000;

(8) Whether to add the method getvar to obtain experimental parameters, and call this method to report the AB exposure event.

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

(1) [SDK Initialization Verification] Open the developer tools, and you can see "sdk is ready" in the console to prove that the sdk initialization is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30bc573cc02d4e718ba2cd3a30f8f922~tplv-goo7wpa0wc-image.image) </span>

(2) [ssid acquisition] Get the statistical caliber (ssid) of the debugging device in the browser. Turn on the A/B Test and log switch in the Web/H5/Wap SDK, and complete the initialization:


* Call getToken in the code to get ssid!


```javascript
window.collectEvent('getToken', (res)=> {
   console.log(res)
})
javascript
```



* Query ssid in developer tools (chrome example)


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c10c1a266404a991a5b44f1b35fc3d10.png) </span>

(3) After obtaining the ssid, add the ssid to any version of the whitelist for testing, and click the "Save" button in the lower right corner.

Whitelist function description (please refer to this document for details: [User Testing Whitelist](https://docs.byteplus.com/docs/DataTester/User-Testing-Whitelist)).

[1] The whitelist function is mainly used to test and debug experiments/features. Users who add the whitelist will be forced to hit the experiment, which is convenient for testing the effect of the experimental version and the control version during the testing process.

[2] The whitelist needs to add the shunt id. The client side experimental shunt id is ssid, and the decisionid used for the server level experimental shunt id (that is, the first id of the code). Generally, we recommend using uuid, so we will also see that some whitelists are uuid.

(4) ab shunt interface verification

Select the network to find abtest_config interface to see if the data returns the experimental version information added in the whitelist, for example: the test adds ssid to the experimental version, then abtest_config should return the vid and value of the experimental version, if you see the corresponding experimental version information, then prove that the shunt is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbf1c960064b44708a70a9e53fed50e1~tplv-goo7wpa0wc-image.image) </span>

(5) [Exposure Event Verification] For the AB system, no matter what the SDK, as long as the experimental SDK side is hit, a preset event (abtest_exposure) will be reported to record the user's incoming group information, so we can check the list interface in the console\-network to see if the abtest_exposure event is triggered.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adcf3155ced54fdd9399c0d294d6bdff~tplv-goo7wpa0wc-image.image) </span>

If these five steps are successfully verified, then it proves that our experimental debugging has been successful.

<span id="_3-数据验证"></span>
# 3. Data validation

<span id="_3-1-控制台验证"></span>
## 3.1 Console verification

Select the network, when the code event tracking, then every click will report a list interface, check the list interface, whether the interface is 200, and see the custom event, attribute reporting and event ab_sdk_version in the load. If the interface is 200, you can see custom events and custom properties to prove that the event was successfully reported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b0dc18126be4c4ea50be055a9243bad~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-系统验证"></span>
## 3.2 System verification

In Metrics Management \- Data Management Verify that the reported custom events and custom properties exist in the event list, event properties, and user properties list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1335bffc0fa421c9431828a1b1c1a46~tplv-goo7wpa0wc-image.image) </span>

In Global Settings \- Audience Management \- User Review, view the detailed behavior of the reported user. When the verification data is OK after the user review, the entire integration and reporting is completed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/524427db105143e39b0b227e34916461~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/625210f6c22747beb27906f042cf2cb1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c8cf1ede22040abb67786dc073ead59~tplv-goo7wpa0wc-image.image) </span>
