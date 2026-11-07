---
title: "General Event Tracking Verification Operation Guide"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/General_Event_Tracking_Verification_Operation_Guide"
---

<span id="3403f53d"></span>
# 1. Integrated verification

<span id="0a273588"></span>
## 1.1 Web JS SDK

<span id="1753e66f"></span>
### 1.1.1 check item validation


|**Check item** |**Inspection precautions** |**Reference documentation** |
|---|---|---|
|Is the SDK introduced? |Check the SDK integration code, the code needs to **introduce the JavaScript file of the SDK first** and then initialize the SDK. |[Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_) |
|Is the APPID correct? |Check whether the APPID in the initialization code is the APPID that needs to be reported to the application. ||
|Check whether the reporting address is correct. |*  ||


<span id="8e8dd51c"></span>
### 1.1.2 Integration verification


1. After opening the web page, you can see "sdk is ready" in the browser console to prove that the sdk initialization was successful.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/187431e075764ce283a59c32361070b1~tplv-goo7wpa0wc-image.image" width="1727px" />   </div>
   

2. Select Network. If the code event tracking is successfully completed, the list interface will be reported every time you click on the web interface. You can check:

   * Check if the http code of the list interface is 200 and if the interface returns e: 0.

   * See custom events and property reports in the payload.

      If the interface HTTP code is 200, the return value is e: 0, and you can see the custom event and custom properties to prove that the event was successfully reported.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b49c8bfdb1cc4f6988ea517b328cf656~tplv-goo7wpa0wc-image.image" width="1719px" />   </div>
   

   If the return value e is not 0, you can check this table again.

   
   |**Return field** |**Type** |**Return value description** |
   |---|---|---|
   |e |int |Status Code:<br><br><br>* 0: normal<br><br>* \-1: Request parameter validation error (missing user, header, or event)<br><br>* \-2: event format error<br><br>* \-3: Request parameter parsing error (no parsing json)<br><br>* \-4: Unsupported request types<br><br>* \-5: Request array is too long (only for list interface, limit 50)<br><br>* \-6: Too many events in the request (limit 50)<br><br>* \-7: Get APPID error<br><br>* \-8: Parse user errors (mostly internal errors)<br><br>* \-9: Parse header error (multidimensional internal error)<br><br>* \-10: Parse event error (mostly internal error)<br><br>* \-11: Data sent downstream error (internal error)<br><br>* \-12: event array is empty<br><br>* \-100: Unknown error |
   |m |string |Error message, only appears when the request is verbose |
   |tc |int |Total number of events in the request |
   |sc |int |Number of events successfully parsed and collected |
   


<span id="1628f1f6"></span>
## 1.2 Android SDK

<span id="1a4e3a08"></span>
### 1.2.1 check item validation


