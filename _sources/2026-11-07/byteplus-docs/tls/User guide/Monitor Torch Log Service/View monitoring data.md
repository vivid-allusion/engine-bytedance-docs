---
title: "View monitoring data"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/view_monitore_data"
---

You can view billing\-related metrics and analyze the usage of TLS resources in the TLS console. This topic explains TLS metrics and describes how to view the metrics.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Units in the metric table are basic units. Metric units in the console prevail. Units displayed in the console are adjusted based on the value and conversion standard. For example, the basic log storage unit is byte. If the volume of stored logs reaches a KiB, GiB, or TiB level, the unit is converted to KiB, GiB, or TiB in the console, respectively.

<span id="5912da2b"></span>
## View monitoring data

<span id=".6YCa6L-H5pel5b-X5pyN5Yqh5o6n5Yi25Y-w5p-l55yL55uR5o6n5pWw5o2u"></span>
### View monitoring data in the TLS console

You can view monitoring data in the TLS console. For more information on metrics, refer to [Metrics](https://docs.byteplus.com/docs/tls/view_monitore_data#.55uR5o6n6aG56K-05piO).


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

3. Select the target project, then click the project name.

4. In the **Topic** pane, locate the target topic, and click the **Check the monitoring** in the **Action** column.

5. In the left\-side navigation pane, under the **Topic** tab, click the expand icon in front of the specified topic, and then click **Cloud monitoring**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b473813de9640fda31ce4f0aa4427d2~tplv-goo7wpa0wc-image.image) </span>

6. View cloud monitoring data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the page displays the monitoring data of the topic in the past day. Alternatively, select a time period to view the corresponding data. You can also check <strong>chart linkage</strong> to see the data values of all monitored items at a given moment.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bada431a178440bda4345af182f3f67c~tplv-goo7wpa0wc-image.image) </span>


<span id="4e338f45"></span>
### View monitoring data in the Cloud Monitor console


1. Log on to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor).

2. In the left\-side navigation pane, click **Cloud Service Monitor**, then click **TLS**.

3. In the top navigation bar, select the region.

   The page will display an overview of alerts and a list of projects for the specified region.

   * In the **Alarm overview** area, you can view the current total number of alarms, the number of alarms at each level, and the number of alarm policies.

   * The log projects list displays the project name, project ID, creation time, and number of log topics of the log project. You can quickly find target log projects by filtering by log project name or project ID.

4. Click the log project name to enter the monitoring data page for that log project.

5. Select the log topic name in the **tls_billing** tab and view the monitoring data.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the page displays the monitoring data of the topic in the past day. Alternatively, select a time period to view the corresponding data. You can also check <strong>chart linkage</strong> to see the data values of all monitored items at a given moment.   </div>
   

<span id="b61f2255"></span>
## Set cloud monitoring alarm policies

You can monitor the usage of TLS resources through the cloud monitoring alarm function to avoid abnormal resource usage causing the fee to skyrocket. After setting alarm policies in the Cloud Monitor console, when the specified resource usage meets the trigger condition, Cloud Monitor will send an alarm notification in time.


1. Log on to the [Cloud Monitor console ](https://console.byteplus.com/cloud-monitor).

2. In the left\-side navigation pane, click **Cloud Service Monitor**, then click **TLS**.

3. At the top right of the page, click **Create alarm strategy**.

4. On the **Create alarm strategy** page, set the parameters related to the alarm policy.

   For example, refer to the following configuration to monitor intranet write traffic, intranet read traffic, data shipping traffic and data processing traffic. An alarm will be triggered when their average value increases by 50% compared to the previous day. You can also check **Use preset trigger conditions** to use system\-predicted alarm conditions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2b1354a233cf414a9bd4f88a70a79497~tplv-goo7wpa0wc-image.image) </span>

5. Click **OK**.


<span id=".55uR5o6n6aG56K-05piO"></span>
## Metrics

TLS supports the following topic\-level monitoring data.


|Metric ID |Unit |Dimensions |Description |
|---|---|---|---|
|StandardLogStorage |Byte |Topic |The volume of stored logs. |
|ShardNum |Count |Topic |The number of shards. |
|StandardIndexStorage |Byte |Topic |The volume of stored index data. |
|ReadRequest |Count |Topic |The number of requests to call the TLS read API.<br><br>The number of TLS read and write API requests that you send using LogCollector, API actions, and SDKs, excluding the API calls triggered by operations in the console. |
|WriteRequest |Count |Topic |The number of requests to call the TLS write API.<br><br>The number of TLS write API requests that you send using LogCollector, API actions, and SDKs, excluding the API calls triggered by operations in the console. |
|InnerReadTraffic |Byte |Topic |The downstream traffic generated by accessing a TLS private endpoint. For example, read traffic over an internal network is generated when you download logs over a private network or consume logs using a private network application. Read traffic is not generated when you query and analyze logs using the console or APIs. |
|InnerWriteTraffic |Byte |Topic |The upstream traffic generated by accessing a TLS private endpoint. |
|PublicReadTraffic |Byte |Topic |The downstream traffic generated by accessing a TLS public endpoint. For example, read traffic over the internet is generated when you download logs over a public network or consume logs using a public network application. Read traffic is not generated when you query and analyze logs using the console or APIs. |
|PublicWriteTraffic |Byte |Topic |The upstream traffic generated by accessing a TLS public endpoint. |
|ShipperTraffic |Byte |Topic |You are charged based on the amount of data shipped to Torch Object Storage (TOS). |
|ETLProcessedTraffic |Byte |Topic |You are charged based on the amount of log data for data transformation. The amount of log data refers to the amount of uncompressed raw log data. |
|IndexTraffic |Byte |Topic |You are charged based on the amount of data generated by the indexes that are built or rebuilt in raw logs. |
|InfrequentStorage |Byte |Topic |After enabling the low\-frequency storage feature, the storage volume of low\-frequency storage of logs. Among them, the storage volume refers to the uncompressed raw data volume. |
|InfrequentIndexStorage |Byte |Topic |The amount of indexed data stored after enabling the low\-frequency storage function and when the data is indexed. Among them, the data amount refers to the uncompressed raw data amount. |
