---
title: "Reference: iOS SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_iOS_SDK_Integration_FAQ"
---

<span id="9275f7ef"></span>
# SDK integration

<span id="f87a88f7"></span>
## iOS SDK's cache cleanup mechanism?

A: As of version 6.16.8, iOS has not had the ability to delete data expiration in the tob version of Rangers Applog. That is, cleaning outdated cache data is not currently supported.

<span id="45d1f1b0"></span>
## Does the iOS SDK conflict with the third\-party component OpenSSL standard library?

Answer: The new SM2 function after the iOS SDK upgrade 6.16.4 version introduces the openssl standard library, which may conflict with third\-party components. If you don't need to remove the SM2 function component, you can. If you must use the SM2 function, you can consider not using the pod integration, directly pull the corresponding integration product to access, delete the openssl dependency of one of xindun or Rangers Applog, and contact the students on the volcano side if none of the above can be solved.

<span id="f419ce1e"></span>
## Why do I need to remove the scheme package for the official launch? What is compliance risk?

A: The official launch version requires the offline scheme package. The scheme package contains injected code, and privacy compliance is risky.

<span id="e9e31391"></span>
## iOS will report a warning after integrating the sdk /RangersAppLog/BDAutoTracker/Classes/Core/Logger/RangersLogManager.m: 134 Thread running at User\-interactive quality\-of\-service class waiting on a lower QoS thread running at Utility quality\-of\-service class. Investigate ways to avoid priorit？

Answer:


1. The error originated from the log printing function enabled in Debug mode, causing resource contention between high\-priority threads (User\-interactive QoS) and low\-priority threads (Utility QoS), which is the expected behavior of the SDK in a specific debugging scenario.

2. When customers go online, the debug switch needs to be turned off, which should have no impact on their online.


<span id="fd16f4f2"></span>
## Integrated ios sdk encountered that onekit could not be pulled from pods, how to solve it?

Answer: Just delete the onekit subpackage directly.

<span id="5df61280"></span>
## iOS data reporting strategy

Answer: The SDK will not be cached locally without initialization. When to report:


* Report immediately when switching between the front and back of the app

* Profile request immediately

* After the SDK is started, it will be reported every 60s (up to 2,000 pieces each time. If more than 2,000 pieces are generated in one minute, you need to wait for the next 60s to report again)


<span id="f60c0d63"></span>
## Where iOS local cache stored? Is there any restriction on the SDK side?

Answer: The local cache is stored in SQLite, and the SDK has no restrictions, following the memory size limit of the mobile phone.

<span id="0e32402e"></span>
## iOS SDK supports iWatch watch OS

Answer: Not supported yet. If you need to use event tracking, you can consider using the HTTP API, refer to the documentation: [HTTP API](https://docs.byteplus.com/docs/DataFinder/HTTP_API).

<span id="4ff08cd6"></span>
## iOS client side can't receive the callback notification of ABTestSuccess after calling the pullABTestConfigs interface

Answer: Check whether the object listening for the notification is released when the notification is called back. If it is released, the notification will not be received.

<span id="1b5422f1"></span>
## If you call [BDAutoTrack allABTestConfigs] before BDAutoTrackNotificationABTestSuccess this callback, and then iterate through it one by one according to the Key, is the obtained AB value correct?

Answer: The API for obtaining the shunt result on the iOS end is the result obtained from the SDK cache area. For customers, it is only the value before and after the cache update. As for whether it is correct or not, it depends on whether the cache update has changed before.

<span id="e1d08259"></span>
# Abnormal reported data

<span id="4f7a2f4c"></span>
## iOS reporting event data real\-time event tracking, but the finder does not query the data of the drop library?

Answer:


1. Real\-time event tracking verification and data reporting are two different reporting channels, so the successful connection of real\-time event tracking verification does not mean the successful data reporting.

2. You can use the devtool tool to observe whether the status of an event is reported and query the data on the finder platform based on user_unique_id, ssid, or device_id in devtool.


<span id="c73fa302"></span>
# More FAQ

See the FAQ for more information on data access [SDK集成&数据上报](https://docs.byteplus.com/docs/undefined/663450cccb273002f1bb4b55).
