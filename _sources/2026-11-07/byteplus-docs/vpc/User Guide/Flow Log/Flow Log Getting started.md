---
title: "Flow Log Getting started"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Flow-Log-Getting-Started"
---

This topic introduces how to view traffic between Elastic Compute Service (ECS) instances within a VPC using flow logs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5394576320c4f62c9c39d8d2ab768049.png) </span>

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations


* See the diagram above to create a VPC and two ECSs. For actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) and [Creating an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* When using the Flow Log service for the first time: Navigate to the [Flow Log console](https://console.byteplus.com/vpc/region:vpc+cn-beijing/vpc?projectName=default), click **Create Flow Log**. In the pop\-up window, click **Authorize**. On the cross\-service access request page that appears, click **Authorize Now** to complete the authorization.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following section only covers essential parameters and their recommended values. For all parameters not explicitly discussed, retain the default settings unless otherwise required by your specific use case.</div>


<span id=".5q2l6aqk5LiA77ya5Yib5bu65rWB5pel5b-X"></span>
### Step 1: Create Flow Log


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Flow Log**.

3. In the top menu bar, select the target project and region.

4. Click **Create Flow Log**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Billing method |Currently only supports Pay\-as\-you\-go. |Pay\-as\-you\-go |
   |Name |Enter the name of flow log. |flowlog\-1 |
   |Resource Type |Select the resource type for flow log recording, which defines the scope of flow log collection.<br><br><br>* Virtual Private Cloud (VPC): Collects the traffic of all network interfaces within the VPC.<br><br>* Subnet: Collects the traffic of all network interfaces within the subnet.<br><br>* Network interface: Collects the traffic of a specified network interface. |VPC |
   |Resource |Based on the selected resource type, select the target resource to collect from the dropdown list. |vpc01 |
   |Traffic type |Select the traffic type, i.e., the traffic to be recorded in the flow logs.<br><br><br>* All Traffic: Collects all inbound and outbound traffic of the Network Interface.<br><br>* Permitted Traffic: Collects traffic allowed by security groups and network ACLs.<br><br>* Rejected Traffic: Collects traffic rejected by security groups and network ACLs. |Total traffic |
   |Sampling interval |Select the sampling interval for the flow log. The sampling interval is the interval at which the VPC delivers flow log data to the Torch Log Service (TLS). For connections with continuous data packets, the sampling interval also represents the maximum aggregation time for traffic data aggregated into a single log entry.<br><br><br>* 10 minutes: The flow log samples every 10 minutes, storing the traffic data within these 10 minutes to the Torch Log Service.<br><br>* 5 minutes: The flow log samples every 5 minutes, storing the traffic data within these 5 minutes to the Torch Log Service.<br><br>* 1 minute: The flow log samples every 1 minute, storing the traffic data within this 1 minute to the Torch Log Service. |10 minutes |
   |Log project |Select a Log Project. A Log Project is the fundamental resource management unit in the TLS, used for tenant resource isolation and access control.<br><br><br>* Create a Log Project: Create a new log project by entering a name for it.<br><br>* Select Existing: Select an existing log project.  |New log project<br><br>vpc\-flowlog\-project—1 |
   |Log topic |Select a Log Topic for the logs. A Log Topic is the fundamental unit in Log Service for log management (e.g., collection, storage, query, and analysis).<br><br><br>* Create New Log Topic: Create a new log topic. And automatically Enable automatic sharding. This Log Topic is managed by VPC Flow Logs. It can only be modified or deleted after the associated VPC Flow Logs are deleted.<br><br>* Use Existing: Select an existing log topic. If the existing log topic does not have automatically split log partitions enabled, exceeding the capacity of existing partitions may lead to data loss. Therefore, it is recommended to enable Automatic sharding.  |New log topic<br><br>vpc\-flowlog\-topic—1 |
   |Enable index |Select Enable Indexing Indexes are used for searching and analyzing data. Flow Logs must be configured with indexes before you can perform search and analysis.<br><br><br>* After selection, the system automatically configures key\-value indexing based on[flow log fields](https://docs.byteplus.com/en/docs/vpc/Flow-log-overview#.5rWB5pel5b-X5a2X5q61)within the log topic.<br><br>* If not selected, you must configure indexes for the flow logs in the log topic and enable field analytics before analyzing the flow logs. See [Configure Index](https://docs.byteplus.com/en/docs/vpc/Configuring-an-index) for instructions. |**Check** |
   

6. Follow the console guidance to review and accept Legal.

7. Click **Buy now** to complete creation.


<span id="TrjyCY6Q"></span>
### Step 2: Analyze flow log

Flow logs require actual data transmission between ECS\-A and ECS\-B to analyze the traffic between them. For example, you can use a local computer browser to remotely log in to ECS\-A and execute the `ping <ECS-B's IP address>` command. After waiting for 5 minutes, open a new tab in the local browser, remotely log in to ECS\-A again, and execute the `ping <ECS-B's IP address>` command once more.


1. Click the Topic Name under the **Log topic** column for the target flow log (e.g., flowlog\-1).

2. Click the Search & Analyze icon on the right side of the target Log Topic.

3. Type the search and analysis statement, then click **Search**. Taking the example of viewing traffic from ECS\-A accessing ECS\-B, the analysis query is as follows:

   ```Plain Text
   srcaddr:"192.168.1.11" and dstaddr: "192.168.1.22" | SELECT DATE_FORMAT(t, '%H:%i:%S') AS time, dstaddr, SUM((bytes * 8) / (`end` - start)) AS bandwidth FROM (SELECT `end`, start, dstaddr, bytes, (__time__ - (__time__ % 36000)) AS t limit 1000) GROUP BY time, dstaddr ORDER BY time ASC limit 1000
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When inputting the analysis statement, please replace the source IP address (ECS\-A's address) 192.168.1.11 and the destination IP address (ECS\-B's address) 192.168.1.22 with the actual IP address.   </div>
   

4. View the analysis results.

   As shown in the figure above, over the past 10 minutes, the traffic from ECS\-A (192.168.1.11) to ECS\-B (192.168.1.22) has shown a step\-like increase.

   Chart analysis settings are configured as follows:

   
   |Parameter |Description |Example |
   |---|---|---|
   |Chart type |Select the chart type as needed. |Traffic Volume Dashboard |
   |X\-axis field |Select the X\-axis field. |time |
   |Y\-axis field |Select the Y\-axis field. |bandwidth |
   |Aggregation field |Select the aggregation field. |dstaddr |
   |Formatting |Select Formatting. |bps, kbps, Mbps(SI) |
   

   Keep the remaining settings at their default values. 


&nbsp;

&nbsp;
