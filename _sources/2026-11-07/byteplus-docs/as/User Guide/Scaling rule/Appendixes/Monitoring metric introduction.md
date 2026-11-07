---
title: "Monitoring metric introduction"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Metrics"
---

This topic describes the monitoring metrics supported by AS alert tasks. The alert task feature is integrated with [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/Release-notes). This enables scaling operations to be performed automatically when thresholds of monitoring metrics are reached, ensuring stable business operations.

The Auto Scaling service provides a wide range of monitoring metrics for ECS instances based on basic monitoring, operating system monitoring, and GPU card monitoring. Details are listed below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To retrieve metrics for operating system monitoring and GPU card monitoring, you need to install the Agent plugin and complete authorization on the instance first. Otherwise, the metrics cannot be retrieved. For installation instructions, refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1">ECS monitoring overview</a>.</div>


<span id=".5Z-656GA55uR5o6n5oyH5qCH"></span>
## Basic monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cloud Monitor collects basic monitoring metrics every 60 seconds. Collected data reflects the maximum, minimum, and average values of the instance metrics over every 60 seconds.</div>



|Monitoring metric name |Unit |Metric description |
|---|---|---|
|Maximum out\-of\-band CPU utilization |% |Maximum CPU usage of all instances in a scaling group |
|Minimum out\-of\-band CPU utilization |% |Minimum CPU usage of all instances in a scaling group |
|Average out\-of\-band CPU utilization |% |Average CPU usage of all instances in a scaling group |
|Average out\-of\-band network outbound rate |bits/s |Average network inbound rate of all instances in a scaling group |
|Average out\-of\-band network inbound rate |bits/s |Average network outbound rate of all instances in a scaling group |
|Average out\-of\-band network packet sending rate |bits/s |Average inbound intranet traffic rate of all instances in a scaling group |
|Average out\-of\-band network packet receiving rate |bits/s |Average outbound intranet traffic rate of all instances in a scaling group |


<span id="nPlzjmqO"></span>
## Operating system monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Cloud Monitor collects operating system monitoring metrics every 30 seconds. Collected data reflects the maximum, minimum, and average values of the instance metrics over every 30 seconds.</div>


* <div data-tips="true" data-tips-type="tip"><strong>System volume\-related metric description</strong>: If the image of the instances in your scaling group is a custom image or if the latest version of the monitoring plugin is not installed on them, an alert task for related metrics may not run properly.</div>




|Monitoring metric name |Unit |Metric description |
|---|---|---|
|Maximum CPU usage |% |Maximum CPU usage of all instances in a scaling group |
|Minimum CPU usage |% |Minimum CPU usage of all instances in a scaling group |
|Average CPU usage |% |Average CPU usage of all instances in a scaling group |
|Maximum memory usage |% |Maximum memory usage of all instances in a scaling group |
|Minimum memory usage |% |Minimum memory usage of all instances in a scaling group |
|Average memory usage |% |Average memory usage of all instances in the scaling group |
|Average system volume read bandwidth |B/s |Average read bandwidth of system volumes of all instances in a scaling group |
|Average system volume write bandwidth |B/s |Average write bandwidth of system volumes of all instances in a scaling group |
|Average system volume read IOPS |Count/s |Average read IOPS of system volumes of all instances in a scaling group |
|Average system volume write IOPS |Count/s |Average write IOPS of system volumes of all instances in a scaling group |
|Average number of TCP connections |count |Average number of TCP connections of all instances in a scaling group (including TCP connections in states such as ESTABLISHED, LISTEN, TIMEWAIT, SYNSENT, and SYNRECV) |
|Maximum GPU usage |% |Maximum GPU usage of all instances in a scaling group |
|Minimum GPU usage |% |Minimum GPU usage of all instances in a scaling group |
|Average GPU usage |% |Average GPU usage of all instances in a scaling group |
|Maximum GPU memory usage |% |Maximum GPU memory usage of all instances in a scaling group |
|Minimum GPU memory usage |% |Minimum GPU memory usage of all instances in a scaling group |
|Average GPU memory usage |% |Average GPU memory usage of all instances in a scaling group |
