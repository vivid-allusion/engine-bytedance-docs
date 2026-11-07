---
title: "Extraction Parameters"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Extraction_Parameters"
---

<span id="_1-概述"></span>
# 1. Overview

Users can optimize synchronization configurations, ensure the success rate of synchronization tasks, and improve task performance by setting operating parameters.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios


* Professional data producers set appropriate operating parameters (resource\-related) for synchronization tasks when creating datasets.

* General users, when a dataset synchronization task fails, can review diagnostic prompts and rerun the task after setting appropriate operating parameters.


<span id="_2-2-使用入口"></span>
## 2.2 Entry point


* Custom SQL and table extraction settings allow configuration of **extraction parameters**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02fdf2f047894484b7129352fb158f20~tplv-goo7wpa0wc-image.image" width="666px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b1d342a8a344f5da016c9e1fcce0836~tplv-goo7wpa0wc-image.image" width="666px" /></div>



* Operating parameters can be set in [3.1.7 Advanced settings](https://docs.byteplus.com/docs/dataagent/Synchronization_Setting#_3-1-7-%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebe9186602ca4229836c922053b2e9ba~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能说明"></span>
# 3. Function description

<span id="_3-1-抽取参数"></span>
## 3.1 Extraction parameters

**Extraction parameters currently support the following data source types**: Mysql, Clickhouse, Oracle, SQL Server, Maxcompute, Impala, Hive_jdbc, Redshift, LAS, Presto, Databricks

**Supported parameter information:** 


|Parameter |Description |Default value |Required |Recommended value |
|---|---|---|---|---|
|prep.job.datax.channel |Read concurrency, needs to be used in conjunction with splitPk<br><br>Recommended not to exceed: 5 (concurrency will put pressure on the target database) |Disabled (1) |No |* No unique key: 1<br><br>* If the table contains a unique key such as id: less than 5. |
|prep.job.datax.partition.num |Number of partitions calculated by the Spark engine for subsequent ETL processing after datax data extraction;<br><br>Usage scenario: When the target extracted data volume is very large (more than 10 million rows), it is recommended to enable this to improve downstream processing speed. The recommended value is 512 (power of 2); |Disabled (1) |No |* Small data volume: 1<br><br>* Large data volume: 512 |
|prep.job.datax.splitPk |Description: When MysqlReader performs data extraction, if splitPk is specified, it means the user wants to use the field represented by splitPk for data partitioning. Datax will therefore start concurrent tasks for data synchronization, which can greatly improve synchronization efficiency.<br><br>It is recommended that users set splitPk to the table's primary key, as primary keys are usually evenly distributed, so the resulting partitions are less likely to cause data hotspots. Currently, splitPk only supports partitioning integer data, and does not support floating point, string, date, or other types. If the user specifies other unsupported types, MysqlReader will report an error. If splitPk is not specified, including not providing splitPk or the splitPk value is empty, DataX will treat it as using a single channel to synchronize the table data. Required: No Default value: Empty In fact, test results show that slicing must be used together with channels. If only splitpk is enabled but the channel configuration is set to 1, there will still be no concurrency effect. |Disabled |No |* If there is a unique key, configure it. For example, if the unique key is uid, enter: uid<br><br>* If there is no unique key, do not configure |
|prep.job.datax.timeout |Advanced configuration for datax tasks. The waiting timeout for MaxCompute data source partition detection, in minutes. If not configured, the task will fail immediately when the queried table partition is empty |Disabled |No |Not recommended to enable |
|prep.job.datax.disable |Disable dataX for the task |false |No |false |


<span id="_3-2-运行参数"></span>
## 3.2 Operating parameters


|**Parameter name** |**Function description** |**Default parameter value** |**Parameter value type** |
|---|---|---|---|
|spark.driver.cores |Number of CPUs for the driver |2 |int |
|spark.driver.memory |Memory size of the driver |4g |string |
|spark.driver.maxResultSize |Maximum amount of data that can be fetched to the driver. Generally, no adjustment is needed. |2g (default is half of spark.driver.memory) |string |
|spark.executor.cores |Number of CPUs for each executor. The maximum concurrency of a Spark task is **spark.executor.cores \* number of executors** |2 |int |
|spark.executor.memory |Memory size of the executor |4g |string |
|spark.dynamicAllocation.maxExecutors |Maximum number of executors for a single Spark task |100 |int |
|spark.sql.autoBroadcastJoinThreshold |Broadcast threshold on the data source side. Set to \-1 to disable. PS: Disabling does not affect Spark AQE's own broadcast |*  |int |
|spark.sql.broadcastTimeout |Broadcast timeout period. Set to \-1 to disable the timeout limit |*  |int |
|spark.sql.files.maxPartitionBytes |Maximum file size for each partition (Spark Partition), used for splitting large files |268435456 |int |
|spark.sql.files.openCostInBytes |Files smaller than this value will be merged, used for merging small files |8388608 |int |
