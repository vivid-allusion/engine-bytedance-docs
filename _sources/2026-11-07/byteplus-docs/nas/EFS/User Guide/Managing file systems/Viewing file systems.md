---
title: "Viewing file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Viewing_file_systems"
---

This topic explains how to view details about your file systems, such as an overview and capacity information.

<span id="C2j9a7u8"></span>
## Prerequisites

You have created a file system. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

<span id="rS28MWdq"></span>
## Viewing file system overview


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. On the **Overview** page, view the details about the file system. The parameter descriptions are as follows.

   * **Basic information**

      
      |Parameter |Description |
      |---|---|
      |File System name |The name of the file system.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To change the name of the file system, click the edit icon next to it.</div><br> |
      |File System ID |The unique identifier of the file system. This cannot be changed after creation.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To copy the file system ID, click the copy icon next to it.</div><br> |
      |State |The operational status of the file system, including:<br><br><br>* Creating<br><br>* Creation failed<br><br>* Running<br><br>* Updating<br><br>* Deleting<br><br>* Deletion failed<br><br>* Deleted<br><br>* Closed |
      |Availability Zone |The zone where the file system is deployed. |
      |Creation time |The time when the file system is created. |
      |Description |The description of the file system.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To update the description of the file system, click the edit icon next to it.</div><br> |
      

   * **Billing information**

      
      |Parameter |Description |
      |---|---|
      |Billing method |The payment model for the file system. |
      

   * **Instance information**

      
      |Parameter |Description |
      |---|---|
      |Instance type |The product specification of the file system. |
      |Performance density |The performance density of the file system. |
      

   * **Capacity**

      
      |Parameter |Description |
      |---|---|
      |Capacity ceiling |The maximum capacity that the file system can provide. |
      |Maximum file count |The maximum number of files that the file system can hold. |
      |Used capacity |The size of the data currently stored in the file system. |
      

   * **Bandwidth**

      
      |Parameter |Description |
      |---|---|
      |Bandwidth mode |The bandwidth mode selected for the file system, either **Provisioned Bandwidth** or **Baseline Bandwidth**.<br><br>To change the mode, click the edit icon next to it.<br><br><br>* When the bandwidth mode is **Baseline Bandwidth**, you can click the edit icon next to it to switch to **Provisioned Bandwidth**, and configure it based on your needs.<br><br>* When the bandwidth mode is **Provisioned Bandwidth**, you can click the edit icon next to it to switch to **Baseline Bandwidth**. |
      |Baseline Bandwidth |The baseline bandwidth for the file system. |
      |Provisioned Bandwidth |This area displays the provisioned bandwidth value when the bandwidth mode is **Provisioned Bandwidth**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To adjust <strong>Provisioned Bandwidth</strong>, click the edit icon next to it.</div><br> |
      |Instance bandwidth cap |This area displays the current bandwidth limit when the bandwidth mode is **Provisioned bandwidth**. |
      |Burst Bandwidth limit |The burst bandwidth limit configured for the file system.<br><br><br>* If **Burst** **Bandwidth** is not enabled, click the edit icon to enable it and set the **Burst** **Bandwidth** **limit**.<br><br>* If **Burst** **Bandwidth** is enabled, click the edit icon to disable it or adjust the **Burst** **Bandwidth** **limit**. |
      

   * **Advanced information**

      
      |Parameter |Description |
      |---|---|
      |Affiliated project |The project to which the file system belongs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To access the <strong>Project details</strong> page, click the project name.</div><br> |
      |Tag |The number of tags in the file system.<br><br><br>* To view tag details, hover over the tag count.<br><br>* To make changes to the tag information, click the edit icon next to it. |
      


<span id="fOutOEs5"></span>
## Viewing storage details


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **Monitoring** **alarm**.

6. On the **Monitoring** **alarm** page, click the **capacity** tab to view the total capacity, used capacity, and other details for the file system.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can specify a time range or a date for querying at the top of the tab.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Expand the statistics chart by clicking the expand icon in the top right corner.   </div>
