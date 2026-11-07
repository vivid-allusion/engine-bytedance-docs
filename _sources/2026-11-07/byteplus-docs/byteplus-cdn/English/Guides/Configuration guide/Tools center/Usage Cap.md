---
title: "Usage Cap"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/usage-cap_en-us"
---

<span id="8e42d37e"></span>
## Overview

BytePlus CDN provides [Usage Cap](https://console.byteplus.com/cdn/cdn-bp/tools/consumption-limit). On this page, you can create usage cap policies for domains. In a policy, you need to specify the monitoring metric, statistic period, and usage threshold. Once the policy is created, CDN starts monitoring the usage of the domain. If the usage of the domain exceeds the threshold within a statistic period, CDN will disable the domain for a period of time to prevent continuous growth of usage. Within each statistic period, CDN disables the domain at most once. This feature is mainly applicable to scenarios where you need to strictly control CDN costs and prevent unexpected fees caused by traffic spikes or malicious attacks. This article introduces how to configure and use the Usage Cap feature.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24e019e34e914acc9309853a1240ca7e~tplv-goo7wpa0wc-image.image) </span>

In the policy, you can also specify the disable duration for the domain. When the disable period ends, CDN will re\-enable the domain. In addition, you can set an alert threshold for usage in the policy to receive notifications when usage reaches the alert threshold.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">During the domain disable period, you can manually enable your domain at any time.</div>


* <div data-tips="true" data-tips-type="tip">When the domain disable period ends, CDN cannot re\-enable your domain if any of the following conditions exist:</div>


   * <div data-tips="true" data-tips-type="tip">Your account is in arrears.</div>


   * <div data-tips="true" data-tips-type="tip">You modified the domain configuration during the disable period.</div>


   * <div data-tips="true" data-tips-type="tip">Other uncommon situations. These situations are not listed here one by one. If your scenario does not fall into the first two cases, but CDN still cannot enable your domain, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a>.</div>


* <div data-tips="true" data-tips-type="tip">For CDN, collecting metric data, analyzing data, and disabling domains all take a certain amount of time. Therefore, there may be a 15\-minute delay between the time when usage exceeds the threshold and the time when CDN disables the domain. During this period, the usage of the domain will still be billed.</div>



<span id="650b33e1"></span>
## Notifications

When a domain is disabled, re\-enabled, or its usage reaches the alert threshold, CDN sends corresponding notifications to you via email and internal message.

<span id="7e4ed96f"></span>
### Notification Content

The following are examples of the main content in the notifications:


* Under your BytePlus account xxxxxxxxxx /example ,Domain www.example.com was triggering the usage cap policy you configured.


<span id="28bbee5c"></span>
## Procedure


1. Open the [Usage Cap page](https://console.byteplus.com/cdn/cdn-bp/tools/consumption-limit).

2. Click **Create Policy** to create a usage cap policy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/560c2233b1e34f0ba21285a681448f5b~tplv-goo7wpa0wc-image.image) </span>


<span id="ee4503f5"></span>
## Configuration Description


|**Configuration** |**Description** |
|---|---|
|Domain Name |Indicates the domain to be monitored. You need to select a domain from the list. You can also enter a domain name. |
|Statistic Type |Indicates the data statistical method for monitoring metrics. This configuration has the following options:<br><br><br>* Peak Usage: Indicates using the peak data of the metric as the metric data within the statistic period. Applied to Bandwidth and QPS.<br><br>* Cumulative Usage: Indicates using the cumulative data of the metric as the metric data within the statistic period. Applied to Traffic and Request Count. |
|Statistic Period |Indicates the time granularity for statistical data. CDN calculates the domain usage separately for each statistic period. Within each statistic period, CDN calculates the domain usage for the current period every 5 minutes.<br><br><br>* If **Statistic Type** is **Peak Usage**, this configuration can only be **Every 5 minutes**.<br><br>* If **Statistic Type** is **Cumulative Usage**, the options for this configuration are **Hourly**, **Daily**, **Monthly**.<br><br><br>The first statistic period depends on the creation time of the policy or the re\-enable time of the policy (if it was previously disabled).<br><br>**Example**<br><br>Suppose you created a policy on August 12 at 09:22,<br><br><br>* You set **Statistic Type** to **Peak Usage**. In this case, since the statistic period is 5 minutes, the first statistic period is [09:20, 09:25) of the day, the next is [09:25, 09:30), and so on.<br><br>* You set **Statistic Type** to **Cumulative Usage** and **Statistic Period** to **Hourly**. In this case, the first statistic period is [09:00, 10:00) of the day, the next is [10:00, 11:00), and so on.<br><br>* You set **Statistic Type** to **Cumulative Usage** and **Statistic Period** to **Daily**. In this case, the first statistic period is [August 12 00:00, August 13 00:00), the next is [August 13 00:00, August 14 00:00), and so on.<br><br>* You set **Statistic Type** to **Cumulative Usage** and **Statistic Period** to **Monthly**. In this case, the first statistic period is [August 1 00:00, September 1 00:00), the next is [September 1 00:00, October 1 00:00), and so on. |
|Cap Threshold |Indicates the usage threshold, which must be an integer.<br><br><br>* If **Statistic Type** is **Peak Usage**, you can set usage thresholds for the following metrics:<br><br>   * Bandwidth: Indicates the bandwidth within the statistic period. The threshold range is 10Mbps\-100Tbps.<br><br>   * QPS: Indicates the user request QPS within the statistic period. The threshold range is 100\-1,000,000 QPS.<br><br>* If **Statistic Type** is **Cumulative Usage**, you can set usage thresholds for the following metrics:<br><br>   * Traffic: Indicates the traffic within the statistic period. The threshold range is 100MB\-10,000TB.<br><br>   * Request Count: Indicates the user request count within the statistic period. The threshold range is 10,000\-10,000,000,000.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">1GB=1,000MB, 1Gbps=1,000Mbps.</div><br> |
|Enforcement |Indicates the operation CDN performs on the domain when usage exceeds the threshold. Currently, this configuration can only be **Disable Domain**, which means CDN disables your domain. When the domain is disabled, CDN will send you a notification.<br><br>&nbsp;<br><br>Within a statistic period, CDN disables the domain at most once. If you modify the policy, the domain disable count will be reset.<br><br>&nbsp;<br><br>**Example**<br><br>&nbsp;<br><br>You set **Statistic Type** to **Cumulative Usage**, **Statistic Period** to **Monthly**, and **Enforcement Duration** to **1 Day**.<br><br>&nbsp;<br><br>At 09:25 on August 12, the domain was disabled by CDN because the cumulative traffic for the month exceeded the threshold, and was re\-enabled by CDN at 09:25 on August 13. After enabling, although the cumulative traffic for the month still exceeds the threshold, CDN will not disable the domain again within the month.<br><br>&nbsp;<br><br>Then, you updated the policy at 09:03 on August 15, adjusting **Enforcement Duration** to **3 Days**. At 09:05 on the same day, the domain was disabled by CDN again because the cumulative traffic for the month exceeded the threshold. |
|Enforcement Duration |Indicates the effective duration of the **Enforcement**.<br><br><br>* When **Enforcement** is **Disable Domain**, this configuration indicates the disable duration of the domain. When the domain disable period ends, CDN will re\-enable your domain and send you a [Notification](https://docs.byteplus.com/en/docs/18/84290#notifications).<br><br><br>This configuration has the following options: **1 Hour**, **12 Hours**, **1 Day**, **3 Days**, **Permanent**. |
|Alerting |Indicates whether you want to receive [Notifications](https://docs.byteplus.com/en/docs/18/84290#notifications) when metric data reaches the alert threshold you set. |
|Alert Threshold |This configuration appears when **Alerting** is enabled, representing a percentage of the cap threshold. When metric data reaches this percentage, CDN sends you a [Notification](https://docs.byteplus.com/en/docs/18/84290#notifications). You can set an integer threshold in the range of 10\-90.<br><br>&nbsp;<br><br>When domain usage reaches this threshold:<br><br><br>* If **Statistic Type** is **Peak Usage**, although the statistic period is 5 minutes, CDN sends at most one notification per hour.<br><br>* If **Statistic Type** is **Cumulative Usage**, CDN sends at most one notification within each statistic period.<br><br><br>If the domain is disabled or re\-enabled by CDN due to usage cap policy, or if the policy is updated, the notification count will be reset.<br><br>&nbsp;<br><br>**Example**<br><br><br>* You set **Statistic Type** to **Cumulative Usage**, **Statistic Period** to **Hourly**, **Cap Threshold** to 100MB, and **Alert Threshold** to 60%.<br><br>   * In the statistic period [13:00, 14:00), the cumulative traffic of the domain reached 62MB. However, CDN will not send you a notification again until 14:00.<br><br>* You set **Statistic Type** to **Peak Usage**, **Cap Threshold** to 100Mbps, and **Alert Threshold** to 60%.<br><br>   * During [13:05, 13:10), the bandwidth peak of the domain reached 62Mbps. Therefore, CDN sends you a notification at 13:10. However, CDN will not send you a notification again until 14:00.<br><br><br>During [13:55, 14:00), the bandwidth peak of the domain reached 62Mbps. Therefore, CDN sends you a notification at 14:00.<br><br><br>* During [13:05, 13:10), the bandwidth peak of the domain reached 62Mbps, and the bandwidth peak for every 5 minutes thereafter remained above 60Mbps until 15:10 of the day. In this scenario, CDN will send you notifications at 13:10, 14:00, and 15:00 respectively.<br><br><br>**Policy Update Example**<br><br>&nbsp;<br><br>You set **Statistic Type** to **Cumulative Usage**, **Statistic Period** to **Hourly**, **Cap Threshold** to 100MB, and **Alert Threshold** to 60%.<br><br><br>* At 13:05, the cumulative traffic of the domain within the current hour reached 62MB. Therefore, CDN sends you a notification at 13:05. At 13:08, you modified the policy, changing **Cap Threshold** to 200MB. At 13:15, the cumulative traffic of the domain within the current hour reached 190MB. Therefore, CDN sends you a notification at 13:15. |
