---
title: "Quick Start: Research and Development"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Quick-Start-Research-and-Development"
---

<span id="_1-概述"></span>
# 1. Overview

<span id="_1-1-为什么需要接入数据"></span>
## 1.1 Why do you need to access data?

When you want to conduct an experiment, you need to integrate the SDK and report metric events, and data access is also a prerequisite for starting the experiment.

DataTester provides a variety of access methods such as client side, Web side, and server side to meet various needs. The data access work is mainly completed by R&D personnel.

<span id="_1-2-接入说明"></span>
## 1.2 Access instructions

<span id="接入支持方式"></span>
### Access support method

(1) Client side SDK: Android SDK, iOS SDK, SDK of various frameworks (RN, flutter, uni\-app), Mini Program (WeChat, Alipay, ByteDance, etc.), JS SDK.

(2) Server side SDK: java, go, etc.

Description: If you need to report the metric data at the server side, you can also do event reporting through httpapi.

<span id="客户端sdk采集数据分类"></span>
### Client side SDK acquisition data classification


1. The first type, device data, is used to uniquely identify a device, especially when the user is not logged in to the app, we distinguish users by device.

2. The second type, behavioral data, that is, event tracking data. In the operation flow of user interaction, the application finds key events for event tracking. When the user triggers a key event, the application will hand over the event tracking to AppLog, which collects event tracking and reports it to the background.

3. The third type, user data. When a user logs into an account or switches accounts, or when the app collects other information about the user, the user information can be handed over to AppLog, which can be reported to the background for unified processing.


<span id="_2-集成准备及相关文档说明"></span>
# 2. Integration preparation and related documentation

<span id="_2-1-系统信息准备"></span>
## 2.1 System information preparation

<span id="_2-1-1-地址及账号信息"></span>
### 2.1.1 Address and account information

**Private deployment**

(1) System login address

(2) SDK reporting address

(3) Account passwords for each role

**SaaS**

(1) System login address

(2) Account passwords for each role

<span id="_2-1-2-应用信息"></span>
### 2.1.2 Application information

Click on the details after the application to get the "appid", "appkey", "URL Scheme" of the assigned application and the "appname" displayed in the list

<span id="_2-2-埋点及sdk准备"></span>
## 2.2 Event tracking and sdk preparation

(1) Designed business tracking scheme

(2) SDK at each end

All remote integration can be ignored. If you need to use offline integration, please contact the relevant students of ByteDance.

<span id="_2-3-集成相关文档说明"></span>
## 2.3 Integration related documentation

Data Formats: [Data Formats, Growth Analysis - BytePlus](https://www.volcengine.com/docs/6285/66211)

About Preset Events and Properties: [Preset Properties Summary Table - A/B Testing - BytePlus](https://docs.volcengine.com/docs/6285/108553?lang=en)

About ssid, uuid and device_id: [User Identity - A/B Testing - BytePlus](https://docs.volcengine.com/docs/6285/1208581?lang=en)

Error\-prone point description:


1. The data format does not conform to the specification

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22757e7af3e04dc999dbb5755b6e74ad~tplv-goo7wpa0wc-image.image) </span>

2. If you need to upload numeric type attributes, you need to note that you need to upload numeric type attributes in the code.

    &nbsp;


<span id="_3-sdk-client-side-integration-and-validation"></span>
# 3. SDK client side integration and validation

Description: SDK integration is divided into 3 steps

(1) Introduction of the SDK

(2) Initialize the SDK

(3) Calling SDK\-related APIs to implement related functions

<span id="_3-1-web-js-sdk"></span>
## 3.1 Web/JS SDK

Integration Documentation Reference: [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataTester/Web-JavaScript-SDK-Integration)

Integration Validation Reference: [Web/JS SDK Debugging and Data Validation](https://docs.byteplus.com/docs/DataTester/Web-JS-SDK-Debugging-and-Data-Validation)

<span id="_3-2-android-sdk"></span>
## 3.2 Android SDK

Integration Documentation Reference: [Android SDK Integration](https://docs.byteplus.com/docs/DataTester/Android-SDK-Integration)

Integration Validation Reference: [Android SDK Debugging and Data Verification](https://docs.byteplus.com/docs/DataTester/Android-SDK-Debugging-and-Data-Verification)

<span id="_3-3-ios-sdk"></span>
## 3.3 iOS SDK

Integration Documentation Reference: [iOS SDK Integration](https://docs.byteplus.com/docs/DataTester/iOS-SDK-Integration)

Integration Validation Reference: [iOS SDK Debugging and Data Validation](https://docs.byteplus.com/docs/DataTester/iOS-SDK-Debugging-and-Data-Validation)

<span id="_3-4-小程序-sdk"></span>
## 3.4 Mini Program SDK

<span id="_3-4-1-微信小程序"></span>
### 3.4.1 WeChat Mini Program

Integration Documentation Reference: [WeChat Mini Program SDK Integration (Universal)](https://docs.byteplus.com/docs/DataTester/WeChat-Mini-Program-SDK-Integration-Universal)

<span id="_3-4-2-字节跳动小程序"></span>
### 3.4.2 ByteDance Mini Program

Integration Documentation Reference: [ByteDance Mini Program SDK](https://docs.byteplus.com/docs/DataTester/ByteDance-Mini-Program-SDK)

<span id="_3-4-3-支付宝小程序"></span>
### 3.4.3 Alipay Mini Program

Integration Documentation Reference: [Alipay Mini Program SDK](https://docs.byteplus.com/docs/DataTester/Alipay-Mini-Program-SDK)

<span id="_4-服务端集成及验证"></span>
# 4. Server side integration and validation

<span id="_4-1-java-服务端sdk"></span>
## 4.1 Java server side sdk

Integration Documentation Reference: [Java SDK](https://docs.byteplus.com/docs/DataTester/Java-SDK)

Other server side SDK integration refer to this document: [Server Side SDK Overall Description](https://docs.byteplus.com/docs/DataTester/Server-Side-SDK-Overall-Description)

<span id="_4-2-http-api（只做数据上报）"></span>
## 4.2 HTTP API (only for data reporting)

Integration Documentation Reference: [HTTP API](https://docs.byteplus.com/docs/DataTester/HTTP-API)

List interface body

```plain
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


JSON interface body

```plain
{
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
}
```
