---
title: "Overview"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/rdb-overview"
---

This topic introduces Redis's RDB analysis feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance type is the **Primary\-secondary** instance. Single node instances do not support the RDB analysis feature. For details about the feature differences between the two instance types, refer to [Feature differences](https://docs.byteplus.com/en/docs/redis/feature-faq#.5Li75aSH5a6e5L6L5ZKM5Y2V6IqC54K557G75Z6L5a6e5L6L5pSv5oyB55qE5Yqf6IO954m55oCn5pyJ5L2V5beu5Yir77yf).

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

Through RDB analysis, you can quickly detect big kKeys in the instance by analyzing the RDB files of Redis, and understand relevant information such as memory usage, distribution and expiration time of the keys, providing data reference for you to optimize big keys and avoiding issues such as insufficient memory space and performance degradation caused by big keys.

When RDB analysis cannot meet the service performance analysis requirements, you can [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files) to a local device and then use open\-source tools to analyze the backup files offline.

<span id=".5YiG5p6Q57uT5p6c"></span>
## Analysis results

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to view the analysis results, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-rdb-analysis-task">Viewing RDB analysis task</a>.</div>


<span id=".5Z-65pys5L-h5oGv"></span>
### Basic information


|Information item |Description |
|---|---|
|Instance ID |Instance ID of the current Redis instance. |
|Analysis method |Backup file analysis method adopted for the current RDB analysis task. The following analysis methods are supported:<br><br><br>* **Backup now**: A new backup file is created for analysis.<br><br>* **Select history backup**: An existing backup set is used for analysis.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating a backup, the Cache for Redis will preferentially pull data from the secondary node of the instance for backup. If there is no available secondary node for instance, it will pull data from the primary node for backup. During the backup period, it may cause a short\-term increase in instance access latency. It is recommended to perform backup\-related operations during off\-peak business hours. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/backup-recovery-intro#.5pWw5o2u5aSH5Lu9">Data backup</a>.</div><br> |
|Backup file |Information about the backup file used for RDB analysis, including the start and end times of the backup. |
|Creation time |The creation time of the RDB analysis task. |
|Start time |The time when the RDB analysis task starts to analyze the backup file after it is created. |
|End time |The time when backup file analysis ends. |


<span id=".55u45YWz5YiG54mH"></span>
### **Overview**

On the analysis results page, click the **Overview** tab to view the key distribution overview for the current RDB analysis task.

**Filter by shard**

The page provides a shard filter at the top. Use the dropdown menu to switch the analysis scope:


* **All shards**: Display the sum of RDB analysis results for all shards.

* **Specific shard**: Switch to a specific shard (e.g., server\-redis\-xxx\-1) to view its analysis data.


**Chart description**

The overview page contains the following four charts:


|**Chart name** |**Description** |
|---|---|
|Memory usage distribution |Display the memory usage distribution of various data types (e.g., stream, hash, set, string, list, zset) in a pie chart. |
|Key type distribution |Displays the distribution of Key counts for different data types (e.g., stream, hash, set, string, list, zset) in a pie chart. |
|Memory usage TTL distribution |Displays memory usage distribution as a histogram across different TTL (expiration time) ranges. TTL ranges include: Expired, 0\-1 hour, 1\-4 hours, 4\-12 hours, 12\-24 hours, 1\-7 days, 7\-30 days, greater than 30 days, and never expire.<br><br>You can use the **Show No expiry** switch to control whether to show memory data for keys that never expire in the chart. |
|Key count TTL distribution |Display the distribution of key counts across different TTL (expiration time) ranges in a histogram. TTL ranges include: Expired, 0\-1 hour, 1\-4 hours, 4\-12 hours, 12\-24 hours, 1\-7 days, 7\-30 days, greater than 30 days, and never expire.<br><br>You can use the **Show No expiry** switch to control whether to show quantity data for keys that never expire in the chart. |


<span id="z8cdWPGm"></span>
### Key details


<Tabs>
<Tab zoneid="LFX2VVhgx5" title="Top big keys">
<TabTitle>Top big keys</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">According to the RDB analysis results, the details of the top 500 keys with the largest memory usage or the largest number of elements will be displayed on the <strong>Top big keys</strong> tab.</div>


* <div data-tips="true" data-tips-type="tip">You can also click<img src="https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg" width="14px" />icon in the upper right corner of the list to export the analysis results as a CSV file, which will be automatically downloaded to your local device via the browser. You can view this file using a text\-editing tool.</div>




|Information item |Description |
|---|---|
|Key |Key name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Key names support up to 1,024 characters, and any excess characters will be automatically removed.</div><br> |
|Shard ID |The ID of the shard where the keys are located. |
|Data type |Data type of keys. For example, String, List, Set, Zset, Hash, Stream, lua or function, etc.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Redis 6.0 and earlier support displaying the lua data type, while Redis 7.0 supports displaying the function data type. The specific supported data types are subject to the information displayed on the console.</div><br> |
|Encoding |The underlying data structure adopted by the keys. |
|Expiration time |The expiration time set for the keys. |
|Memory usage |Memory usage of the keys. Unit: Byte.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Byte is the base unit for this metric. The unit displayed on the console will be flexibly converted for monitoring values according to the IEC standard (prefix of 1024). If the monitoring value of memory usage is relatively large, the units on the console may be converted to KiB, MiB, GiB, and so on.</div><br> |
|Number of element(s) |Number of elements contained in a key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the big key list, the default number of elements contained in each String key is 1.</div><br> |
|Maximum element length |The length of the largest element in the key. Unit: Byte. |
|Database name |The name of the database to which the key belongs. |





</Tab>
<Tab zoneid="uptaV6lxdO" title="Top key prefixes">
<TabTitle>Top key prefixes</TabTitle>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">According to the RDB analysis results, the details of the top 500 key prefixes with the highest memory usage or the largest number of elements will be displayed on the <strong>Top key prefixes</strong> tab.</div>


* <div data-tips="true" data-tips-type="tip">You can also click<img src="https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg" width="14px" />icon in the upper right corner of the list to export the analysis results as a CSV file, which will be automatically downloaded to your local device via the browser. You can view this file using a text\-editing tool.</div>




|Information item |Description |
|---|---|
|Key prefix |Key prefix.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Support displaying all levels of key prefixes via delimiters, helping present the true hierarchical structure of complete data, accurately locating deep\-level abnormal prefixes, and providing more precise diagnostic basis for performance optimization.</div><br> |
|Data type |Data type of keys. For example, String, List, Set, Zset, Hash, Stream, lua or function, etc.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Redis 6.0 and earlier support displaying the lua data type, while Redis 7.0 supports displaying the function data type. The specific supported data types are subject to the information displayed on the console.</div><br> |
|Number of key(s) |Number of keys using the target prefix. |
|Memory usage |Memory usage of the keys. Unit: Byte.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Byte is the base unit for this metric. The unit displayed on the console will be flexibly converted for monitoring values according to the IEC standard (prefix of 1024). If the monitoring value of memory usage is relatively large, the units on the console may be converted to KiB, MiB, GiB, and so on.</div><br> |
|Number of element(s) |Number of elements contained in a key.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the big key list, the default number of elements contained in each String key is 1.</div><br> |





</Tab>
</Tabs>
