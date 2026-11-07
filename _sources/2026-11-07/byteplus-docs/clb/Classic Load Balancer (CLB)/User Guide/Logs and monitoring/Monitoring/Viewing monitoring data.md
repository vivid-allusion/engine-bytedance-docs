---
title: "Viewing monitoring data"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Viewing-monitoring-data"
---

You can view the Classic Load Balancer (CLB) instance and listener monitoring data through the CLB console or the cloud monitor console. 

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The cloud monitor collects CLB monitoring metric data every 30 seconds, which is the average value of the CLB over 30 seconds. For example, New Connections Per Second is displayed by the cloud monitor as the average number of new connections in 30 seconds.</div>


* <div data-tips="true" data-tips-type="tip">IAM users cannot directly view the monitoring data of CLB. To view it, the root user of the IAM user must grant cloud monitor permission to the IAM user. For specific actions, please refer to <a href="https://docs.byteplus.com/en/docs/clb/Log-and-monitoring-faq#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf">Why can't IAM users view monitoring data</a>.</div>



<span id=".6LSf6L295Z2H6KGh5o6n5Yi25Y-w5p-l55yL"></span>
## View through CLB console


1. Log in to[ the CLB console](https://console.byteplus.com/clb/LoadBalancer). 

2. In the top menu bar, select the target region and target project.

3. Click the monitoring icon under the **monitoring** column of the target CLB instance.

4. Switch between the **Instance** and **Listener** tabs as needed to view their respective monitoring metrics.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If an instance is stopped or upgraded, CLB monitoring data may be unavailable, and no data points or lines are displayed in the monitoring metric chart during a period of time.   </div>
   

<span id=".5LqR55uR5o6n5o6n5Yi25Y-w5p-l55yL"></span>
## View monitoring data on the Cloud Monitor console

For detailed steps, refer to [Viewing CLB monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

<span id=".55u45YWz5paH5qGj"></span>
## Related document

[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData)
