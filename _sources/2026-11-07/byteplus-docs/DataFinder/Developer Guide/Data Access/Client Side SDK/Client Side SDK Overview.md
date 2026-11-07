---
title: "Client Side SDK Overview"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Client_Side_SDK_Overview"
---

BytePlus Growth Analysis provides a variety of client side SDKs for easy access to your data.

<span id="_1-sdk支持范围"></span>
# 1. SDK support scope

<span id="客户端sdk"></span>
## Client side SDK


| |**Native client side** |||||**Mobile end framework** ||||||
|---|---|---|---|---|---|---|---|---|---|---|---|
|**SDK Features** |Android |iOS |Web JS |Mini Program |Windows（C++） |Flutter |React Native |Weex |uni\-app |Unity |Cordova |
|Data collection and event tracking |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |
|A/B Experiment (Tester) |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |✅ |
|Full event tracking |✅ |✅ |✅ |✅ | |✅ |✅ | | | | |
|visual circling |✅ |✅ |✅ | | | |✅ | | | | |
|Compliance delayed initialization |✅ |✅ |✅ |✅ | |✅ |✅ | | | |✅ |


<span id="服务端sdk"></span>
## Server level SDK


|Server level language |Support Notes |
|---|---|
|Java |✅ |
|PHP |✅ |
|Python |Privatization support only |
|Golang |✅ |


<span id="_2-sdk常用功能汇总"></span>
# 2. Summary of common functions of SDK


|Function |Function Description |Android |iOS |Web |Mini Program |
|---|---|---|---|---|---|
|Preset events and properties |Including app activation, launch, exit, etc.,[Preset Property Summary Table](https://docs.byteplus.com/docs/DataFinder/Preset_Property_Summary_Table) |✅ |✅ |✅ |✅ |
|custom event |Custom code event tracking |✅ |✅ |✅ |✅ |
|Full event tracking |Page visits, clicks, exposures, and other events |✅ |✅ |✅ |✅ |
|Real\-time event tracking verification |Real\-time view of event tracking for Debug |✅ |✅ |✅ |✅ |
|Crash event collection |App crash event |✅ |✅ | | |
|ad monitoring |Advertising monitoring capabilities |✅ |✅ | | |
|Full link monitoring |Monitor various metrics of the SDK runtime |✅ |✅ | | |
|SDK acquisition switch |Control whether the SDK is turned on or off | | |✅ |✅ |
|Event tracking blacklist |After the server level (event tracking interface) issues the blacklist event list, the client side will not report all events in the blacklist list. For configuration, please contact technical support. |Privatization support<br><br>SDK6.13.0 + and later versions support |Privatization support<br><br>SDK6.13.0 + and later versions support | | |
|multiple instances |Support different AppIDs to create different SDK instance objects and report to different environments. |✅ |✅ | | |


<span id="_3-devtools调试工具说明"></span>
# 3. DevTools debugging tool description


|Debugging function |Function Description |Android |iOS |Web |Mini Program |
|---|---|---|---|---|---|
|SDK access status |Support to check whether the SDK initialization status and SDK core logic are normal |✅ | |✅ |✅ |
|Initialization parameters, public parameters |Support viewing the parameters of the initialization SDK (including various switches), dynamically configured parameters, public parameters (including collected device information and sensitive data), etc |✅ |✅ |✅ |✅ |
|service configuration |Support real\-time view of device ID, server level configuration, user hit AB test configuration, etc |✅ |✅ |✅ | |
|Event tracking list |Support real\-time viewing of the collected event tracking list and status (including whether it was successfully reported) and event tracking parameters |✅ |✅ |✅ |✅ |
|Event tracking pre\-check |Support to check whether the event tracking name and parameters comply with the reporting rules (including the Finder's event configuration) |✅ | | | |
|SDK run log |Support real\-time viewing of the logs printed by the SDK runtime, and support one\-click export |✅ |✅ |✅ |✅ |
|network packet capture |Support real\-time viewing of information such as request volume and response body content of network requests |✅ | |✅ | |


<span id="_4-各端集成文档"></span>
# 4. Integrated documentation at each end


* iOS end:[(Legacy Documentation)iOS SDK Integration](https://docs.byteplus.com/docs/DataFinder/Legacy_Documentation_iOS_SDK_Integration)

* Android:

   * [Android SDK Integration](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Integration_)

   * [Android SDK Event Tracking and Properties](https://docs.byteplus.com/docs/DataFinder/Android_SDK_Event_Tracking_and_Properties)

* Web/JS SDK：[Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_)

* Mini Program SDK:

   * WeChat Mini Program SDK: [WeChat Mini Program SDK Integration](https://docs.byteplus.com/docs/DataFinder/WeChat_Mini_Program_SDK_Integration)

   * ByteDance Mini Program SDK: [ByteDance Mini Program SDK Integration](https://docs.byteplus.com/docs/DataFinder/ByteDance_Mini_Program_SDK_Integration)

   * Alipay Mini Program SDK: [Alipay Mini Program SDK Integration](https://docs.byteplus.com/docs/DataFinder/Alipay_Mini_Program_SDK_Integration)

* WeChat official account data access: [(不发布,海外无该功能)WeChat official account data access](https://docs.byteplus.com/docs/undefined/6a4ce36a45b03c05520aff29)

* App third\-party frameworks:

   * Flutter：[Flutter SDK Integration and Event Tracking](https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration_and_Event_Tracking)

   * Cordova：[Cordova SDK Integration and Event Tracking](https://docs.byteplus.com/docs/DataFinder/Cordova_SDK_Integration_and_Event_Tracking)

   * React Native：[React Native SDK Integration and Event Tracking](https://docs.byteplus.com/docs/DataFinder/React_Native_SDK_Integration_and_Event_Tracking)
