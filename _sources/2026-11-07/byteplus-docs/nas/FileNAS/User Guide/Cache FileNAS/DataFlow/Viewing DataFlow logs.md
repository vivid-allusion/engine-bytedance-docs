---
title: "Viewing DataFlow logs"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Viewing_DataFlow_logs"
---

FileNAS provides log analysis capabilities through Torch Log Service (TLS), which tracks real\-time data flow of import, export, and eviction tasks. This topic explains how to view DataFlow logs.

<span id="ac2c985b"></span>
## Billing notes

Enabling FileNAS log analysis incurs charges for log storage, index storage, write traffic, index traffic, etc. TLS will bill these charges separately. For billing details, see [TLS Billing overview](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode).

<span id="758e3979"></span>
## Index fields


|**Field** |**Indexing** |**Description** |
|---|---|---|
|cache_strategy_id |Supported |DataFlow policy ID. |
|file_name |Supported |Relative file path. For example, if the file system path in the DataFlow policy is `/dir1/` and the absolute file path is `/dir1/subdir1/file1`, then the value here is `subdir1/file1`. |
|file_system_id |Supported |File system ID. |
|job_id |Supported |Task ID. |
|size_bytes |Supported |File size in bytes. |
|success |Supported |The value indicates file synchronization result:<br><br><br>* `1`: Success.<br><br>* `0`: Failure. |
|type |Supported |The value indicates the DataFlow task type:<br><br><br>* `LoadMeta Event`: Imports metadata immediately after the DataFlow policy is created.<br><br>* `LoadData Event`: Imports data immediately after the DataFlow policy is created.<br><br>* `TosToNas Event`: Imports incremental metadata and data.<br><br>* `NasToToS Event`: Exports data.<br><br>* `AutoFileEvict Event`: Automatically removes data.<br><br>* `ManualFileEvict Event`: Manually removes data. |
|skipped |Not supported |Policy for handling files with the same name during import or export tasks:<br><br><br>* `true`: Skip.<br><br>* `false`: Do not skip. |


<span id="8fc6f4c8"></span>
## Enabling log analysis

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Once log analysis is enabled, TLS automatically creates a project and topic to store related TOS logs. The log topic is named by default using the DataFlow policy ID.</div>


<span id="7491398a"></span>
### **Enabling log analysis when creating a DataFlow policy**

See [Creating DataFlow policies](https://docs.byteplus.com/en/docs/nas/Managing_DataFlow_policies#899321e9) for steps to enable the **Log analysis** feature when creating a DataFlow policy.

<span id="1e787bcd"></span>
### **Enabling log analysis for an existing DataFlow policy**


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region of the DataFlow policy you want to manage.

3. In the left navigation pane, select **File System** \> **DataFlow**.

4. On the **Policy** tab of the **DataFlow** page, click the DataFlow policy.

5. On the **Policy details** page, go to the **Log analysis** tab and click **Click to authorize** to allow your FileNAS to access BytePlus TLS.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the <strong>Log analysis</strong> tab on the policy details page shows <strong>You have authorized your NAS to access BytePlus TLS Log Service</strong>, you don't need to reauthorize.   </div>
   

6. Click **Edit** on the **Log analysis** tab. Toggle on the log analysis switch and click **Create**.


<span id="64c53cf6"></span>
## Viewing DataFlow logs


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region of the DataFlow policy you want to manage.

3. In the left navigation pane, select **File System** \> **DataFlow**.

4. On the **Policy** tab of the **DataFlow** page, click the DataFlow policy.

5. On the policy details page, click the **Log analysis** tab. Set the time range for the search, enter the query statement, and click **Search** to view the logs of the specified fields.

   Example queries are as follows:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For an introduction to log analysis query syntax, see <a href="https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2">Query syntax</a>.   </div>
   

   
   |**Query content** |**Example queries** |
   |---|---|
   |All logs within the specified time range |Set the time range, leave the query statement blank, and click **Search**. |
   |DataFlow synchronization failures |Set the time range with the query statement `NOT success:1`, and click **Search**. |
   |Logs for a specific file |Set the time range with the query statement `file_name:"file name"`, like `file_name:"czy0426/0619/empty"`, and click **Search**. |
   |All incremental import events |Set the time range with the query statement `type:"TosToNas Event"`, and click **Search**. |
   

&nbsp;


<span id="faf658e0"></span>
## Other operations


* **Disable log analysis**

   1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

   2. In the top menu bar, select the region of the DataFlow policy you want to manage.

   3. In the left navigation pane, select **File System \> DataFlow**.

   4. On the **Policy** tab of the **DataFlow** page, click the DataFlow policy.

   5. On the **Policy details** page, click the **Log analysis** tab.

   6. Click **Disable Log Analysis**, and then click **OK** in the box that appears.

* **View existing logs after disabling log analysis**

   Disabling log analysis will prevent the generation of new logs, but existing logs and TLS topics will not be deleted automatically. You can still view existing logs.

   1. Log in to the [TLS console](https://console.byteplus.com/tls).

   2. In the left navigation pane, select **Resource management** \> **Project**.

   3. On the **Project** page, click `filenas-service-project-` (marked with the `FileNAS` flag).

   4. On the project details page, navigate to the **Topic** tab. Click the topic name that matches the ID of the DataFlow policy for which you disabled the log analysis feature.

   5. On the query page, specify a time range to view the logs.

* **Delete DataFlow logs**

   When deleting a DataFlow policy, you can select the option to **Synchronize delete the policy for Torch Log Service TLS Projects and Topics**. The system will then automatically delete the TLS topic that was generated by that policy. For more information, see [Deleting DataFlow policies](https://docs.byteplus.com/en/docs/nas/Managing_DataFlow_policies#e6fb08be).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When deleting a DataFlow policy, if you do not select the option to <strong>Synchronize delete the policy for Torch Log Service TLS Projects and Topics</strong>, you can also delete the associated topic in the TLS console. For instructions, see <a href="https://docs.byteplus.com/en/docs/tls/Managing_topics#.5Yig6Zmk5pel5b-X5Li76aKY">Delete topic</a>.   </div>