|**Check item** |**Inspection precautions** |**reference documentation** |
|---|---|---|
|Is the SDK introduced? |* It can be imported in two ways: remote import (push) and offline import. If it is imported remotely, you need to check whether the app\-level gradle file introduces the SDK in the dependencies.<br><br>* Check whether the maven repository is added to the repositories of allprojects in the project\-level gradle.<br><br>* Check if the initialization code is integrated |[Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_) |
|Is the APPID and channel address correct? |* Check whether the APPID in the initialization code is the APPID that needs to be reported to the application.<br><br>* Check whether the channel address channel field after the appid has a value. This field is required, such as oppo, vivo, huawei and other channels. ||
|Is the data reporting address correct? |Confirm whether the data reporting address is configured correctly.<br><br><br>* Saas: use the default value ||
|(Optional)<br><br>Use full event tracking and other additional required checks |* If using the full event tracking function, determine whether to add the maven repository to the repositories of buildscript in the project\-level gradle, and whether to add the plugin to the dependencies.<br><br>* If you use real\-time event tracking or circling, you need to do the following verification<br><br>   * Confirm the introduction of the scheme package: [1.5 Real-time event tracking and circling (optional)](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_#_1-5-%E5%AE%9E%E6%97%B6%E5%9F%8B%E7%82%B9%E6%A3%80%E6%B5%8B%E5%92%8C%E5%9C%88%E9%80%89%E5%8A%9F%E8%83%BD-%E5%8F%AF%E9%80%89).<br><br>   * Verify that the schema configuration is correct, such as the APPID, URL schema in it: [4. Configuration Scheme (optional)](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_#_4-%E9%85%8D%E7%BD%AEscheme-%E5%8F%AF%E9%80%89).<br><br>* Verify whether the version numbers of pluign, sdk and scheme are consistent. | |


After the above check and verification, you can call the relevant APIs, such as user, event, and other APIs to report.

<span id="9a4b573b"></span>
### 1.2.2 Integration verification

<span id="b4f2c4ad"></span>
#### 1.2.2.1 Power builder verification (Android stuido)


1. See the two proofs marked in the picture to prove that the sdk was successfully initialized (provided that the log switch is turned on during initialization to see it)

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff59471faee241e2ada039aa1f199b13~tplv-goo7wpa0wc-image.image" width="2274px" />   </div>
   

2. When reporting an event, to see if the event is successfully reported, you need to use the capture or event tracking verification function, refer to 1.2.2.2 or 1.2.2.3.


<span id="db30a4c8"></span>
#### 1.2.2.2 DevTools validation event report

Function description: [event tracking developer tool](https://www.volcengine.com/docs/76880/1033592)

After accessing DevTools according to the documentation, open the DevTools panel to view access status, parameter configuration, event reporting and log requests, etc

Reference to determine whether the local report is normal:


* The status in the information bar is started, and there are SSID, BD_DID and other information

* Events in the event list exist and have been reported

* In the network list/service/2/app_log/interface status is 200 (green)


<span id="4d0610ad"></span>
#### 1.2.2.3 Event tracking verification function verification

Function description:[Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)

It needs to be integrated according to the relevant requirements of real\-time event tracking. When the integration is successful, in Data Management \- General Events, click Verify Event Tracking, and select Mobile End.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cf5b405abf34130a99ad5a25d76d303~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


After scanning the code, you will see the reported behavior data in real time. The left side is the real\-time behavior, and the right side is the attribute information of the corresponding behavior.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6ac3ad7f37a428484ee3a8caf7eb98f~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


<span id="2f8a5d0e"></span>
#### 1.2.2.4 capture verification

Configure the packet capture tool, select the interface corresponding to the data reporting address to view the interface of the app_logevent_v3

Saas address: http://toblog.volceapplog.com

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e54a8a088807458a8183fb63c2072877~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


<span id="5dd9b65e"></span>
## 1.3 iOS SDK

<span id="84ac1aed"></span>
### 1.3.1 Check item validation


|**Check item** |**Inspection precautions** |**Reference documentation** |
|---|---|---|
|Is the SDK introduced? |* You can import it remotely (recommended) and offline. If you need to import it manually, please download the SDK first, and then refer to the documentation for hand integration:[1.5 Manual introduction instructions](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration#8632f037)<br><br>* Check if the source is added<br><br>* Check if the initialization code is integrated |[(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration) |
|Is the APPID and channel address correct? |* Check whether the APPID in the initialization code is the APPID that needs to be reported to the application.<br><br>* Check whether the channel channel is configured, iOS the general default App Store channel | |
|Is the data reporting address correct? |Confirm whether the data reporting address is configured correctly.<br><br><br>* Saas: use the default value | |
|(Optional)<br><br>Use full event tracking and other additional required checks |If you use real\-time event tracking or the circling function, you need to do the following verification:<br><br><br>* Check if the APPID is correct, including the appid in the handleurl and the initialized appid.<br><br>* Check **url_scheme** and **package names** are configured correctly | |


After the above inspection and verification, you can call the relevant APIs, such as user, event and other APIs to report

<span id="56f1165f"></span>
### 1.3.2 Integration verification

<span id="6ee56683"></span>
#### 1.3.2.1 Developer Tools Verification


1. Turn on the log switch during initialization, and you can see the Track Launch event related information in the output to prove that the sdk initialization was successful.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a55551025863490bbb7229ae5950365b~tplv-goo7wpa0wc-image.image" width="2784px" />   </div>
   

2. After reporting user data or event data, you can see the corresponding event in ouput to prove that the event and attributes were sent successfully.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b25b6671f10d47d5b27779d0ca698683~tplv-goo7wpa0wc-image.image" width="2466px" />   </div>
   


<span id="37cc8949"></span>
#### 1.3.2.2 DevTools validation event report

Function description: [event tracking developer tool](https://www.volcengine.com/docs/76880/1033592)

Access DevTools in the Debug environment, you can view the event tracking report status, debug log, configuration parameters and other information locally in real time.


|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae67682bea9d45e9bbcba8f173c77fc7~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c14e4969c2bb4956b9b5436a55f7de76~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba26cde22191470d9098414186de5eaa~tplv-goo7wpa0wc-image.image) </span> |
|---|---|---|


Reference to determine whether the local report is normal:


* The status in the information bar is Running, and there are SSID, BD_DID and other information

* Events in the event list exist and have been reported


<span id="08e1468f"></span>
#### 1.3.2.3 Event tracking verification function verification

Function description: [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification)

It needs to be integrated according to the relevant requirements of real\-time event tracking. When the integration is successful, in Data Management \- General Events, click Verify Event Tracking, and select Mobile End.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cf5b405abf34130a99ad5a25d76d303~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


After scanning the code, you will see the reported behavior data in real time. The left side is the real\-time behavior, and the right side is the attribute information of the corresponding behavior.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e29dec61e004ecc88605a8227bb36b0~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


<span id="96b3f285"></span>
#### 1.3.2.3 capture verification

Configure the packet capture tool, select the interface corresponding to the data reporting address to view the interface of the app_logevent_v3

Saas address: http://toblog.volceapplog.com

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c7bcdb1698d48a9b8896cc60574bb29~tplv-goo7wpa0wc-image.image" width="2942px" /></div>


<span id="37117966"></span>
## 1.4 Mini Program SDK (WeChat Mini Program as an example)

<span id="63be4ed5"></span>
### 1.4.1 Check item validation


|**Check item** |**Inspection precautions** |**Reference documentation** |
|---|---|---|
|Is the SDK introduced? |* Verify whether the SDK is installed.<br><br>   You can check whether there is an sdk\-mp file in the dependencies in the Mini Program package.json, if there is any proof that the sdk was successfully introduced.<br><br>* Whether to add the data reporting address to the "request legal domain name" in the background of the Mini Program<br><br>* Check if initialization code is introduced in the app.js file | |
|Is the APPID correct? |Check whether the APPID in the initialization code is the APPID that needs to be reported to the application. ||
|Is the data reporting address correct? |Confirm whether the data reporting address is configured correctly.<br><br><br>*  ||


After the above inspection and verification, you can call the relevant APIs, such as user, event and other APIs to report

<span id="6edf4c3c"></span>
### 1.4.2 Integration verification

<span id="232eb9b6"></span>
#### 1.4.2.1 Power builder verification


1. The integration has completed the compilation. In the debugger Console, you see the following information to prove that the sdk initialization was successful.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19762b64f9114cd581f60d7880df77d1~tplv-goo7wpa0wc-image.image" width="2448px" />   </div>
   

2. Verify that there is a list interface reported in the debugger network, and the status code is 200

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72ccaaac3f484657acf0855cf192d046~tplv-goo7wpa0wc-image.image" width="2586px" />   </div>
   

3. When clicking the code event tracking button, the corresponding event tracking event will be triggered. You can find the list? tea interface in the network to view the specific information of the event. If the status code is 200, it proves that the event was reported successfully.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/491deb7f87584af4b7b4bd877bb7e55c~tplv-goo7wpa0wc-image.image" width="2746px" />   </div>
   


<span id="5a1f1fba"></span>
#### 1.4.2.2 Real machine verification can be monitored or captured through real\-time event tracking

Function description: [Event Tracking Real-Time Verification](https://docs.byteplus.com/docs/DataFinder/Event_Tracking_Real-Time_Verification).

It needs to be integrated according to the relevant requirements of real\-time event tracking. When the integration is successful, in Data Management \- General Events, click Verify Event Tracking, select WeChat Mini Program, and upload the Mini Program code according to the instructions.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cf5b405abf34130a99ad5a25d76d303~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


After scanning the code, you will see the reported behavior data in real time. The left side is the real\-time behavior, and the right side is the attribute information of the corresponding behavior.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68979e35fdde4741b8aa001758282fbe~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


<span id="2616879f"></span>
#### 1.4.2.3 DevTools validation event report

Function description: [event tracking developer tool](https://www.volcengine.com/docs/76880/1033592)

Through the Mini Program SDK event tracking power builder (DevTools component), the content and format of event tracking can be conveniently checked during the development stage. The tool provides functions such as environmental information viewing, initialization information status viewing, and event log viewing.


|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2ed7bf964744808a85f2d196ea9d8c7~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/888cc3e744454db0af9c1cff5ca83d5d~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f02b2e700d5145158c4230928b46d373~tplv-goo7wpa0wc-image.image) </span> |
|---|---|---|


Reference to determine whether the local report is normal:


* Init, send and other API calls, report the domain name and initialization status;

* Events in the event list have a reported status.


<span id="59b00456"></span>
## 1.5 Server level SDK (Java language)


|**Check item** |**Inspection precautions** |**Reference documentation** |
|---|---|---|
|SDK integration code configuration check |* Check the SDK integration code:<br><br>   * Is the integration mode configured correctly? Java SDK integration methods include HTTP mode . You need to check whether the configuration result of the mode configuration parameter datarangers.sdk.mode is correct.<br><br>   * Verify that the APPID is configured correctly.<br><br>   * Verify that the reporting address is configured correctly.<br><br>* Determine if the configuration is as expected by monitoring the startup log by looking at the startup log. Mainly focus on `sdkMode`, `domain`, `headers`and other configurations. |[Java SDK Integration](https://docs.byteplus.com/docs/DataFinder/Java_SDK_Integration) |
|Integrated result checking |* HTTP mode can enable Debug authentication, or use the curl command to verify, see details [HTTP Mode Debug Verification](https://docs.byteplus.com/docs/DataFinder/Java_SDK_Integration#f28d46fd). ||


<span id="ec0c987b"></span>
## 1.6 Http API

<span id="d5338b0a"></span>
### 1.6.1 Validate Basic Configuration Items

Verify that the configuration of the Appkey in the header is correct, do not write it as appid.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ff2bec06f8e47429a41662c08f11e66~tplv-goo7wpa0wc-image.image" width="1996px" /></div>


It needs to be configured as the following result:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d68b64868933420faae2cdb955ef6713~tplv-goo7wpa0wc-image.image) </span>

<span id="8272c8f1"></span>
### 1.6.2 check response message

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4e3fdaadc644cc09f7f39130a66c0b9~tplv-goo7wpa0wc-image.image" width="1758px" /></div>



* If the value of e in the response message is not 0, it means that the report was not successful.

* If the return is successful (e = 0), but the data is still not seen in the system, check the local_time_ms event timestamp:

   * Whether the time of the day is set, if it is the time of the day, the data can be seen in the system in real time;

   * If it is not on the same day and within the window period (within the past 7 days and within the next 24 hours), the data will not be seen until the next day. It is recommended to use the same\-day timestamp for testing when testing.

   * If the time is outside the window (7 days ago and beyond the next 24 hours), the data will not be stored.

   * If the time is outside the window period (7 days ago and more than the next 24 hours), and you want to report historical data or data outside the window period, you need to add is_history identification, local_time_ms can be seen in real time on the same day, not the next day of the day see


<span id="fb61383c"></span>
### 1.6.3 Common problem

**Q1: Error: get appid error**

The appkey is wrong, you need to fill in the correct appkey.

**Q2: Error: parse web/mp3 data error**

This error is written as a problem with the parameters of the body. Just check the body and refer to it normally.

```JSON
[{
    "user": {
        "user_unique_id": "useid1"
    },
    "header": {
        "app_name": "test031701",
        "ab_sdk_version": "24",
        "app_version":"1.0.1.2",
        "custom": {
              "public_prop222": "22222" 
        }
    },
    "events": [
        {
            "ab_sdk_version": "24",
            "event": "track11",
            "params": "{\"pay_real\":\"2990\", \"pro_type\":\"4\"}",
            "local_time_ms": 1656582814712
        }
    ]
}]
```


**Q3: For anonymous user scenarios, can the client side SDK be reported without integration?** 

No, for anonymous users, you need to report deviceID or bddid. These two IDs need to be generated by the integrated client side and then passed through to the server level.

<span id="e596a7d8"></span>
# 2. System data verification

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After completing the data access, you need to wait 10 to 15 minutes before verifying the system data.</div>



1. In Data Management \- General Events/Event Properties/User Properties, verify that the reported custom events and custom properties exist in the event list, event properties and user properties list.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4cf5b405abf34130a99ad5a25d76d303~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. User\-user detailed investigation, according to ssid or uuid query to see the specific behavior of the user, to see if the user exists, and whether there are behavioral events

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3651161a4654f90a899d31e5fd1cb97~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0f09079f2a04cb4b48a6bb3e377bf3d~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e27e53cf9554334a9a75586e74ec365~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

3. It can also be verified in Advanced Analysis\-Event Analysis, but it should be noted that if it is data transmitted on the same day, the date needs to be selected today when querying the data.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5723466842a34c45b411a3ac691d1393~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

4. When users can scrutinize or analyze the reported data, then the SDK integration and event reporting are successful.

5. If the user does not report successfully, you need to see whether to call the API that sets the user (user_unique_id). If you do not set user_unique_id then the user is anonymous.

6. If the list in the browser developer network shows success, but the system does not find certain events or event properties, you can check whether there are failed events and properties reported in Data Management \- Data Quality.


<span id="582f0aa5"></span>
# 3. Special scenario verification

<span id="0fcd3315"></span>
## 3.1 APP embedded H5 verification

Description: If you need to do the app embedded H5 to get through, you can do the following checks. If you don't need it, you can ignore it.

<span id="ccd647c3"></span>
### 3.1.1 Check item validation


* Does the H5 page integrate with JavaScript?

* After the H5 page integrates with JSSDK, whether the initialized Nataive parameter is true (Native: true before the 5.1.3 version, enable_native: true after the 5.1.3 version)

* Whether the mobile end integrates the sdk (ios, android) of the mobile end

* Whether to refer to the integration code of each end for integration in mobile end integration needs to do two things

   * Turn on the H5Bridge switch during initialization

   * configuration whitelist


<span id="77497982"></span>
### 3.1.2 Data validation


* When the data is connected, use the app to report the behavioral event data, and check whether the value of the platform field in the corresponding behavioral event is wap or ios/android through real\-time event tracking monitoring or bag grabbing tools:

   * If the WAP proves that the data is not connected, it needs to be checked accordingly.

   * If it is iOS/Android, it proves that the data is successfully connected.

* Real\-time event tracking monitoring and packet capture refer to the verification instructions of each end above

* Real\-time event tracking data reference

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a01795988872436baffd6a4a8dbd8b80~tplv-goo7wpa0wc-image.image" width="1133px" />   </div>
   

   Packet capture tool data reference:

   * Get through the reference (platform is android):

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d6c2b58cf4d4c35a9489aa03210962f~tplv-goo7wpa0wc-image.image" width="2220px" />      </div>
      

   * If the platform is not opened, it is wap.

      <div style="text-align: center">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b15dc3faca941e0af7253f0b69c13fd~tplv-goo7wpa0wc-image.image" width="1926px" />      </div>
      

* When the platform attribute of the real\-time event tracking monitoring or bag capture display behavior event is ios/android, you can check the corresponding user's behavior in the system\-user scrutiny to determine whether the platform is ios/android in this user behavior event, and see if the event tracking triggered by H5 and the event tracking triggered by mobile end are the same user. If these two verifications are successful, then it proves that the H5 data embedded in the app is successfully connected

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6f5dfd42f3a4db2ba4a108da75ecd8b~tplv-goo7wpa0wc-image.image" width="2576px" />   </div>
