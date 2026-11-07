---
title: "Configuring alarm rules"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Configuring-alarm-rules"
---

You can set corresponding alarm strategies for the PFS file system according to your business needs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">This topic only introduces the operation steps of configuring alarm strategies in the PFS console. You can log in to the <a href="https://console.byteplus.com/auth/login?redirectURI=%2Fcloud-monitor%2Foverview">CloudMonitor</a> console to directly configure alarm strategies. For specific steps, please refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Instances** in the left navigation bar. On the Instance List page, click on the target file system name.

4. On the instance details page, click **Monitoring alarm** tab, and then click on **Create an alert policy** at the top right corner of the page.

5. On the **Create alarm strategy** page, select the **Resource type** as PFS, configure the alarm parameters, and click OK.

   The description of the subnamespace supported by vePFS is as follows.

   
   |Parameter |Explanation |
   |---|---|
   |Basic information |Basic identification information for setting alarm strategies.<br><br><br>* **Name:**  Custom alarm strategy name, used to identify the alarm strategy.<br><br>* **Description**: Explanatory information for the custom alarm strategy. |
   |**Alarm object** ||
   |Resource type |Choose **vepfs**. |
   |selection method |Ways to select resources, optional:<br><br><br>* **Manual selection**: Manually select resources.<br><br>* **Resource Group**: Lock resources based on object grouping, you need to first create object groups on the Cloud Monitor, for specific operation instructions, please refer to [Creating a resource group](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-a-resource-group).<br><br>* **Resource Name**:Lock resources based on resource name. Set the matching rules for resource names, and lock resources based on the matching rules.<br><br><br>For detailed explanation of the selection methods, please refer to [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy). |
   |Region |Select the Region of the file system. |
   |Subnamespace |Subnamespace description is as follows:<br><br><br>* **capacity**<br><br>   Trigger conditions are as follows:<br><br>   * **Storage utilization**<br><br>   * **Inode utilization**<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">We recommend setting up an alarm strategy when the file system capacity reaches 90% to avoid issues such as data being unable to be written due to insufficient capacity.   </div><br>   <br><br>* **Fileset**<br><br>   Trigger conditions are as follows:<br><br>   * **Fileset Capacity Usage**<br><br>   * **Fileset inode used ratio**<br><br>   * **Fileset Block Used**<br><br>   * **Fileset pre\-allocation inode**<br><br>   * **Fileset Alloc Inode**<br><br>* **latency**<br><br>   Trigger conditions are as follows:<br><br>   * **Read latency**<br><br>   * **Write latency**<br><br>* **protocol_service**[Need to apply for a medical certificate]<br><br>   Trigger conditions are as follows:<br><br>   * **ProtocolServiceReadBandwidth**<br><br>   * **ProtocolServiceWriteBandwidth**<br><br>   * **ProtocolServiceReadlops**<br><br>   * **ProtocolServiceWritelops**<br><br>   * **ProtocolServiceReadLatency**<br><br>   * **ProtocolServiceWriteLatency**<br><br>   * **ProtocolServiceSmbReadBandwidth**<br><br>   * **ProtocolServiceSmbWriteBandwidth**<br><br>   * **ProtocolServiceSmbReadlops**<br><br>   * **ProtocolServiceSmbWritelops**<br><br>   * **ProtocolServiceSmbReadLatency**<br><br>   * **ProtocolServiceSmbWriteLatency**<br><br>   * **Fsproxy Read Bandwidth**<br><br>   * **Fsproxy Write Bandwidth**<br><br>   * **Fsproxy Read IOPS**<br><br>   * **Fsproxy Write IOPS**<br><br>   * **Fsproxy Read Latency**<br><br>   * **Fsproxy Write Latency**<br><br>* **bandwidth**<br><br>   Trigger conditions are as follows:<br><br>   * **read bandwidth**<br><br>   * **write bandwidth**<br><br>* **IOPS**<br><br>   Trigger conditions are as follows:<br><br>   * **Read IOPS**<br><br>   * **Write IOS** |
   |Resources |Set the scope of the alarm strategy to only monitor within the specified resource range.Support any of the following settings:<br><br><br>* **All**:Set alarm strategy for all resources under the current account that meet the specified resource type, region, and dimension. At the same time, newly created resources that meet the criteria will also automatically be matched with this alarm strategy.<br><br>* **Part**:You need to manually select one or more resources. After selection, it indicates that the alarm strategy is only set for that specific resource.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The range of resources available for different subnamespaces may vary. Please refer to the actual information in the console.</div><br> |
   |Alarm rules |Set **Metric type**,**Trigger condition**,**Alarm level**,**Effective time**,etc. For detailed instructions, please refer to the [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy). |
   |Alarm way |Set **Alarm** **channel**,including **Email**,**Webhook**.For detailed information about alarm channels, please refer to the [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy). |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed explanation of alarm parameters, please refer to <a href="https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy">Creating an alarm strategy</a>.   </div>
