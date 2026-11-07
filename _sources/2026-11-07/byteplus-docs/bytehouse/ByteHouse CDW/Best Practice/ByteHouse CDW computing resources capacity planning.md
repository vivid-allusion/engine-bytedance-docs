---
title: "ByteHouse CDW computing resources capacity planning"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/computing-resources-capacity-planning"
---

This tutorial aims to provide recommended usage standards for computing resources in ByteHouse Cloud Data Warehouse, and to introduce how to monitor and adjust these resources according to these standards to ensure stable business operations.

<span id="140a0a98"></span>
# Recommended capacity standards

The main computational resources of ByteHouse Cloud Data Warehouse include: virtual warehouse, private server, local disk of the virtual warehouse, and more. When purchasing these computing resources for use, you need to monitor resource usage. If resource usage exceeds the risk threshold, the success rate of read and write operations will decrease. Therefore, it is recommended to set appropriate monitoring and alerting policies for resource usage, and promptly adjust the specifications of computing resources that are at risk threshold.

The following are the usage standards for each computing resource:


* **Core usage metric**: When using this computing resource, pay special attention to this metric. Metric data can be obtained in the **Tenant management** \> \*\*\*\* \*\*Cloud monitor \*\*module.

* **Recommended resource safety level**: The recommended safe threshold for resource usage.

* **Low risk threshold**: When resource usage reaches the low risk threshold, **pay close attention**, **mainly focus on usage trends** and **the success rate of your application's read/write operations**. If the threshold is triggered occasionally, continue monitoring; if the frequency is high (for example, if it occurs every day), you need to plan to expand the corresponding computing resources.

* **High\-risk threshold**: When resource usage reaches the high\-risk threshold, **immediate scaling is required** to prevent business loss.



