---
title: "Extraction Parameters"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Extraction_Parameters"
---

<span id="_1-概述"></span>
# 1. Overview

Users can optimize synchronization configuration, ensure the success rate of synchronization tasks, and improve task performance by setting extraction parameters.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-常用使用场景"></span>
## 2.1 Common usage scenarios


* Professional data producers set appropriate extraction parameters (resource\-related) for synchronization tasks when creating datasets.

* General users, when a dataset synchronization task fails, can view diagnostic prompts and set appropriate extraction parameters before rerunning the task.


<span id="_2-2-使用入口"></span>
## 2.2 Entry point


* Custom SQL and table extraction settings allow configuration of **extraction parameters**


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e50aef432aa74330813a846d018da69d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f7a9d12ed5840d8b5849b900f243f12~tplv-goo7wpa0wc-image.image) </span>


* Extraction parameters can be set in [Advanced settings](https://docs.byteplus.com/docs/DataWind/Synchronization_Setting#_3-1-7-%E9%AB%98%E7%BA%A7%E8%AE%BE%E7%BD%AE).


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c620888524b644a288d786a5c95c7be9~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能说明"></span>
# 3. Feature description

<span id="_3-1-抽取参数"></span>
## 3.1 Extraction parameters

**Currently supported data source types for extraction parameters**: Mysql, Clickhouse, Oracle, SQL Server, Maxcompute, Impala, Hive_jdbc, Redshift, LAS, Presto, Databricks

**Supported parameter information:** 


|Parameter |Description |Default value |Required |Recommended value |
|---|---|---|---|---|
|prep.job.datax.channel |Read concurrency, which needs to be used in conjunction with splitPk<br><br>Recommended not to exceed: 5 (concurrency will put pressure on the target database) |Not enabled (1) |No |* No unique key: 1<br><br>* Contains a unique key such as id: less than 5 |
|prep.job.datax.partition.num |The number of partitions calculated on the Spark engine side for subsequent ETL processing after data extraction by DataX.<br><br>Usage scenario: When the target data extraction volume is very large (over 10 million rows), it is recommended to enable this to improve downstream processing speed. The recommended value is 512 (a power of 2). |Not enabled (1) |No |* Small data volume: 1<br><br>* Large data volume: 512 |
|prep.job.datax.splitPk |Description: When MysqlReader performs data extraction, if splitPk is specified, the field represented by splitPk will be used for data sharding. Datax will then start concurrent tasks for data synchronization, thus greatly improving data synchronization efficiency.<br><br>It is recommended that splitPk users use the table's primary key, as the primary key is generally evenly distributed, making it less likely for the resulting partitions to have data hotspots. Currently, splitPk only supports partitioning integer data; it does not support floating\-point, string, date, or other types. If the user specifies other unsupported types, MysqlReader will report an error. If splitPk is not specified, including not providing splitPk or leaving the splitPk value empty, DataX will treat it as using a single channel to synchronize the table data. Required: No Default value: Empty In fact, test results show that partitioning must be used together with channel. If only splitPk is enabled but the channel configuration is set to 1, there will still be no concurrency effect. |Do not enable |No |* If there is a unique key, configure it. For example, if the unique key is uid, enter: uid<br><br>* If there is no unique key, do not configure. |
|prep.job.datax.timeout |Datax task advanced configuration: the wait timeout for MaxCompute data source partition detection, in minutes. If not configured, the task will fail directly when the queried table partition is empty. |Do not enable |No |Not recommended to enable |
|prep.job.datax.disable |Disable dataX for the task |false |No |false |


<span id="_3-2-运行参数"></span>
## 3.2 Extraction parameters


|**Parameter name** |**Feature description** |**Default parameter value** |**Parameter value type** |
|---|---|---|---|
|spark.driver.cores |The number of CPUs for the driver. |2 |int |
|spark.driver.memory |The memory size of the driver. |4g |string |
|spark.driver.maxResultSize |The upper limit of data pulled to the Driver. Generally, this does not need to be adjusted. |2g (defaults to half of spark.driver.memory) |string |
|spark.executor.cores |The number of CPUs for each executor. The maximum concurrency of a Spark task is **spark.executor.cores \* number of executors** |2 |int |
|spark.executor.memory |The memory size of the executor. |4g |string |
|spark.dynamicAllocation.maxExecutors |The maximum number of executors for a single Spark task. |100 |int |
|spark.sql.autoBroadcastJoinThreshold |The broadcast threshold on the data source side. Set to \-1 to disable. Note: Disabling this does not affect Spark AQE's own broadcast. |*  |int |
|spark.sql.broadcastTimeout |Broadcast timeout period. Set to \-1 to disable the timeout limit. |*  |int |
|spark.sql.files.maxPartitionBytes |The maximum file size for each partition (Spark Partition), for splitting large files. |268435456 |int |
|spark.sql.files.openCostInBytes |Files smaller than this value will be merged (for small file merging). |8388608 |int |
