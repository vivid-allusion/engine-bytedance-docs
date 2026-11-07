---
title: "Viewing DataFlow logs"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Viewing_DataFlow_logs"
---

EFS provides log analysis using Torch Log Service (TLS), which records DataFlow activity in real time. This topic explains how to view DataFlow logs.

<span id="wJVWR016"></span>
## Background information


* You can view relevant logs in either the EFS or TLS console. This topic only describes how to view logs in the EFS console. For information on viewing logs in the TLS console, see [Query and analysis workflow](https://docs.byteplus.com/en/docs/tls/Query-and-analysis-process?lang=zh).

* Once log analysis is enabled, TLS automatically creates a project (**auditlog_efs_default**) and topic (**auditlog_efs_dataflow**) to store DataFlow\-related logs.


<span id="JrmwkvKO"></span>
## Prerequisites


* To view DataFlow policy logs, you must first create a DataFlow policy. For instructions, see [Creating DataFlow policies](https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_policies#hgQLhtsU).

* To view DataFlow task logs, you must enable log analysis when creating a DataFlow task. For instructions, see [Creating DataFlow tasks](https://docs.byteplus.com/en/docs/nas/efs_Managing_DataFlow_tasks).


<span id="5nLJHj9S"></span>
## Enable log analysis (Optional)

If you have not enabled the log analysis feature when creating a DataFlow policy, you can enable it by following these steps:


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. On the **Policy** tab, click the name of the policy you want to manage.

8. On the policy details page, click the **Log analysis** tab.

9. Click **Click Authorize** to grant EFS permission to access TLS.

10. Enable log analysis by toggling the switch next to **Log analysis status**.

11. In the box that appears, click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The log analysis feature has been successfully enabled when <strong>Log analysis status</strong> displays as <strong>Enable</strong>.   </div>
   

<span id="g4Smxy16"></span>
## Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, click **DataFlow**.

6. On the **DataFlow** page, select the **Policy** tab.

7. On the **Policy** tab, click the name of the policy you want to manage.

8. On the policy details page, click the **Log analysis** tab.

9. Type a search query into the search box, select a time range for the log data, and click **Search**.


<span id="mcuEk34C"></span>
## Indexed Fields


|**Field** |**Indexing** |**Description** |
|---|---|---|
|cache_strategy_id |Supported |DataFlow policy ID. |
|file_name |Supported |Relative file path. For example, if the file system path in the DataFlow policy is `/dir1/` and the absolute file path is `/dir1/subdir1/file1`, then the value here is `subdir1/file1`. |
|file_system_id |Supported |File system ID. |
|job_id |Supported |Task ID. |
|object_name |Supported |Object name. |
|size_bytes |Supported |File size in bytes. |
|success |Supported |The value indicates file synchronization result:<br><br><br>* `1`: Success.<br><br>* `0`: Failure. |
|type |Supported |The value indicates the DataFlow task type:<br><br><br>* `LoadMeta Event`: Imports metadata immediately after the DataFlow policy is created.<br><br>* `LoadData Event`: Imports data immediately after the DataFlow policy is created.<br><br>* `TosToNas Event`: Imports incremental metadata and data.<br><br>* `NasToToS Event`: Exports data.<br><br>* `AutoFileEvict Event`: Automatically evicts data.<br><br>* `ManualFileEvict Event`: Manually evicts data. |
|skipped |Not supported |Indicates the conflict handling result for files with the same name during import or export tasks:<br><br><br>* `true`: Skip.<br><br>* `false`: Do not skip. |


<span id="fDRvNgNx"></span>
## Example queries

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">For an introduction to log analysis query syntax, see <a href="https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2">Query syntax</a>.</div>



|**Query content** |**Example queries** |
|---|---|
|All logs within the specified time range |Set the time range, leave the query statement blank, and click **Search**. |
|DataFlow synchronization failures |Set the time range with the query statement `NOT success:1`, and click **Search**. |
|Logs for a specific file |Set the time range with the query statement `file_name:"file name"`, for example, `file_name:"test/example/project"`, and click **Search**. |
|All incremental import events |Set the time range with the query statement `type:"TosToNas Event"`, and click **Search**. |


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c25bcda4a6ca903ef4f501aee04c1b87.png) </span>

&nbsp;

<span id="drGVPStg"></span>
## Related operations


|Operation |Steps |
|---|---|
|Disable log analysis |Follow the steps below to disable log analysis for a DataFlow policy:<br><br><br>1. On the **DataFlow** page, select the **Policy** tab.<br><br>2. On the **Policy** tab, click the name of the policy you want to manage.<br><br>3. On the policy details page, click the **Log analysis** tab.<br><br>4. Disable log analysis by toggling the switch next to **Log analysis status**.<br><br>5. In the box that appears, click **OK**. |
|View existing logs after disabling log analysis |Disabling log analysis will prevent the creation of new logs. However, existing logs and TLS topics will not be automatically deleted. You can still view existing logs.<br><br><br>1. Log in to the [TLS console](https://console.byteplus.com/tls).<br><br>2. In the left navigation pane, select **Project**.<br><br>3. On the **Project** page, click the project named **auditlog_efs_default**.<br><br>4. On the **Topic** tab, click the topic named **auditlog_efs_dataflow**. Then, specify a time range to view the logs. |


&nbsp;
