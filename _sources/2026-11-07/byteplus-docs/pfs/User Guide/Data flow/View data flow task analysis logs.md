---
title: "View data flow task analysis logs"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/View_DataFlow_task_analysis_logs"
---

You can use the log analysis feature to search and analyze DataFlow task logs. This article explains how to view analysis logs.

<span id="r7HSRAVl"></span>
## Background information

You can view relevant logs in the PFS or TLS console. This article only describes how to view logs in the PFS console. For log viewing steps in the TLS console, see [Query and analysis process](https://docs.byteplus.com/en/docs/tls/Query-and-analysis-process?lang=zh).

<span id="r7HSRAVl"></span>
## Prerequisites

You have created a Data Flow task. For detailed steps, see [Creating manual tasks](https://docs.byteplus.com/en/docs/pfs/Creating_manual_tasks).

<span id="3JIlpfOS"></span>
## Steps


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File** **System** \> **File** **System** **Lis**t.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, click the **Data flow** tab.

6. On the **Data flow** tab, click **Data Flow Task** \> **manual task**.

7. On the **Manual Tasks** page, click the target task name.

8. In the task details page, click the **Log Analysis** tab.

9. Enter a search query in the search box and set the time range for log data, then click **Search**.


<span id="T3SVBhZ5"></span>
## Example queries

You can refer to the following example queries to search for specific logs. For details on log search fields, see [Field descriptions](https://docs.byteplus.com/en/docs/pfs/View_DataFlow_task_analysis_logs#wxOOFDVz).


<Tabs>
<Tab zoneid="ATvnWVWHwh" title="View action records for the specified file">
<TabTitle>View action records for the specified file</TabTitle>

* Search statement: `file_name:#"<File name>"`

* Example: Query actions on the file named `example/vdb.1_4.dir/vdb_f0399.file` in the past 30 days.

   Search statement: `file_name:#"example/vdb.1_4.dir/vdb_f0399.file"`


</Tab>
<Tab zoneid="lEsMvymrF0" title="View the number of executions for a specific task type">
<TabTitle>View the number of executions for a specific task type</TabTitle>

* Search statement: `* | SELECT COUNT(*) AS totalCount WHERE type='<Task type>'`

* Example: Query actions on `TosToFileSystem Event` in the past 30 minutes.

   Search statement: `* | SELECT COUNT(*) AS totalCount WHERE type='TosToFileSystem Event'`


</Tab>
<Tab zoneid="u7BCkgX73a" title="View the number of executions for various task types">
<TabTitle>View the number of executions for various task types</TabTitle>

* Search statement: `* | SELECT type, COUNT(*) AS totalCount GROUP BY type ORDER BY totalCount DESC`

* Example: Query the number of executions of all task types in the past 30 minutes, with results sorted in descending order.

   Search statement: `* | SELECT type, COUNT(*) AS totalCount GROUP BY type ORDER BY totalCount DESC`


</Tab>
<Tab zoneid="yeN1NNK19x" title="View the total size of files for various task types">
<TabTitle>View the total size of files for various task types</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The unit of <code>totalSize</code> in the query result is <code>bytes</code>.</div>



* Search statement: `* | SELECT type, SUM(size_bytes) AS totalSize GROUP BY type ORDER BY totalSize DESC`

* Example: Query the total file size executed by all task types in the past 30 minutes, sorted in descending order.

   Search statement: `* | SELECT type, SUM(size_bytes) AS totalSize GROUP BY type ORDER BY totalSize DESC`


</Tab>
<Tab zoneid="clTXvjraKE" title="View the total number of files for various task types in a directory">
<TabTitle>View the total number of files for various task types in a directory</TabTitle>

* Search statement: `*| SELECT type, COUNT(*) AS totalCount Where file_name LIKE '<directory name>%' GROUP BY type ORDER BY totalCount DESC`

* Example: Query the total number of files executed by each task type in the `example/vdb.1_1.dir/` directory in the past 30 days, sorted in descending order.

   Search statement: `*| SELECT type, COUNT(*) AS totalCount Where file_name LIKE 'example/vdb.1_1.dir/%' GROUP BY type ORDER BY totalCount DESC`


</Tab>
<Tab zoneid="NdNZtRWUGq" title="View the total size of files for various task types in a directory">
<TabTitle>View the total size of files for various task types in a directory</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The unit of the query result <code>totalSize</code> is <code>bytes</code>.</div>



* Search statement: `* | SELECT type, SUM(size_bytes) AS totalSize Where file_name LIKE '<directory name>%' GROUP BY type ORDER BY totalSize DESC`

* Example: Query the total size of files executed by various tasks under the `example/vdb.1_1.dir/` directory for the past 30 days, ordered in descending order.

   Search statement: `* | SELECT type, SUM(size_bytes) AS totalSize Where file_name LIKE 'example/vdb.1_1.dir/%' GROUP BY type ORDER BY totalSize DESC`


</Tab>
</Tabs>


<span id="wxOOFDVz"></span>
## Field descriptions

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Some fields only appear in the logs of specific task types; please refer to the actual page for details.</div>



|Field name |Note |
|---|---|
|type |Data Flow task types. Available types are as follows:<br><br><br>* **TosToFileSystem Event**: Warm up event<br><br>* **FileSystemToTos Event**: Settlement event |
|success |Whether the data flow task was successful |
|file_name |Filename |
|size_bytes |File size |
|object_name |Object name |
|version |Object version |
|crc |Object CRC |
|inode |File inode |
|skipped |Skip |
