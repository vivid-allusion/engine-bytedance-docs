---
title: "Monitoring and alarm"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/monitoring-and-alarm"
---

<span id="c2ada7cb"></span>
# Monitoring metric description

The monitoring and alarm function of ByteHouse Cloud Data Warehouse provides multiple types of monitoring, including virtual warehouse, keys and licenses, task center, storage, connections, dedicated server, and virtual warehouse local disk. The monitoring metrics for each category are shown in the table below.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For ease of display, the monitoring alarm charts will automatically adjust the unit of magnitude based on the data volume, and the display is the final reference. For example, when the replication delay is significant, the unit will be adjusted from µs to ms; when the replication delay is even greater, it will be adjusted from ms to s.</div>


* <div data-tips="true" data-tips-type="tip">You can use the <a href="https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData">GetMetricData</a> interface to query various monitoring metrics and alarm information. When calling the query interface, it is necessary to obtain the product's Namespace, the SubNamespace to which the metric to be queried belongs, and the MetricName. The Namespace for ByteHouse Cloud Data Warehouse Edition is <strong>VCM_ByteHouse</strong>, and the MetricName and SubNamespace for each metric are as shown in the table below.</div>


* <div data-tips="true" data-tips-type="tip">You can also obtain detailed information on each monitoring metric at <a href="https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_ByteHouse&tabKey=metric">ByteHouse Cloud Data Warehouse Edition Monitoring Metrics Query</a>.</div>


* <div data-tips="true" data-tips-type="tip">You can also use the SDK to query various monitoring metric data, see <a href="https://docs.byteplus.com/docs/bytehouse/cdw-query-bytehouse-monitoring-data-using-sdk">Query ByteHouse monitoring data using SDK</a>.</div>




