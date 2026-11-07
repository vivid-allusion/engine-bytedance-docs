---
title: "Viewing file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Viewing_file_systems"
---

In the FileNAS console, you can view file system details, including basic information and storage details.

<span id="c76fa848"></span>
## Viewing basic information


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the file system.

5. On the **Overview** tab, view the basic information of the file system. The parameter descriptions are as follows.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Basic information** ||
   |Name |The name of the file system.<br><br>Click the edit icon next to the file system name to modify it. |
   |Availability Zone |The zone where the file system is deployed. This cannot be changed after creation. |
   |ID |The unique identifier of the file system. This cannot be changed after creation.<br><br>Click the copy icon next to the ID to copy it. |
   |Used/Total capacity |* Used capacity: The size of the data currently stored in the file system.<br><br>* Total capacity: The storage capacity of the file system. |
   |File System type |**Cache FileNAS**, which indicates the file system edition. This cannot be changed after creation. |
   |Storage type |The storage type of the file system. Currently, only the **Standard type** is supported. |
   |File protocol |The access protocol of the file system. Currently, only **NFS** is supported. |
   |Creation time |The time when the file system is created. |
   |Description |The description of the file system.<br><br>Click the edit icon next to the description to modify it. |
   |**Platform information** ||
   |Billing method |The payment model for the file system. Currently, only **pay\-as\-you\-go** is supported. |
   |Affiliated project |The project to which the file system belongs. This cannot be changed after creation. |
   |Tag |The number of tags in the file system.<br><br>Click the edit icon in this section to modify the tags. |
   |**Performance information** ||
   |Baseline Bandwidth |The baseline performance of the file system.<br><br>For Cache FileNAS file systems, performance scales linearly with capacity. Baseline performance consists of two components: provisioned baseline and capacity\-based scaling. The initial guaranteed bandwidth is 600 MB/s, with a scaling rate of 0.1 MB/s per GiB. |
   |DataFlow Bandwidth |The maximum amount of bandwidth available between FileNAS and TOS. The DataFlow bandwidth uses 30% of the read and write bandwidth of the file system. |
   |Provisioned Bandwidth |The amount of bandwidth allocated based on business needs, regardless of storage capacity. Higher bandwidth enables faster reading, writing, and access speeds.<br><br>You can modify the provisioned bandwidth. For more information, see [Changing provisioned bandwidth](https://docs.byteplus.com/en/docs/nas/Managing_provisioned_bandwidth#279d31ad). |
   |Burst Bandwidth |Temporary bandwidth boost. After enabling burst bandwidth, you can set an upper limit for how much extra bandwidth the system can use during performance spikes.<br><br>You can modify the burst bandwidth. For more information, see [Modifying burst bandwidth](https://docs.byteplus.com/en/docs/nas/Managing_burst_bandwidth#PZhyVaMK). |
   


<span id="bee4ec6f"></span>
## Viewing storage details

Follow the steps below to view storage details, including total storage, used storage, total inode, used inode, storage utilization, and inode utilization.


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System** \> **File System list**.

4. On the **File System list** page, click the file system.

5. On the file system details page, click the **Monitoring alarm** tab.

6. Click the **Capacity** tab, review details about your file system, including total and used capacity.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can specify a time range or a date for querying at the top of the tab.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Expand the statistics chart by clicking the expand icon in the top right corner.   </div>
