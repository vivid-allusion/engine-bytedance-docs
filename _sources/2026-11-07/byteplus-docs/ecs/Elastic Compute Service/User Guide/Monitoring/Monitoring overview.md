---
title: "Monitoring overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Monitoring-overview"
---

BytePlus provides monitoring services for ECS instances. Comprehensive monitoring metrics, event\-based monitoring, and visualized data display help you track the running state of resources created. You can also customize metric thresholds, alert notifications, event monitoring rules, and other capabilities. This allows you to be timely informed when the instance has an exception and therefore to run your businesses stably.

<span id=".5oyH5qCH55uR5o6n"></span>
## Metric monitoring

ECS instances can be monitored based on various monitoring metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following table provides methods for you to view monitoring metrics for one instance. To view monitoring metrics of operating systems for multiple instances, go to the Cloud Monitor console.</div>



|Feature/Operation |Description |
|---|---|
|[Monitoring metrics of ECS instances](https://console.byteplus.com/cloud_monitor/docs?tabKey=metric&namespace=VCM_ECS) |Display the Chinese and English names, purposes, descriptions, and other information about ECS monitoring metrics. |
|[View basic monitoring data](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data) |Monitor basic performance metrics of the instance, such as CPU, network, and disk. This feature can help you learn the overall load and resource consumption of instances. |
|[View monitoring data of operating systems](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data) |Monitor the operating system of the instance, including its CPU, memory, disk, network, and network interface. This can help you to obtain deeper and more accurate information about instance operations. |
|[View TCP connection monitoring](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data) |Monitor the TCP connection state of the instance operating system. Monitoring metrics include TCP bytes sent/received and connection retransmission count for connections between local and remote IP addresses. This can help you timely detect the TCP connection state of the instance operating system. |
|[Manage process monitoring](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics) |Monitor active internal processes within the Elastic Compute Service (ECS) in real time, including metrics like CPU usage and memory usage, to understand the process's consumption of system resources and to timely identify processes with high resource consumption. |
|[View GPU monitor​ing data of instances](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |Only monitor the metrics of GPU instances, such as GPU utilization rate, GPU memory utilization rate, and GPU temperature. This can help you easily learn about instance information, such as GPU memory usage and GPU utilization rate. |
|[View RDMA monitoring data of instances](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |Only monitor the RDMA network metrics of GPU Compute Service (GPU) instances. Monitoring metrics include RDMA network inflow/outflow rate, the number of received/sent RDMA data packets, the number of RDMA network outbound/inbound suspended packets, and other metrics. This feature can help you learn RDMA network\-related information of instances. |


If you need the Cloud Monitor to send you alert notifications when the monitoring metrics reach the specified thresholds, you can configure alert rules yourself.


|Feature/Operation |Description |
|---|---|
|[Configuring metric-based alarms and monitoring](https://docs.byteplus.com/en/docs/ecs/Collecting-alerts-triggered-by-ECS-metrics) |Alarm templates (alarm strategies) for ECS instance CPU and disk resource usage are pre\-configured by default. You can enable them with one click to receive timely alerts about instance resource issues. |
|[Configure alarm strategies for ECS instances](https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center) |You can configure alarm strategies as needed to monitor more metrics. |
|[View alert records of ECS instances](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history) |You can view the alert records of ECS instances in the console to understand their abnormal metric trends. |


<span id=".5LqL5Lu255uR5o6n"></span>
## Event monitoring

ECS instances support event\-level monitoring. For details, refer to:


* [Event monitoring overview](https://docs.byteplus.com/en/docs/ecs/Event-monitoring-overview)

* [Query and handle events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events)

* [Event type overview](https://docs.byteplus.com/en/docs/ecs/Event-type-overview)

* [Configuring event monitoring notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications): If you need to receive alert notifications when a specified monitoring event is triggered in an instance, you can configure event alert rules and notification channels.


<span id=".5a6e5L6L5YGl5bq354q25oCB55uR5o6n"></span>
## Instance health state monitoring

The monitoring feature for instance health state automatically detects the software and hardware running information of the instance, calculates the health state of the instance in summary, and helps you quickly understand the instance's health state through the console. For details, refer to [Viewing instance health status](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-health-status).
