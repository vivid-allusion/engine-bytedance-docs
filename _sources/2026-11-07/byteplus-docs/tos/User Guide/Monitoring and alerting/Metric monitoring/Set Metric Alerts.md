---
title: "Set Metric Alerts"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-metric-alerts"
---

You can set alert policies for TOS based on your business needs. When monitored metrics exhibit abnormalities, the system sends notification alerts in your specified manner to help you promptly identify any exceptional metrics. This article explains how to set metric alert policies.

<span id="2a68a188"></span>
## Precautions

TOS has certain limitations on performance attributes like bandwidth and QPS. It is advisable to set alert policies based on these limitations and your business conditions to avoid business impacts due to rate limiting. For details on restrictions, please see [Restrictions](https://docs.byteplus.com/docs/tos/docs-restrictions)

<span id="7c8affbf"></span>
## Prerequisites

For prerequisites to setting alert policies, please see [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

<span id="132a2f9e"></span>
## Procedure


1. Log in to [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left\-side navigation pane, select **Alarm Center** \> **Alarm strategy**.

3. On the **Alarm strategy** page, click **Create alarm strategy**.

4. On the **Create alarm strategy** page, select **Resource type** as **Storage \> TOS**, set the alert parameters. Key parameter descriptions are as follows:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">TOS supports setting alert policies based on <strong>Bandwidth</strong>, <strong>QPS</strong>, <strong>Storage</strong>, <strong>Bucket Status Code</strong>, and <strong>account dimension</strong>. For details on other parameters, please see <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Create Alert Policy</a>.   </div>
   

   
   |Parameters |Description |
   |---|---|
   |**Alarm object** ||
   |Resource type |Select **TOS**. |
   |Subnamespace |TOS supports setting alarm policies based on dimensions such as **Bandwidth**, **QPS**, **Storage**, **Bucket Status Code**, and **account dimension**. |
   |Resource |Select the bucket for which you wish to set alarm rules. |
   |**Alarm Rules** ||
   |Metric Type |Select Metric Type, supporting the choice of **Single metric** or **Multiple metrics**. If you need to monitor multiple metrics of a resource, you can configure multiple metric types directly. |
   |Trigger Conditions |For details on monitoring metrics supported by TOS, please see [Monitoring Metrics Description](https://docs.byteplus.com/en/docs/tos/Monitoring-indicator-description). Common trigger conditions are as follows:<br><br><br>* **The proportion of 2XX status codes < 90%** : indicates that the success rate of requests may be below 90%.<br><br>* **The proportion of 5XX status codes \> 0%** : indicates that there may be errors on the server side.<br><br>* **Request count of 429 status codes \> 0**: indicates that the business might trigger flow control.<br><br><br>We recommend you set specific triggering conditions based on actual business circumstances. |
   

5. Once the settings are complete, click **Create**.


&nbsp;