|**Category** |**Metric Name** |**MetricName** |**SubNamespace** |**Metric Dimensions** |**Metric Units** |**Metric Purpose** |**Metric Description** |
|---|---|---|---|---|---|---|---|
|Virtual Warehouse |CPU Utilization |VirtualWarehouse_CPU_Usage_Percentage |VirtualWarehouse |ResourceID,VWID,Pod(Optional) |Percent |Alarm, Consumption |Current CPU usage as a percentage of requested resources |
|Virtual Warehouse |Memory occupancy (RSS) |VirtualWarehouse_Memory_Usage_Percentage |VirtualWarehouse |ResourceID,VWID,Pod(Optional) |Percent |Alarm, Consumption |Current memory usage (RSS) as a percentage of requested resources |
|Virtual Warehouse |Queries Per Second (QPS) |VirtualWarehouse_Query_Per_Second |VirtualWarehouse |ResourceID,VWID |Count/Second |Alarm, Consumption |Average number of queries of all types processed per second in 5 minutes |
|Virtual Warehouse |Query P95 Latency |VirtualWarehouse_Query_P95_Latency |VirtualWarehouse |ResourceID,VWID |Millisecond |Alarm, Consumption |The fastest 95% average latency among currently executing queries |
|Virtual Warehouse |Query Success<br><br>Ratio |VirtualWarehouse_Query_Success_Percentage |VirtualWarehouse |ResourceID,VWID |Percent |Alarm, Consumption |Proportion of queries successfully executed within 5 minutes |
|Virtual Warehouse |Slow Queries (longer than 10s) |VirtualWarehouse_Query_Slow_Queries |VirtualWarehouse |ResourceID,VWID |Count |Alarm, Consumption |The number of queries that have been executed for more than 10 seconds |
|Virtual Warehouse |Default Query QPS |VirtualWarehouse_Query_Per_Second_Default |VirtualWarehouse |ResourceID,VWID |Count/Second |Alarm, Consumption |The average number of default type queries processed per second in 5 minutes |
|Virtual Warehouse |Insert Query QPS |VirtualWarehouse_Query_Per_Second_Insert |VirtualWarehouse |ResourceID,VWID |Count/Second |Alarm, Consumption |Average number of insertion queries processed per second in 5 minutes |
|Virtual Warehouse |System Query QPS |VirtualWarehouse_Query_Per_Second_System |VirtualWarehouse |ResourceID,VWID |Count/Second |Alarm, Consumption |The average number of system queries processed per second in 5 minutes |
|Virtual Warehouse |Concurrent Queries |VirtualWarehouse_Concurrent_Queries |VirtualWarehouse |ResourceID,VWID |Count |Alarm, Consumption |Number of queries of all types currently executing concurrently |
|Virtual Warehouse |Concurrent Default Queries |VirtualWarehouse_Concurrent_Queries_Default |VirtualWarehouse |ResourceID,VWID |Count |Alarm, Consumption |The number of default class queries currently executing concurrently |
|Virtual Warehouse |Concurrent Insert Queries |VirtualWarehouse_Concurrent_Queries_Insert |VirtualWarehouse |ResourceID,VWID |Count |Alarm, Consumption |The number of insert\-class queries currently executing concurrently |
|Virtual Warehouse |Concurrent System Queries |VirtualWarehouse_Concurrent_Queries_System |VirtualWarehouse |ResourceID,VWID |Count |Alarm, Consumption |The number of system class queries currently executing concurrently |
|Virtual Warehouse |Insertion success rate |VirtualWarehouse_Insert_Success_Percentage |VirtualWarehouse |ResourceID,VWID |Percent |Alarm, Consumption |Percentage of successful inserts executed within 5 minutes |
|Virtual Warehouse |Number Of Background Tasks |VirtualWarehouse_Current_Manipulation |VirtualWarehouse |ResourceID,VWID,Pod(Optional) |Count |Alarm, Consumption |Number Of Background Tasks |
|Virtual Warehouse |Query P75 delay |VirtualWarehouse_Query_P75_Latency |VirtualWarehouse |ResourceID,VWID |Millisecond |Alarm, Consumption |The fastest 75% average latency among currently executing queries |
|Virtual Warehouse |Network Peak Input Rate |VirtualWarehouse_Network_Peak_Receive_Throughput |VirtualWarehouse |ResourceID,VWID,Pod(Optional) |Bytes/Second(SI) |Alarm, Consumption |Peak network traffic per second |
|Virtual Warehouse |Network Peak Output Rate |VirtualWarehouse_Network_Peak_Transmit_Throughput |VirtualWarehouse |ResourceID,VWID,Pod(Optional) |Bytes/Second(SI) |Alarm, Consumption |Peak network traffic per second |
|Virtual Warehouse |Memory occupancy (WSS) |VirtualWarehouse_Memory_WorkingSet_Usage_Percentage |VirtualWarehouse |ResourceID,VWID,Pod(Optional) |Percent |Alarm, Consumption |Current memory usage (WSS) as a percentage of requested resources |
|Keys and Licenses |API Key remaining valid period |KeyAndLicense_API_Key_Expires_In_Days |KeyAndLicense |ResourceID,APIKeyMask,SubAccountID |Day |Alarm, Consumption |API Key remaining valid period |
|Task Center |Hourly Task Completions |TaskCenter_Task_Completion_Rate |TaskCenter |ResourceID,TaskID |Count |Alarm, Consumption |Hourly Task Completions |
|Task Center |Task Successes |TaskCenter_TTask_Success_Rate |TaskCenter |ResourceID,TaskID |Count |Alarm, Consumption |Hourly Task Successes |
|Task Center |Task Failures |TaskCenter_Task_Failure_Rate |TaskCenter |ResourceID,TaskID |Count |Alarm, Consumption |Hourly Task Failures |
|Task Center |Task Success Ratio |TaskCenter_Task_Success_Ratio |TaskCenter |ResourceID,TaskID |Percent |Alarm, Consumption |Percentage of successful task execution within one hour |
|Storage |Total Volume |Storage_Total_Volume_Bytes |Storage |ResourceID |Bytes(IEC) |Alarm, Consumption |The size of the database storage space, accurate to bytes |
|Storage |Total Databases |Storage_Total_Databases |Storage |ResourceID |Count |Alarm, Consumption |Number of databases created |
|Storage |Total Tables |Storage_Total_Tables |Storage |ResourceID |Count |Alarm, Consumption |Total number of data tables created |
|Storage |Total Rows |Storage_Total_Rows |Storage |ResourceID |Count |Alarm, Consumption |Sum of rows of data inserted |
|Connect |Current number of gateway connections |Connection_Gateway_Connection_Count |Connection |ResourceID |Count |Alarm, Consumption |Current number of gateway connections |
|Private Server |CPU Utilization |PrivateServer_CPU_Usage_Percentage |PrivateServer |ResourceID,Pod(Optional) |Percent |Alarm, Consumption |CPU Utilization |
|Private Server |Memory occupancy (RSS) |PrivateServer_Memory_Usage_Percentage |PrivateServer |ResourceID,Pod(Optional) |Percent |Alarm, Consumption |Current memory usage (RSS) as a percentage of requested resources |
|Private Server |Total QPS |PrivateServer_Query_Per_Second |PrivateServer |ResourceID,Pod(Optional) |Count/Second |Alarm, Consumption |Average number of queries of all types processed per second in 5 minutes |
|Private Server |Default Query QPS |PrivateServer_Query_Per_Second_Default |PrivateServer |ResourceID,Pod(Optional) |Count/Second |Alarm, Consumption |The average number of default type queries processed per second in 5 minutes |
|Private Server |Insert Query QPS |PrivateServer_Query_Per_Second_Insert |PrivateServer |ResourceID,Pod(Optional) |Count/Second |Alarm, Consumption |Average number of insert\-type queries processed per second in 5 minutes |
|Private Server |Concurrent Queries |PrivateServer_Concurrent_Queries |PrivateServer |ResourceID,Pod(Optional) |Count |Alarm, Consumption |The number of queries of all types currently executing concurrently |
|Private Server |Concurrent Default Queries |PrivateServer_Concurrent_Queries_Default |PrivateServer |ResourceID,Pod(Optional) |Count |Alarm, consumption |The number of default class queries currently executing concurrently |
|Private Server |Query Success Ratio |PrivateServer_Query_Success_Percentage |PrivateServer |ResourceID,Pod(Optional) |Percent |Alarm, Consumption |Percentage of queries successfully executed within 5 minutes |
|Private Server |Slow Queries \> 10s |PrivateServer_Query_Slow_Queries |PrivateServer |ResourceID,Pod(Optional) |Count |Alarm, Consumption |The number of queries that have been executed for more than 10 seconds |
|Private Server |Query P95 Latency |PrivateServer_Query_P95_Latency |PrivateServer |ResourceID,Pod(Optional) |Millisecond |Alarm, Consumption |The fastest 95% average latency among currently executing queries |
|Private Server |Query P99 Latency |PrivateServer_Query_P99_Latency |PrivateServer |ResourceID,Pod(Optional) |Millisecond |Alarm, consumption |The fastest 99% average latency among currently executing queries |
|Private Server |Insert Success Ratio |PrivateServer_Insert_Success_Percentage |PrivateServer |ResourceID,Pod(Optional) |Percent |Alarm, Consumption |Percentage of successful inserts executed within 5 minutes |
|Private Server |Insert Query Concurrency |PrivateServer_Concurrent_Queries_Insert |PrivateServer |ResourceID,Pod(Optional) |Count |Alarm, Consumption |The number of insert\-class queries currently executing concurrently |
|Private Server |Query P75 delay |PrivateServer_Query_P75_Latency |PrivateServer |ResourceID,Pod(Optional) |Millisecond |Alarm, Consumption |The fastest 75% average latency among currently executing queries |
|Private Server |Network Peak Input Rate |PrivateServer_Network_Peak_Receive_Throughput |PrivateServer |ResourceID,Pod(Optional) |Bytes/Second(SI) |Alarm, Consumption |Peak network traffic per second |
|Private Server |Network Peak Output Rate |PrivateServer_Network_Peak_Transmit_Throughput |PrivateServer |ResourceID,Pod(Optional) |Bytes/Second(SI) |Alarm, Consumption |Peak network traffic outflow per second |
|Private Server |Memory occupancy (WSS) |PrivateServer_Memory_WorkingSet_Usage_Percentage |PrivateServer |ResourceID,Pod(Optional) |Percent |Alarm, Consumption |Current memory usage (WSS) as a percentage of requested resources |
|Virtual warehouse local disk |Disk Utilization |DiskCache_Spaced_Used_Percentage |DiskCache |ResourceID,VWID,Pod(Optional) |Percent |Alarm, Consumption |Disk Utilization Rate |
|Virtual warehouse local disk |Cache data read and write times |DiskCache_Rows_Read_From_DiskCache_Pre_Sec |DiskCache |ResourceID,VWID,Pod(Optional) |Count/Second |Alarms, Expenditure |Cache Data Read Write Count |
|Virtual warehouse local disk |Cache Hit Rate |DiskCache_Disk_Cache_Hit_Rate |DiskCache |ResourceID,VWID,Pod(Optional) |Percent |Alarms, Expenditure |Cache Hit Rate |
|Virtual warehouse local disk |Disk IOPS (Read) |DiskCache_Disk_Read_IOPS |DiskCache |ResourceID,VWID,Pod(Optional) |Count/Second |Alarm, Consumption |Disk IOPS (Read) |
|Virtual warehouse local disk |Disk IOPS (Write) |DiskCache_Disk_Write_IOPS |DiskCache |ResourceID,VWID,Pod(Optional) |Count/Second |Alarm, Consumption |Disk IOPS (Write) |
|Virtual warehouse local disk |Disk Bandwidth (Read) |DiskCache_Disk_Read_Byte |DiskCache |ResourceID,VWID,Pod(Optional) |Kibibytes/Second |Alarm, Consumption |Disk Bandwidth (Read) |
|Virtual warehouse local disk |Disk Bandwidth (Write) |DiskCache_Disk_Write_Byte |DiskCache |ResourceID,VWID,Pod(Optional) |Kibibytes/Second |Alarm, Consumption |Disk Bandwidth (Write) |
|Virtual warehouse local disk |iNodes Usage |DiskCache_Disk_Inode_Usage |DiskCache |ResourceID,VWID,Pod(Optional) |Percent |Alarm, Consumption |iNodes Usage Ratio |