|Resource type |Primary capacity metrics |Recommended resource threshold |Low risk threshold |High risk threshold |
|---|---|---|---|---|
|Virtual warehouse |CPU utilization |Consistently less than 70% |Meets one of the following conditions:<br><br><br>1. Higher than 80% for 10 minutes continuously<br><br>2. Higher than 70% for 30 minutes continuously |Meets one of the following conditions:<br><br><br>1. Higher than 90% for 10 minutes continuously<br><br>2. Higher than 80% for 30 minutes continuously |
||Memory utilization |Consistently less than 70% |Meets one of the following conditions:<br><br><br>1. Higher than 80% for 10 minutes continuously<br><br>2. Higher than 70% for 30 minutes continuously |Meets one of the following conditions:<br><br><br>1. Higher than 90% for 10 minutes continuously<br><br>2. Higher than 80% for 30 minutes continuously |
|Private server |CPU utilization |Consistently less than 60% |Meets one of the following conditions:<br><br><br>1. Higher than 70% for 10 minutes continuously<br><br>2. Higher than 60% for 30 minutes continuously |Meets one of the following conditions:<br><br><br>1. Higher than 80% for 10 minutes continuously<br><br>2. Higher than 70% for 30 minutes continuously |
||Memory usage |Consistently less than 60% |Meets one of the following conditions:<br><br><br>1. Higher than 70% for 10 minutes continuously<br><br>2. Higher than 60% for 30 minutes continuously |Meets one of the following conditions:<br><br><br>1. Higher than 80% for 10 minutes continuously<br><br>2. Higher than 70% for 30 minutes continuously |
|Virtual warehouse local disk |Disk utilization rate |Consistently less than below 70% |Meets one of the following conditions:<br><br><br>1. Higher than 80% for 10 minutes continuously<br><br>2. Higher than 70% for 30 minutes continuously |Meets one of the following conditions:<br><br><br>1. Higher than 90% for 10 minutes continuously<br><br>2. Higher than 80% for 30 minutes continuously |
||Disk IOPS (read) + Disk IOPS (write) |Total read/write IOPS, consistently less than 60% × min |Meets one of the following conditions:<br><br><br>1. For a continuous period of 10 minutes, the metric remains higher than 70% \* Min{1800 + 50 × capacity (GiB), 50000}.<br><br>2. For a continuous period of 30 minutes, the metric remains higher than 60% × Min{1800 + 50 × capacity (GiB), 50000}. |Meets one of the following conditions:<br><br><br>1. For a continuous period of 10 minutes, the metric remains higher than 80% × min<br><br>2. For a continuous period of 30 minutes, the metric remains higher than 70% × min{1800 + 50 × capacity (GiB), 50000 |
||Disk bandwidth (read) + disk bandwidth (write) |Total read/write bandwidth, consistently lower than 60% \* min{120 + 0.5 × capacity (GiB), 350}, in MB/s |Meets one of the following conditions:<br><br><br>1. For a continuous period of 10 minutes, the metric remains higher than 70% \* min{120 + 0.5 × capacity (GiB), 350}.<br><br>2. For a continuous period of 30 minutes, the metric remains higher than 60% \* min{120 + 0.5 × capacity (GiB), 350}. |Meets one of the following conditions:<br><br><br>1. For a continuous period of 10 minutes, the metric remains higher than 80% × min{120 + 0.5 × capacity (GiB), 350}.<br><br>2. For a continuous period of 30 minutes, the metric remains higher than 70% \* min{120 + 0.5 × capacity (GiB), 350}. |


<span id="c1ae6386"></span>
# Usage monitoring, alerting, and adjustment methods


1. All ByteHouse resource usage data is pushed to the BytePlus Cloud Monitor product. You can monitor it through the [BytePlus Cloud Monitor console](https://console.byteplus.com/cloud-monitor), or go to **Tenant management** \> \*\*Cloud monitor \*\*page in the ByteHouse Cloud Data Warehouse console.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25adeb4b07e547dbb4ccf911a3c8396c~tplv-goo7wpa0wc-image.image) </span>

2. Configure alert methods. You can configure settings in the ByteHouse Cloud Data Warehouse Console. For configuration details, see [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm). Meanwhile, you can configure alarm templates in the BytePlus Cloud Monitor Console by referring to the **ByteHouse Cloud Data Warehouse Version Preset Alert Template**. For operation details, see [Edit alarm templates](https://docs.byteplus.com/en/docs/cloudmonitor/Editing-an-alarm-template).

3. When the usage metric exceeds the threshold, you can refer to the adjustment methods in the table below and adjust the resources as needed.

   
   | |Rules |Adjustment method |
   |---|---|---|
   |Virtual warehouse |When the CPU usage rate or the CPU/memory usage rate triggers the risk threshold. |1. Scale up to a larger instance of the same type: for example, 2XL \> 3XL<br><br>2. Estimate the new size based on the recommended resource threshold after scaling\-up.<br><br><br>For expanding a virtual warehouse, please refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f). |
   ||Only the memory usage rate triggers the risk threshold. |1. Specification type adjusted to performance type: for example, 2XL \-\> 2XL_PLUS<br><br>2. Estimate the new size based on the recommended resource threshold after scaling\-up.<br><br><br>For expanding a virtual warehouse, please refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f). |
   ||CPU/memory usage rate fluctuates periodically, showing troughs and peaks over time. |In the ByteHouse Console, go to **Task center** \> **Create new task**, and create a virtual warehouse scaling task to enable scheduled elasticity. For operation details, see [Cron task](https://docs.byteplus.com/docs/bytehouse/docs-cron-task). |
   ||CPU and memory utilization rates may fluctuate due to varying workloads. |You can use the ByteHouse elasticity feature. For details, see [Load elasticity](https://docs.byteplus.com/docs/bytehouse/docs-virtual-warehouses#8ad22697). |
   |Private server |When CPU usage or memory usage triggers the risk threshold. |Scale up related resource specifications. For example, 32 Core 128 GiB \* 2 nodes \-\> 64 Core 256 GiB \* 2 nodes. For higher specifications, please contact the ByteHouse team.<br><br>To expand a private server, see [Scale up the private server](https://docs.byteplus.com/docs/bytehouse/private-server#45ff32e3). |
   |Local disk of the virtual warehouse |The disk space utilization rate triggers a risk threshold. |Expand the local disk of the virtual warehouse, with the size estimated to reach the recommended resources waterline after expansion.<br><br>To expand local disk capacity, please refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f). |
   ||Disk bandwidth (read + write) triggers risk threshold. |1. When the value is less than 350MB/s, you can manually expand the local disk of the virtual warehouse. To expand local disk capacity, please refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f).<br><br>2. When the throughput reaches 350MB/s, you may contact the ByteHouse team to request additional capacity. |
   ||Disk IOPS (read + write) triggers risk threshold. |1. When the local disk capacity of the virtual warehouse is less than 50,000, you can manually expand the local disk. To expand local disk capacity, please refer to [Edit virtual warehouse configuration](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse#2c35e58f).<br><br>2. To request additional expansion, contact the ByteHouse team when the count reaches 50000. |
