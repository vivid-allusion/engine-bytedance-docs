---
title: "SDK reporting configuration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration_minipro"
---

After the application integrates the SDK, the data sampled by the SDK will be reported according to the default values in the platform configuration. The SDK reporting configuration feature allows you to configure data sampling for SDK reporting according to your business requirements. This document describes how to perform sampling rate configuration for each module.

<span id="5177a017"></span>
## Background Information

After the mini program integrates the SDK, when the SDK reports data, it uses the configuration in the integration code and also loads the configuration delivered by the platform. After completing the reporting configuration, updating the SDK's reporting configuration means you do not need to update the SDK configuration, release, go live, or go through a series of other complicated processes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once configuration reporting is complete, the configuration will take effect within 5 to 15 minutes after saving.</div>


<span id="53d7dc1f"></span>
## Modify the SDK setting


1. Log in to the [Application Performance Management Plus console](https://console.byteplus.com/observe/apmplus-client).

2. On the top navigation bar, select the target region.

3. In the left\-side menu, select **client Monitoring**, then click the target application name, and under the target application, click **Mini Program Pro Monitoring**.

4. In the upper left corner of the console, select **All features \> Settings \> Project settings**.

5. In the **submit configuration** area, modify the configuration of each module, then click **Save**.

   
   |**Parameter** |**DescriptionS** |
   |---|---|
   |Type |The report type.<br><br>Includes basic configuration, JavaScript error, request monitor, custom monitor, performance monitor, and setData.<br><br>The basic configuration is primarily used to configure the user allowlist. For more information, refer to [Configure allowlist customers](https://docs.byteplus.com/en/docs/apmplus/project_setting_minipro#78955ead). |
   |User sampling rate |The default user sampling rate of Mini Pro Monitoring, that is, the reporting ratio. Example: 0.3 indicates that 30% of users turn on reporting.<br><br><br>* The default user sampling rate for JavaScript error is`1`。<br><br>* The default user sampling rate for request monitor is`1`。<br><br>* The default user sampling rate for the custom monitor is`1`。<br><br>* The default user sampling rate for performance monitor is`1`。<br><br>* The default user sampling rate for setData is `0.01`. |
   |Rule sampling |Supports setting the sampling rate and selecting filter criteria.<br><br><br>* If multiple sampling rules are set at the same time, the rule with the highest priority will be matched first.<br><br>* If a reported data item successfully matches the first rule and is sampled, it will not be evaluated against the next rule.<br><br>* If the first rule does not match, match the next rule in priority order. And so on.<br><br>* If all rules fail to match, sampling and reporting are performed according to the user's sampling rate configuration. |
