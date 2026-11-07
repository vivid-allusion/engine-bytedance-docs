---
title: "Network monitoring has not reported"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Network_monitoring_has_not_reported"
---

<span id="45f56cfe"></span>
## Prerequisites

APMInsight network monitoring supports monitoring OkHttp network requests. Confirm that the project uses OkHttp for network requests.

<span id="c3212522"></span>
## The verification process


* Confirm that the **network analysis** module of the specified version is turned on, that the **network sampling rate** configuration is set, and that sampling is hit on the client side.

   **All features \> Platform management configuration \> SDK reporting configuration**

* Confirm that network monitoring is full sampling, or the URL is in the allowlist, or the URL is not in the blocklist.

   **All features \> Platform management configuration \> Network request settings**

* Confirm that network monitoring is enabled on the device

* Confirm that the code for initializing Okhttp is in the package specified in the allowlist (whiteList) of the above ApmPlugin.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/f719b5e3066647b29a34c4e656f038ea) </span>

* Confirm whether instrumentation for Okhttp network monitoring is successful

   After successful instrumentation, you can see the following logs.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/96d789296c194535bab77a68f8237e99) </span>

   You can see how the code changes after compilation.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/0aa764efa5924416b96916afb949a567) </span>

* Confirm device\-side network data reporting

   Set `builder.debugMode(true);` during initialization, then filter Logcat for the `ApmInsight:` keyword, and confirm that the `Receive:NetData` logs are present.

   ```Plain Text
   2020-11-17 11:47:36.778 13404-13404/com.example.apm.insight.demo D/ApmInsight: APM_INIT
   // Initialization completed
   2020-11-17 11:47:36.947 13404-13532/com.example.apm.insight.demo D/ApmInsight: APM_START
   2020-11-17 11:47:46.957 13404-13532/com.example.apm.insight.demo D/ApmInsight: FetchSetting:
   // Configuration retrieval completed
   2020-11-17 11:47:46.974 13404-13532/com.example.apm.insight.demo D/ApmInsight: FinalSetting:
   // Network monitoring data received
   2020-11-17 11:47:48.284 13404-13617/com.example.apm.insight.demo D/ApmInsight: Receive:NetData
   // On - device monitoring data sent
   2020-11-17 11:49:49.695 13404-13615/com.example.apm.insight.demo D/ApmInsight: Send:
       url:https://tbm.snssdk.com/monitor/collect/c/performance/ response:200
   ```
