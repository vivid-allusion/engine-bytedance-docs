---
title: "Monitoring Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Monitoring-overview"
---

TOS provides various channels of monitoring data including cloud monitoring and cloud auditing, making it easy for you to grasp the status and usage of Buckets. This document introduces the monitoring methods and monitoring data supported by TOS.

<span id="a74d0d5c"></span>
## Precautions

Bucket names are globally unique. If a bucket is deleted and then recreated with the same name, the monitoring and alert rules of the deleted bucket will be applied to the new bucket of the same name.

<span id="20fc77c5"></span>
## Description of the Indicator


* For the monitoring metrics supported by TOS, please see [Monitoring Indicator Description](https://docs.byteplus.com/docs/tos/Monitoring-indicator-description).

* The event metrics supported by TOS, please refer to [Flow Control Event Metrics Description](https://docs.byteplus.com/docs/tos/Flow-control-event-metrics-description).


<span id="cfe5af97"></span>
## Alert Service


* If you need to monitor the data status of TOS resources, you can create a cloud monitoring alert policy. When the monitored cloud product resources meet the trigger conditions for an alert, the system will send notifications through your specified method, making it easy to detect resources with abnormal data promptly. For more details, please see [Alarm mechanism](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-mechanism) and [Set Metric Alerts](https://docs.byteplus.com/docs/tos/Set-metric-alerts).

* If you need to monitor events related to TOS, you can create event alert rules. When TOS events occur, the system will push alert notifications in the way you have specified, making it easy to promptly detect abnormal events. For more details, please refer to [Set Event Alerts](https://docs.byteplus.com/docs/tos/Set-event-alerts).


<span id="d4146272"></span>
## Monitoring Data Retention Period

For the retention period of monitoring data in object storage, please see [Cloud service metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics). Data will be automatically deleted after expiration.

<span id="d615826f"></span>
## Access Monitoring Data

You can obtain TOS\-related monitoring data via the API or SDK provided by Cloud Monitoring. For details, please refer to [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData).

&nbsp;