<span id="ee340b94"></span>
# View monitoring

This section outlines the steps to view monitoring information.

<span id="e2c658ef"></span>
## Steps


1. Log in to [ByteHouse Cloud Data Warehouse Console](https://console.byteplus.com/auth/login?redirectURI=%2Fiam).

2. In the top left corner of the menu bar, select the region to which the instance belongs.

3. At the top of the page, click **Tenant management** \> \*\*\*\* **Cloud monitor** tab. You can click to view monitoring details for **Virtual Warehouses**, **API Key and License**, **Task center**, **Storage**, **Connections**, **Private server**, and **Local disk**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76bf2ed2874743b89bff1e0cddf092fa~tplv-goo7wpa0wc-image.image) </span>


<span id="0710b067"></span>
# Configure alarm

ByteHouse Cloud Data Warehouse has integrated with cloud monitoring services to manage alarm policies through these services. This section explains how to create alarm policies. For more detailed alarm processes and principles, refer to [Alarm mechanism--Cloud Monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Alarm-mechanism).

<span id="886d497e"></span>
## Steps


1. Log in to the [Cloud Monitoring Console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left sidebar, select **Alarm Center** \> **Alarm Strategy**.

3. On the **Alarm Strategy** page, click **Create Alarm Strategy** to enter the Cloud Monitoring service's Alarm Strategy creation page.

4. On the **Create Alarm Strategy** page, configure the parameters based on business needs. For specific parameter configuration instructions, please refer to [Create Alarm Strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the <strong>Create Alarm Strategy</strong> pages, when configuring the alarm object, you need to select the type of Resources as <strong>Data Middle Platform \> ByteHouse Cloud Data Warehouse Edition</strong>.   </div>
   

<span id="95b2d78b"></span>
## Recommended alarm strategy

<span id="d235b9a0"></span>
### Virtual Warehouse


* It is recommended to set an alarm for the Compute Group when CPU usage / memory usage exceeds 80%.


<span id="32b34896"></span>
### API Key


* To avoid service disruptions due to an expired API Key preventing connection to ByteHouse, it is advisable to monitor and alarm when the API Key's validity period is less than 7 days.


<span id="6a1b6618"></span>
### Task center


* Monitor and alarm for scheduled tasks in the Task Center, with monitoring and alarms based on task success rate. The threshold can be customized according to business needs.


<span id="08df7055"></span>
### Gateway connections


* The current threshold for ByteHouse gateway connections is 2000. Exceeding this will trigger a rate limiting operation. Configuring this monitoring alarm can help observe whether the gateway connections used by the business are within a safe range well in advance. It is recommended that the threshold be set at 1500.


<span id="cbd79a2f"></span>
## Relevant links


* [View an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-an-alarm-strategy)

* [Modify an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Modifying-an-alarm-strategy)

* [Enable an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Enabling-an-alarm-strategy)

* [Disable an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Disabling-an-alarm-strategy)

* [Delete an alarm policy](https://docs.byteplus.com/en/docs/cloudmonitor/Deleting-an-alarm-strategy)

* [View alarm history](https://docs.byteplus.com/en/docs/cloudmonitor/Viewing-alarm-history)

* [Instructions for using alarm callbacks](https://docs.byteplus.com/en/docs/cloudmonitor/Webhook-instructions)

* [Connect alarm callbacks with Lark groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-Feishu-groups)

* [Alarm callback linked to DingTalk groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-DingTalk-groups)

* [Alarm callback linked to WeCom groups](https://docs.byteplus.com/en/docs/cloudmonitor/Receiving-alarm-notifications-in-WeChat-groups)
