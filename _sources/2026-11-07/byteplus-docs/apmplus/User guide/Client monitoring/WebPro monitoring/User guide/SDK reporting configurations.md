---
title: "SDK reporting configurations"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configurations_webpro"
---

After the application integrates the SDK, the data sampled by the SDK will be reported according to the platform's default configuration values. The SDK reporting configuration feature allows you to configure the sampling of data reported by the SDK according to your own business needs. This article explains how to configure the sampling rate for each module.

<span id="ba7f2c57"></span>
## Background Information

After the SDK is integrated with the web service, when the SDK reports data, it not only uses the configuration specified in the integration code but also loads the configuration delivered by the platform. After completing the reporting configuration, updating the SDK's reporting configuration eliminates the need to update the SDK configuration or go through a series of complex steps such as publishing and going live.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the configuration is reported, it will take effect within 5 to 15 minutes after it is saved.</div>


<span id="5dce40df"></span>
## Modify the SDK reporting configuration


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **Client Monitoring**, then click the target application name, then click **Webpro Monitoring** under the target application.

4. In the upper left corner of the console, select **All features \> setting \> project setting**.

5. Under the **report configuration** module, modify the configuration of each module, then click **Save**.

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Type |Report type.<br><br>Includes basic configuration, JavaScript error, request monitoring, static resources monitoring, static resource error monitoring, custom monitoring, site performance, blank screen monitoring, long tasks, and user behavior.<br><br>The basic configuration is primarily used to configure the user allowlist. For more information, refer to [Configure allowlisted customers](https://docs.byteplus.com/en/docs/apmplus/project_setting#06462039). |
   |User sampling rate |The default user sampling rate for the WebPro client, that is, the reporting ratio. Example: 0.3 means 30% of users turn on reporting.<br><br><br>* The default user sampling rate for JavaScript error is`1`。<br><br>* The default user sampling rate for the request monitor is `0.5`.<br><br>* The default user sampling rate for the resources monitor is `0.5`.<br><br>* The default user sampling rate for static resource error monitoring is`1`。<br><br>* The default user sampling rate for custom monitor is`1`。<br><br>* The default user sampling rate for site performance is`1`。<br><br>* The default user sampling rate for blank screen monitoring is ...`1`。<br><br>* The default user sampling rate for long tasks is `0.01`.<br><br>* The default user sampling rate for user behavior is `0.01`. |
   |Rule sampling |Support setting sampling rate and select filter criteria.<br><br><br>* If multiple sampling rules are set at the same time, the rule with the higher priority will be matched first.<br><br>* If a reported data entry successfully matches the first rule and can be sampled, it will not be matched against the next rule.<br><br>* If the first rule fails to match, then match the next highest priority rule. and so on.<br><br>* If all rules fail to match, sampling and reporting will be performed according to the user's sampling rate configuration. |
