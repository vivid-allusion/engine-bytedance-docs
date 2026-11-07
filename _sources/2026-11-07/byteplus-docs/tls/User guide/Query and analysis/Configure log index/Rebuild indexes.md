---
title: "Rebuild indexes"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Rebuild-indexes-2"
---

After you modify indexes, the new indexes only take effect for data written after the modification. To rebuild index rules for historical data within a specific time period, refer to this topic.

<span id="d0ee5e95"></span>
## Background

After you modify indexes, historical data still follows the old index rules in log query and analysis. The new indexes only take effect for data written after the modification. Torch Log Service (TLS) allows you to use the latest index configurations to rebuild index rules for historical data within a specific time range. For example, configure indexes for historical data for which indexing is not enabled to expand the scope for data query and analysis; add a specific field to key\-value indexing to find this field from both historical data and new data.

When you rebuild indexes, TLS creates a reindexing task to record the configuration and progress of rebuilding indexes. If you delete the task, the new index data in the corresponding time range is also deleted. The historical data in that time range follows the old index rules before the indexes are rebuilt.

<span id="751c9857"></span>
## Fees

The feature of rebuilding indexes itself does not incur fees. However, the relevant resources may incur fees. For example:


* Index traffic fees: Rebuilding indexes for raw logs in a specific time range incurs one\-time index traffic fees.

* Index storage fees:

   * After you rebuild indexes, the new index data incurs storage fees.

   * If indexing is already enabled for historical data, the index data still exists after you rebuild indexes and incurs fees based on the storage volume.

   * After you delete the reindexing task, TLS deletes the corresponding reindexing data, which no longer incurs storage fees.


<span id="40bcf6e0"></span>
## Before you begin


* Enable indexing for a specific topic. For more information, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).

* Properly assess the time range of logs for which you want to rebuild indexes. The time taken by a reindexing task is related to the volume of log data. The larger the volume, the longer the task takes. Meanwhile, log data in the rebuild process cannot be queried or analyzed. We recommend that you properly assess the time range of logs for which you want to rebuild indexes to shorten the build time, reduce the build costs, and minimize the impact on query and analysis.


<span id="4696d6ae"></span>
## Precautions


|Item |Limits |
|---|---|
|Data range limits |You can only rebuild indexes for historical data within 15 minutes to 30 days earlier than the current time. |
|Operation limits |* When a reindexing task is running, you cannot rebuild indexes again.<br><br>* Each topic supports up to 10 reindexing task records at the same time. To create more tasks, delete historical task records first. |
|Query and analysis limits |* In the process of rebuilding indexes, the rebuilt indexes take effect immediately, while the data being indexed cannot be queried. We recommend that you query and analyze log data in the corresponding time period after the indexes are rebuilt.<br><br>* The indexes for a log cannot be rebuilt and the log data cannot be queried in one of the following situations: (1) The interval between the log time and the time when the log is reported to the server is greater than one hour. (2) The uploaded log time falls within the rebuild time range. |


<span id="ec88593a"></span>
## Procedure


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Common functions** \> **Query and analysis**.

3. Find the topic for which you want to rebuild indexes, expand the index configuration button on the upper\-right corner, then click **Rebuild index**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a73330a9956349e9a6171045c18cf783~tplv-goo7wpa0wc-image.image) </span>

4. Click **Add rebuild index task**.

5. Set the task information.

   
   |Parameter |Description |
   |---|---|
   |Task name |The name of the reindexing task. |
   |Time range |The time range of logs for which you want to rebuild indexes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only rebuild indexes for historical data within 15 minutes to 30 days earlier than the current time.</div><br> |
   

6. Click **OK**.


<span id="116447ee"></span>
## Related operations


* Viewing the task status: On the query and analysis page, click **Rebuild index** to view the status of all reindexing tasks. For tasks in **Reconstruction in progress** or **Cancelled** state, the rebuilding progress is displayed.

* Canceling a reindexing task in progress: In the reindexing task list, find the target task and click **Cancel**. The indexes rebuilt before you cancel the task are retained. The indexing for data to be indexed stops. A canceled task cannot be resumed. To facilitate subsequent query and analysis, we recommend that you delete the canceled task and create a new one.

* Deleting a reindexing task: After you delete a task, the rebuilt indexes are deleted as well and cannot be recovered.
