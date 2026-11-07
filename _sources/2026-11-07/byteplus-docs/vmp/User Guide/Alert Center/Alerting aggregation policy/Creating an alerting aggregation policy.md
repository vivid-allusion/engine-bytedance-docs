---
title: "Creating an alerting aggregation policy"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Creating-alerting-aggregation-rules"
---

To prevent alert storms, where alerts are triggered frequently and a large number of alert notifications are generated in a short period, you need to configure an alert aggregation policy to define the aggregation interval and notification interval.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The new Alert Center is available. It provides comprehensive upgrades and optimizations for features such as notification policies, notification templates, aggregation policies, and suppression policies. We recommend configuring aggregation policies in the new <a href="https://console.byteplus.com/observe/alert/aggregate">Alert Center</a>.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The system has the default alert aggregation policy named default. The following table shows aggregation parameters for alerts at different levels.


|Alert Level |Aggregation interval |Repeat interval |
|---|---|---|
|P0 |1 minute |1 hour |
|P1 |3 minutes |2 hours |
|P2 |5 minutes |4 hours |


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

A root account and its IAM users can create up to five alert aggregation policies in total.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. On the left navigation bar, click **Alert center \> Alerting aggregation policy**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a97c0423cb4e434097f6fec65aff64e5.png) </span>

4. Click **Create** to configure an alert aggregation policy.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b231c8c75f77e4ad32f910812f02caec.png) </span>

   
   |**Parameter** |**Descriptions** |
   |---|---|
   |Aggregation policy name |Specify the name of the alert aggregation policy. |
   |Description |Specify the description of the alert aggregation policy. |
   |Alert policy |Configure the aggregation and notification intervals for alerts at different levels (P0, P1, and P2).<br><br><br>* **Aggregate dimension**: the dimension of alert aggregation. Only `__rule__` is available, which indicates **aggregation by rule**.<br><br>* **Group interval**: the policy check interval. The value is an integer. You can specify **minutes** and **seconds** of the aggregation interval.<br><br>   If a new alert is triggered during the aggregation interval, all alert notifications will be sent. Otherwise, no alert notification will be sent.<br><br>* **Repeat interval**: the interval between successive alert notifications after a rule is triggered. The value is an integer. You can specify the interval in minutes and seconds.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The aggregation interval must be less than or equal to the notification interval.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The aggregation interval and notification interval must be equal to or greater than 1 minute.</div><br><br><br><br>For example, if an alert rule specifies that a P1 alert will be triggered if the metric has exceeded the threshold for 2 minutes, and an alert aggregation policy specifies the P1 level alert, an aggregation interval of 5 minutes, and a notification interval of 30 minutes,<br><br>after an alert rule triggers an alert notification for the first time, the alert aggregation policy checks whether a new alert at the P1 level is triggered every 5 minutes within the current interval.<br><br><br>* The time when the first alert notification is triggered = The time when the first alert is triggered + Waiting time for VMP maintenance (30 seconds for P0 and 60 seconds for P1 and P2).<br><br>* If a new alert is triggered, an alert notification will be sent.<br><br>* If no new alert is triggered, no alert notification will be sent.<br><br>   * If no new alert is triggered for 30 consecutive minutes but unresolved alerts still exist, an alert notification will be sent. |
   

5. Click **Create** to complete the configuration.
