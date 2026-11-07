---
title: "Viewing monitoring data"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Monitoring-01"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

Transit Router (TR) supports real\-time monitoring of metrics for TR instances, network instance attachments, inter\-region attachments, and bandwidth packages through Cloud Monitor.


* By [configuring alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center) for TR, you can be aware of metric exceptions in time and ensure stable business operation.

* For more about TR\-related monitoring metrics, see [Transit Router metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_TransitRouter) and [TR bandwidth package metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_TransitRouterBandwidthPackage).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin

IAM users may not be able to directly view monitoring data of the TR product. To view it, the IAM user should ensure the Cloud Monitor permission has been obtained. For procedure, see[ Why can't IAM users view monitoring data](https://docs.byteplus.com/en/docs/transitrouter/TransitRouter-instance-faq#why-cannot-an-iam-user-view-monitoring-data).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5Lit6L2s6Lev55Sx5Zmo5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the Transit Router console


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select the target project and region.

3. Click the **monitor** icon in the row of the target TR.

4. Switch tabs to view monitoring metric charts of the corresponding TR resources respectively.


<span id=".5bim5a695YyF5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the Bandwidth Package console


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/trbandwidthpkg/trbp).

2. In the top menu bar, select the target project.

3. Click the **monitor** icon in the row of the target bandwidth package.

4. On the monitoring data page, you can view the monitoring metric charts of the target bandwidth package.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the target bandwidth package is not associated with an inter\-region attachment, no monitoring data is collected for the bandwidth package.   </div>
   

<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
### View data via the Cloud Monitor console

For procedure, see [Viewing cloud product monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData): View monitoring metrics.
