---
title: "Data balancing"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Data-balancing"
---

When the file system capacity utilization exceeds 90%, it is recommended to enable the data balancing feature. This topic provides an introduction to data balancing and the corresponding operational steps.

<span id="766fef55"></span>
## Constraints and limitations

Only the 100MB/s/TiB specification supports data balancing function.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

There are the following problems with data balancing:


* The data balancing process consumes the network and disk bandwidth of storage nodes, leading to a decrease in the front\-end IO performance of the file system.

* The more stock data there is in the file system, the longer it takes to balance the data. Taking into account that most businesses do not require automatic data balancing after capacity expansion, the existing data will still be stored on the original storage nodes and will not be automatically migrated to the newly expanded storage nodes.


If you have a need for data balancing, PFS supports automatic configuration of data balancing function. Data balancing is expected to have a certain impact on performance, so it is recommended that you choose to operate during off\-peak hours.

<span id=".5byA5ZCv5pWw5o2u5Z2H6KGh5Yqf6IO9"></span>
## Enable data balancing function.

You can enable data balancing when expanding the file system. For detailed steps, please refer to [Expanding a file system](https://docs.byteplus.com/docs/pfs/Expanding-a-file-system).

<span id=".5p-l55yL5pWw5o2u5Z2H6KGh54q25oCB"></span>
## View data balance status

After enabling data balancing, you can refer to the following steps to check the corresponding status.


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Instances** in the left navigation bar. On the Instance List page, click the name of the target file system.

4. On the instance overview page, you can view data balancing information, including **Equilibrium start time**,**Equilibrium end time**, **state**, **Progress**, and **Actions**. The explanation of data balancing task statuses is as follows.

   
   |Status |Description |
   |---|---|
   |In progress |The data balancing task is currently in progress.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can click <strong>Cancel</strong> button in the <strong>Actions</strong> column of the data balancing task to cancel or pause the data balancing task.</div><br> |
   |Task interrupt |The data balancing task execution interrupted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can click <strong>Enable</strong> button in the <strong>Actions</strong> column of the data balancing task to re\-enable the data balancing task.</div><br> |
   |Completed |The data balancing task has been completed. |
   |Cancelling |The data balancing tasks that are in the process of being cancelled or have failed to be cancelled. |
   |Cancelled |The data balancing task has been manually cancelled.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can click <strong>Enable</strong> button in the <strong>Actions</strong> column of the data balancing task to restart the data balancing task.</div><br> |
