---
title: "Monitoring overview"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Cloud-Monitor-overview"
---

BytePlus provides a GPU Compute Service instance monitoring service with diverse metrics and visualized data display to reflect the running status of resources created. You can also customize metric thresholds and alert notifications to promptly acquire instance exception status. 

<span id="sVyJoUCc"></span>
## Obtain monitoring data through the ECS console

ECS supports basic monitoring and operating system monitoring functions including various monitoring metrics.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following tables describe how to view monitoring data for a single instance. You can also click the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Monitoring-dashboard">Monitoring Dashboard</a> to view operating system monitoring statistics for multiple instances.</div>



|Feature/Operation |Description |
|---|---|
|[Monitoring metrics of ECS instances](https://console.byteplus.com/cloud_monitor/docs?tabKey=metric&namespace=VCM_ECS) |Display instance information, such as the Chinese and English names, purpose, and description. |
|[View basic monitoring data](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data) |Monitor basic performance metrics of the instance, such as CPU, network, and disk. This feature can help you learn the overall load and resource consumption of instances. |
|[View monitoring data of operating systems](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data) |Monitor the operating system of the instance, including its CPU, memory, disk, network, and network interface. This can help you to obtain deeper and more accurate information about instance operations.<br><br> |
|[View TCP connection monitoring](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data) |Monitor the TCP connection state of the instance operating system. Monitoring metrics include TCP bytes sent/received and connection retransmission count for connections between local and remote IP addresses. This can help you timely detect the TCP connection state of the instance operating system. |
|[Manage process monitoring](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics) |Active internal processes within ECS instances are monitored in real time, including metrics such as CPU usage and memory usage. This allows you to learn the system resource consumption of processes and to timely identify resource\-intensive processes. |
|[View GPU monitor​ing data of instances](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |Only monitor the metrics of GPU instances, such as GPU utilization rate, GPU memory utilization rate, and GPU temperature. This can help you easily learn about instance information, such as GPU memory usage and GPU utilization rate.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details of supported specifications, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Heterogeneous-computing">heterogeneous computing</a>.</div><br> |
|[View RDMA monitoring data of instances](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |Only RDMA network metrics of GPU instances are monitored. Monitoring metrics include RDMA network inflow/outflow rate, the number of received/sent RDMA data packets, the number of RDMA network outbound/inbound suspended packets, and other metrics. This way, you can learn more RDMA network\-related information about instances.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details of supported specifications, please refer to <a href="https://docs.byteplus.com/en/docs/ecs/Heterogeneous-computing">heterogeneous computing</a>.</div><br> |


<span id="QcSLObFu"></span>
## Obtain monitoring data through the Cloud Monitor console

The Cloud Monitor console is the unified entry for monitoring data of all products. Here, you can view the monitoring data and alarm history for ECS instances in a more comprehensive manner. For details, refer to [What is Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor).


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor).

2. In the left\-side navigation pane, select "Cloud Service Monitor \> ECS".

3. View the alarm overview, distribution of resources, and the list of ECS instances.

   * Alarm overview:

      * Current number of alarms: Total alarms for all ECS instances, which are categorized into three alarm levels for fine\-grained statistics: "Critical", "Warning", and "Notice". For detailed information, click the number to go to the "Alarm History" page for the alarm history list.

      * Alarm strategy number: Total alarm strategies associated with all ECS instances, which are categorized into two strategy statuses for fine\-grained statistics: "Disabled" and "In alarm". For detailed information, click the number to go to the "Alarm strategy" page for the alarm strategy list.

   * Resource distribution quantity:

      A chart is used to display the resource distribution for performance data across different gradients.

   * The list of instance resources:

      * This list displays the name, status, and other basic information of ECS instances.

      * Click the target instance name to view the monitoring metric charts and associated alarm strategies.

         * Click tabs "BaseMonitor" and "OperateSystemMonitor" to view data of all monitoring metrics of the instance.

         * Click the "Alarm strategy" tab to view all associated alarm strategies of the instance. Enter the alarm strategy details to view the alarm history of this instance.


<span id="h09FjmpO"></span>
## View and configure alerts through the Cloud Monitor.

If you need BytePlus to send alert notifications when monitoring metrics reach specified thresholds, you can configure alert rules manually.


|Feature/Operation |Description |
|---|---|
|[Configuring metric-based alarms and monitoring](https://docs.byteplus.com/en/docs/ecs/Collecting-alerts-triggered-by-ECS-metrics) |Alarm templates (alarm strategies) for ECS instance CPU and disk resource usage are pre\-configured by default. You can enable them with one click to receive timely alerts about instance resource issues. |
|[Configure alarm strategies for ECS instances](https://docs.byteplus.com/en/docs/cloudmonitor/Using-Alarm-Center) |You can configure alarm strategies as needed to monitor more metrics. |
|[View alert records of ECS instances](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history) |You can view the alert records of ECS instances in the console to understand their abnormal metric trends. |


<span id="foTgXhhG"></span>
##
