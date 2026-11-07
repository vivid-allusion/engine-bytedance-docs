---
title: "Viewing monitoring data"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Viewing_monitoring_data"
---

## Scenarios

NLB supports monitoring various business metrics of NLB instances and listeners in real time through CloudMonitor. By [configuring alarm strategies](https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center) for NLB, you can promptly identify metric exceptions to ensure stable business operation. For related monitoring metrics, see [NLB monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_NLB).

> **tip**

> CloudMonitor collects load balancer monitoring metric data every 30 seconds, and the data represents the average over those 30 seconds. For example, the new connections per second metric is displayed by CloudMonitor as the average number of new connections within 30 seconds.

## Prerequisites

An IAM user may not be able to directly view NLB monitoring data. To view it, ensure CloudMonitor permission has been authorized for the IAM user. For details, see [why an IAM user cannot view monitoring data?](https://docs.byteplus.com/en/docs/clb/NLB-instacnce-FAQs#.5Li65LuA5LmI5a2Q55So5oi35peg5rOV5p-l55yL55uR5o6n5pWw5o2u77yf).

## View in NLB console

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click the monitoring icon under the **monitoring** column of the target NLB.

4. Navigate between the Instance, Availability Zone, and Listener tabs to view their dedicated monitoring metrics as needed.

> **tip**

> If an instance is suspended or upgraded, NLB monitoring may show no data during that period; the monitoring metric chart will have no data points or lines for that time frame.

## View data via the Cloud Monitor console

For detailed steps, see [viewing NLB monitoring data](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-Cloud-Service-Monitor#.5p-l55yL5LqR5Lqn5ZOB55uR5o6n5pWw5o2u).

## Related documents

[GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData)
