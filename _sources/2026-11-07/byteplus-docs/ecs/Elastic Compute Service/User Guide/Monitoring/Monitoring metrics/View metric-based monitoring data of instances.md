---
title: "View metric-based monitoring data of instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-instance-monitoring-data"
---

You can go to the ECS console or Cloud Monitor console to view metric\-based monitoring data of instances. Monitoring metrics cover basic monitoring for instances, operating system monitoring, TCP connection monitoring, process monitoring, GPU monitoring, and RDMA monitoring.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The public images provided by BytePlus have the ECS monitoring plugin installed automatically. If you use an image provided by platforms other than BytePlus, you need to first install the plugin and complete the authorization in the instance. Then, you can view the operating system monitoring data. For more details, refer to the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1">Cloud Monitor overview</a>.</div>


<span id=".6YCa6L-H5LqR5pyN5Yqh5Zmo5o6n5Yi25Y-w6I635Y-W"></span>
## Obtain the monitoring data in the ECS console

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top navigation bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. Find the target instance through information such as instance name, ID, or tag.

   * Quick view on the Instances page:

      1. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_72648193f0b4d6e9b7adc0e3d02409e0.png) </span> icon in the "Monitoring" column of the target instance.

      2. In the pop\-up window on the right, you can click the [Basic monitor](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data), [Operating system monitor](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data), [TCP connection monitor](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data), [Process monitor](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics), [GPU monitor](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data), and [RDMA monitor](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) tabs to view instance metrics in different dimensions.

   * View the monitoring data on the instance details page:

      1. On the Instances page, click the name of the target instance.

      2. After you select the "Monitoring" tab, based on your needs, click the [Basic monitor](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data), [Operating system monitor](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data), [TCP connection monitor](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data), [Process monitor](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics), [GPU monitor](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data), or [RDMA monitor](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) tab. Then, you can view instance metrics in different dimensions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only for instances of the HPC\-optimized type, can you view metrics including "RDMA network outflow rate", "RDMA network inflow rate", "QP nums", and other metrics after selecting "Basic monitor \> Network". For detailed actions for instances of this type, refer to <a href="https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances">Creating HPC\-optimized instances</a>.   </div>
   

<span id=".55u45YWz5q2l6aqk"></span>
### Relevant operations

You can also [configure the alerts and monitoring of](https://docs.byteplus.com/en/docs/ecs/Collecting-alerts-triggered-by-ECS-metrics) or [create alarm strategies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) for the metrics. This helps you quickly detect instances in an abnormal state and ensure their normal operations.

<span id=".6YCa6L-H5LqR55uR5o6n5o6n5Yi25Y-w6I635Y-W"></span>
## Obtain the monitoring data in the Cloud Monitor console

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

         * Click tabs such as "BaseMonitor" and "OperateSystemMonitor" to view data for all monitoring metrics of the instance.

         * Click the "Alarm strategy" tab to view all associated alarm strategies of the instance. Enter the alarm strategy details to view the alarm history of this instance.
