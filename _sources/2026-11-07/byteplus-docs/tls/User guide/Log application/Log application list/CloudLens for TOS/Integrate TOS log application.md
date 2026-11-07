---
title: "Integrate TOS log application"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Integrate-TOS-log-application"
---

This topic describes how to integrate the CloudLens for TOS log application.

<span id="e200eabc"></span>
## Integrate the CloudLens for TOS log application

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">After the CloudLens for TOS log application is successfully created, modifying or canceling the integration is not supported.</div>


* <div data-tips="true" data-tips-type="default">You can enable the CloudLens for TOS log application in the Object Storage console, and then configure log analysis dashboards and data pivot dashboards.</div>


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, click **Common functions** \> **Log application**.

4. On the **App Store** tab, select the log application card to be integrated. For example, on the **CloudLens for TOS** card, click **Integrated Application**.

5. Follow the prompts on the page to confirm the following information, and then click **Submit**.

   
   |Parameters |Description |
   |---|---|
   |Billing instructions |After you integrate TOS access logs, TLS will charge based on storage space, read traffic, number of requests, data transformation, log shipping, and more. |
   |RAM authorization |Grant cross\-service access permissions. |
   

6. After successful integration, you can configure log analysis dashboards and data pivot dashboards as needed.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you integrate the log application, a data pivot dashboard named <code>default-account-dashboard</code> is automatically created. The details of this dashboard are as follows:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Billing item: No fees are charged.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Dashboard scope: All regions, all buckets.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Metric collection method: Free metrics (including summary metrics, cost optimization metrics, and data protection metrics).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Prefix aggregation: Not enabled.   </div>
   


<span id="6a284370"></span>
## Next steps

After integrating the CloudLens for TOS log application, you can configure log analysis dashboards and data pivot dashboards as needed.


* [Configure log analysis dashboards](https://docs.byteplus.com/docs/tls/Configure-log-analysis-dashboard)

* [Configure storage lens dashboards](https://docs.byteplus.com/docs/tls/Configure-pivot-dashboard)
