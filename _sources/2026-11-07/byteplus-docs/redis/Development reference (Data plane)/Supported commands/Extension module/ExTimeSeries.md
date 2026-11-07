---
title: "ExTimeSeries"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/exts"
---

Cache for Redis provides the ExTimeSeries data structure based on the open\-source Redis TimeSeries module. ExTimeSeries supports fast filtering or aggregate queries by specifying fields, simplifies the time\-series data processing process, and greatly improves performance. It meets the business requirements in scenarios of low\-latency, high\-concurrency memory read\-write access. This topic introduces the relevant information about the ExTimeSeries extension module in Cache for Redis, including its functional principles, applicable scenarios, and specific command syntax.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance version must meet the following requirements simultaneously to use the ExTimeSeries module:

   * The database version must be Redis 7.0.

   * The minor version of proxy must be greater than or equal to 1.502.0.

   * The minor version of server must be greater than or equal to 7.503.1.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the database version and minor version information of an instance on the <strong>Summary</strong> tab. For specific procedure, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

<span id=".5Yqf6IO95Y6f55CG"></span>
### Function principle


* **Introduction** **to ExTimeSeries extension module**

   The ExTimeSeries of Cache for Redis is a self\-developed extension module extended by BytePlus based on the open\-source Redis TimeSeries, combined with the usage scenarios of multi\-labels. ExTimeSeries divides the key to time\-series data into Pkey and Skey through an additional layer of Hash structure. The following table lists the detailed description of the ExTimeSeries extension module of Cache for Redis for your reference.

   
   |ExTimeSeries extension module |Description |
   |---|---|
   |`Pkey` |A Pkey is a set of timelines, and each Pkey can contain multiple Skeys. |
   |`Skey` |An Skey is a timeline, and each Skey can contain multiple chunks with a fixed capacity.<br><br>Cache for Redis supports setting different labels for each Skey, which is used to quickly filter out the target Skey from massive data. |
   |`Chunk` |The data block of time series data. The default value of a single `CHUNK_SIZE size` is 256.<br><br><br>* The meanings of `CHUNK_SIZE size` vary with different chunk encoding modes:<br><br>   * If the encoding mode is uncompressed (that is, `ENCODING` is `UNCOMPRESSED`), the meaning of `CHUNK_SIZE size` is the number of Datapoints that each chunk can store, and the default size of a single Datapoint is 16 bytes.<br><br>   * If the encoding mode is compressed (that is, `ENCODING` is `COMPRESSED`), the meaning of `CHUNK_SIZE size` is the size of each chunk. Unit: Byte.<br><br>* `CHUNK_SIZE size` can be customized. If compression is not enabled, it can store 256 Datapoints by default; if compression is enabled, it can store more than 256 Datapoints.<br><br>* A chunk is the smallest expiration unit, meaning that the chunk will be deleted only after all Datapoints in a single chunk have expired. |
   |`Datapoint` |A datapoint of time\-series data, which contains a timestamp and a value data (Double type). |
   

   A comparison diagram of Cache for Redis ExTimeSeries and the open\-source Redis TimeSeries extension module is shown below.

   
   <Tabs>
   <Tab zoneid="pdo7ACMXw5" title="Cache for Redis ExTimeSeries">
   <TabTitle>Cache for Redis ExTimeSeries</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_249061f6707ab3a73e7d89212dbed343.png) </span>
   
   
   </Tab>
   <Tab zoneid="oAlk0WQJxU" title="Open-source Redis TimeSeries">
   <TabTitle>Open-source Redis TimeSeries</TabTitle>
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb618e2c65f396b30995d2f4d47ac1dd.png) </span>
   
   
   </Tab>
   </Tabs>
   

* **Feature highlights**

   The ExTimeSeries for Redis Cache has the following feature highlights:

   * Support aggregated queries at the multi\-time series (Pkey) level.

      For example, in the financial market analysis scenario, where it is necessary to monitor daily stock price fluctuations and predict trends, you can use stocks (such as `Financial_product_stock`) as the PKey, and create Skeys named after various monitoring indicator names (such as the closing price of the day `closing_price:A`, trading volume `volume:A`, and so on) and stock codes (such as `stockid:A`). Then, by using the [EXTS.MRANGE](https://docs.byteplus.com/en/docs/redis/exts#exts-mrange) command built into ExTimeSeries, you can quickly obtain the monitoring information related to the stock price fluctuations of the stock with code A. However, if you use the open\-source Redis TimeSeries, you need to perform a large number of aggregation operations in the business code to achieve the above mentioned query.

   * Support aggregate queries through custom sampling intervals (timeBucket), tag filtering (Filter), and common numerical functions to reduce network interactions and improve query efficiency.

   * Support for increasing and decreasing time\-series data at specified time points.

   * Support for setting the expiration time (Retention time) attribute for Skey to ensure that data on each timeline can be automatically cleaned up according to the time window.

   * Support for combining efficient compression algorithms with specific storage technologies to reduce storage costs.


<span id=".6YCC55So5Zy65pmv"></span>
### Applicable scenarios

The ExTimeSeries extension module for Cache for Redis is applicable to the following scenarios:


* Monitoring system scenario

   Large data centers need to monitor server performance indicators in real\-time. The development and operation and maintenance team can use ExTimeSeries to achieve fast storage and query, helping developers to detect performance issues and abnormal user behaviors in a timely manner.

* E\-commerce data analysis scenario

   ExTimeSeries can perform real\-time statistics on the number of page views, the number of product clicks and purchases on e\-commerce websites, analyze product purchase trends, and assist enterprises in formulating adjustment plans for product strategies.

* Financial risk control scenario

   Financial institutions can use ExTimeSeries to process and analyze high\-frequency time\-sensitive data such as stock prices and trading volumes, providing data support for financial analysts to conduct market analysis and risk assessment.

* Internet of Things (IoT) scenario

   ExTimeSeries can play an important role in real\-time monitoring of the status and performance of smart factory equipment. Through anomaly detection and usage trend analysis of equipment, it provides predictive guidance for equipment usage strategies, maintenance and replacement times.


<span id=".5ZG95Luk6K-t5rOV"></span>
## Command syntax

<span id=".5ZG95Luk5YiX6KGo"></span>
### Command list

The commands supported by ExTimeSeries are shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the command syntax in the following table, the definitions are as follows:</div>



* <div data-tips="true" data-tips-type="tip"><code>UPPERCASE KEYWORD</code>: Command keyword, such as <code>EXTS.PCREATE</code>.</div>


* <div data-tips="true" data-tips-type="tip"><code>lowercase keyword</code>: Customizable parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code>[]</code>: The content within <code>[]</code> is an optional parameter, and the content outside <code>[]</code> is a required parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code><Option 1>|<Option 2>|<Option n></code>: A set of mutually exclusive parameter options, meaning only one parameter can be selected from the options for setting.</div>




<Tabs>
<Tab zoneid="IQPOcl667Y" title="Write command">
<TabTitle>Write command</TabTitle>


|command |Syntax |Description |
|---|---|---|
|[EXTS.PCREATE](https://docs.byteplus.com/en/docs/redis/exts#exts-pcreate) |`EXTS.PCREATE Pkey` |Create a new Pkey (ExTimeSeries). Creation fails if the Pkey already exists. |
|[EXTS.CREATE](https://docs.byteplus.com/en/docs/redis/exts#exts-create) |`EXTS.CREATE Pkey Skey [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 label2 val2 ...]` |Create an Skey within the specified Pkey. If the Pkey does not exist, a new Pkey will be automatically created. If the Skey already exists, the creation will fail.<br><br>You can set attributes such as expiration time, whether to enable compression, and labels for the SKey during creation. |
|[EXTS.ALTER](https://docs.byteplus.com/en/docs/redis/exts#exts-alter) |`EXTS.ALTER Pkey Skey [RETENTION time]` |Modify the attributes of the target Skey in the specified Pkey. Currently, only the expiration time (that is, `RETENTION time`) can be modified. |
|[EXTS.ADD](https://docs.byteplus.com/en/docs/redis/exts#exts-add) |`EXTS.ADD Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |Insert a Datapoint into the target Skey within the specified Pkey. If Pkey or Skey does not exist, it will be automatically created. Attributes such as the expiration time of Skey, whether compression is enabled, and labels only take effect when Skey needs to be automatically created. |
|[EXTS.MODIFY](https://docs.byteplus.com/en/docs/redis/exts#exts-modify) |`EXTS.MODIFY Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |Modify the Datapoint data value at the specified time point in the target Skey. If Pkey or Skey does not exist, it will be automatically created. Attributes such as the expiration time of Skey, whether compression is enabled, and labels only take effect when Skey needs to be automatically created. |
|[EXTS.INCRBY](https://docs.byteplus.com/en/docs/redis/exts#exts-incrby) |`EXTS.INCRBY Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |Insert a Datapoint into the target Skey in the specified Pkey, and increment it by adding the value in the command to the value set for the **latest** Datapoint in the target Skey. If you specify the value in the command as a negative number, it will be decremented.<br><br>If Pkey or Skey does not exist, it will be automatically created. The initial value of Datapoint in the newly created Skey is set to 0 by default.<br><br>The attributes of Skey, such as expiration time, whether compression is enabled, and labels, only take effect when Skey needs to be automatically created. |
|[EXTS.INCRBY_TS](https://docs.byteplus.com/en/docs/redis/exts#exts-incrby-ts) |`EXTS.INCRBY_TS Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |Increment by adding the value in the command to the value set for the Datapoint at the **specified time point** in the target Skey. If you specify the value in the command as a negative number, it will be decremented.<br><br>If Pkey or Skey does not exist, it will be automatically created. The initial value of Datapoint in the newly created Skey is set to 0 by default.<br><br>The attributes of Skey, such as expiration time, whether compression is enabled, and labels, only take effect when Skey needs to be automatically created. |
|[EXTS.MADD](https://docs.byteplus.com/en/docs/redis/exts#exts-madd) |`EXTS.MADD Pkey Skey timestamp value [Skey timestamp value ...]` |Insert Datapoint data for multiple Skeys in the specified Pkey respectively.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|[EXTS.MMODIFY](https://docs.byteplus.com/en/docs/redis/exts#exts-mmodify) |`EXTS.MMODIFY Pkey Skey timestamp value [Skey timestamp value ...]` |Modify the data values of Datapoints at the specified time points in multiple Skeys in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|[EXTS.MINCRBY](https://docs.byteplus.com/en/docs/redis/exts#exts-mincrby) |`EXTS.MINCRBY Pkey Skey timestamp value [Skey timestamp value ...]` |Insert a Datapoint for each of the multiple Skeys in the specified Pkey, and increment by adding the value in this command to the value of the **latest** Datapoint in each Skey. If you specify the value in the command as a negative number, it will be decremented.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|[EXTS.MINCRBY_TS](https://docs.byteplus.com/en/docs/redis/exts#exts-mincrby-ts) |`EXTS.MINCRBY_TS Pkey Skey timestamp value [Skey timestamp value ...]` |Modify the value of Datapoint in multiple target Skeys in batches. The value in this command will be added to the value set by the Datapoint at the **specified time point** in the target Skey to achieve an increment. If you specify the value in the command as a negative number, it will be decremented.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|[EXTS.DEL](https://docs.byteplus.com/en/docs/redis/exts#exts-del) |`EXTS.DEL Pkey Skey` |Delete the target Skey in the specified Pkey, including all Datapoint data in this Skey.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When there is no Skey in the Pkey, the Pkey will be automatically deleted.</div><br> |





</Tab>
<Tab zoneid="N0AMy7sAhC" title="Query command">
<TabTitle>Query command</TabTitle>


|command |Syntax |Description |
|---|---|---|
|[EXTS.GET](https://docs.byteplus.com/en/docs/redis/exts#exts-get) |`EXTS.GET Pkey Skey` |Query the latest Datapoint data in the target Skey of the specified Pkey. |
|[EXTS.INFO](https://docs.byteplus.com/en/docs/redis/exts#exts-info) |`EXTS.INFO Pkey Skey` |Query the attribute information of the target Skey in the specified Pkey, including the number of Datapoints, the timestamp and value of the latest Datapoint, and the labels of the Skey. |
|[EXTS.QUERYINDEX](https://docs.byteplus.com/en/docs/redis/exts#exts-queryindex) |`EXTS.QUERYINDEX Pkey filter1 [filter2 ...]` |Query Skeys that meet the custom filtering criteria (filter) from the specified Pkey. |
|[EXTS.RANGE](https://docs.byteplus.com/en/docs/redis/exts#exts-range) |`EXTS.RANGE Pkey Skey fromTimestamp toTimestamp [COUNT count] [AGGREGATION aggregationType timeBucket]` |Query Datapoint data within the specified time period (that is, including the specified time point) in the target Skey. |
|[EXTS.MRANGE](https://docs.byteplus.com/en/docs/redis/exts#exts-mrange) |`EXTS.MRANGE Pkey fromTimestamp toTimestamp [COUNT count] [AGGREGATION aggregationType timeBucket] [WITHLABELS] FILTER filter1 [filter2 ...]` |Query the detailed information of Skeys that meet the custom filtering criteria (filter) within a specified time period (including the specified time point) in the target Pkey, including the Skey name, contained labels, and Datapoint data. |
|[EXTS.PRANGE](https://docs.byteplus.com/en/docs/redis/exts#exts-prange) |`EXTS.PRANGE Pkey fromTimestamp toTimestamp pkeyAggregationType pkeyTimeBucket [COUNT count] [AGGREGATION aggregationType timeBucket] [WITHLABELS] FILTER filter1 [filter2 ...]` |Aggregate Datapoint data that meets the custom filtering criteria (filter) within a specified time period at the Pkey level in the target Pkey.<br><br>If you specify aggregations at both the Pkey and Skey levels simultaneously, the aggregation at the Skey level will be performed first (the usage method is the same as the [EXTS.MRANGE](https://docs.byteplus.com/en/docs/redis/exts#exts-mrange) command), and then a secondary aggregation will be performed on the result of the first aggregation at the Pkey level. |





</Tab>
</Tabs>


<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* To use ExTimeSeries features, [submit a ticket](https://console.byteplus.com/workorder/create/) to technical support to apply for usage.

* After the application is completed, accounts with the Administrator role will have all permissions for ExTimeSeries related commands by default. You can also create a new role that allows the use of all ExTimeSeries commands according to business needs (that is, the ACL rule of this role needs to be set to `+@exts`). After creating the role, you need to log in to Redis with an account that has this role to use ExTimeSeries related commands. For specific procedures about creating a role, refer to [Creating role](https://docs.byteplus.com/en/docs/redis/create-role).

* The Cache for Redis supports big and hot key analysis for the ExTimeSeries data type. It can help timely discover and analyze the details of hot keys and big keys in the database, providing data references for you to optimize hot keys and big keys. For specific procedures, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis) and [Hot key analysis](https://docs.byteplus.com/en/docs/redis/hot-key-analysis).

* After successfully applying for the use of the ExTimeSeries function, the instance will no longer support any data recovery functions, including:

   * [Recovery from backup set](https://docs.byteplus.com/en/docs/redis/recovery-from-backup-set)

   * [Recovery by point in time](https://docs.byteplus.com/en/docs/redis/recovery-by-time-point)

   * [Recovery from deleted instance](https://docs.byteplus.com/en/docs/redis/restore-deleted-instance)

* Cache for Redis supports deleting the target Skey of the specified Pkey in ExTimeSeries through [EXTS.DEL](https://docs.byteplus.com/en/docs/redis/exts#exts-del) command, including all Datapoint data in this Skey. When there is no Skey in the Pkey, the Pkey will be automatically deleted.

   You can also use the following native Redis command to achieve the purpose of deleting ExTimeSeries.

   
   |command |Syntax |Description |
   |---|---|---|
   |[EXPIRE](https://redis.io/docs/latest/commands/expire/) |`EXPIRE Pkey seconds [NX \| XX \| GT \| LT]` |Set the timeout for ExTimeSeries. ExTimeSeries that exceeds this time will be automatically deleted. |
   |[UNLINK](https://redis.io/docs/latest/commands/unlink/) |`UNLINK Pkey [Pkey ...]` |Asynchronously delete one or more ExTimeSeries. When deleting an ExTimeSeries with the `UNLINK` command, this ExTimeSeries is marked as pending deletion, and the actual delete actions are carried out in the background thread without blocking the current Redis process. |
   |[DEL](https://redis.io/commands/del) |`DEL Pkey [Pkey ...]` |Synchronously delete one or more ExTimeSeries. When deleting ExTimeSeries with the `DEL` command, the delete action immediately blocks the current Redis thread until the memory space corresponding to ExTimeSeries is completely withdrawn. If the amount of ExTimeSeries data to be deleted is too large, it may affect the overall performance of Redis. |
   


<span id="exts-pcreate"></span>
### EXTS.PCREATE


|Category |Description |
|---|---|
|Command syntax |`EXTS.PCREATE Pkey` |
|Time complexity |O(1). |
|Command description |Create a new Pkey (ExTimeSeries). Creation fails if the Pkey already exists. |
|Option |`Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Create an ExTimeSeries with the Pkey named `test_exts`.<br><br>```Bash```<br>```EXTS.PCREATE test_exts```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="exts-create"></span>
### EXTS.CREATE


|Category |Description |
|---|---|
|Command syntax |`EXTS.CREATE Pkey Skey [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 label2 val2 ...]` |
|Time complexity |O(1). |
|Command description |Create an Skey within the specified Pkey. If the Pkey does not exist, a new Pkey will be automatically created. If the Skey already exists, the creation will fail.<br><br>You can set attributes such as expiration time, whether to enable compression, and labels for the SKey during creation. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `RETENTION time`: The relative expiration time of Datapoint data. Unit: milliseconds. The value cannot exceed 1 trillion milliseconds. If this parameter is not filled in, it indicates no expiration time is set, that is, the data will not expire.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When all Datapoint data in the Skey has expired, the Skey will be automatically deleted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When there is no Skey in the Pkey, the Pkey will be automatically deleted.   </div><br>   <br><br>* `CHUNK_SIZE size`: The size of a single chunk for storing Datapoint data. Default value: 256.<br><br>   The meanings of `CHUNK_SIZE size` vary with different chunk encoding modes. For more details about `CHUNK_SIZE size`, refer to [Introduction to ExTimeSeries](https://docs.byteplus.com/en/docs/redis/exts#.5Yqf6IO95Y6f55CG).<br><br>* `ENCODING`: Set whether to enable compression for Skey. If this parameter is not filled in, it means that compression is enabled by default (that is, `COMPRESSED`).<br><br>* `LABELS`: Labels for Skey, which supports setting multiple sets of labels simultaneously. For each set of labels, the corresponding label name and label value need to be set at the same time. For example, `LABELS stockid A issuer 1`. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |* Command example 1<br><br>   Create an ExTimeSeries with Pkey named `test_exts`, Skey named `closing_price`, set the relative expiration time of this Skey to 10,000,000 milliseconds, and include 2 labels as `stockid A` and `issuer 1`.<br><br>   ```Bash```<br>```   EXTS.CREATE test_exts closing_price RETENTION 10000000 LABELS stockid A issuer 1```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   OK```<br>```   ```<br>   <br><br>* Command example 2<br><br>   Create an Skey named `volume` for the existing ExTimeSeries with Pkey named `test_exts`, and set the absolute expiration time of this Skey to 20,000,000 milliseconds, with a chunk size of 150.<br><br>   ```Bash```<br>```   EXTS.CREATE test_exts volume RETENTION 20000000 CHUNK_SIZE 150```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   OK```<br>```   ```<br>    |


<span id="exts-alter"></span>
### EXTS.ALTER


|Category |Description |
|---|---|
|Command syntax |`EXTS.ALTER Pkey Skey [RETENTION time]` |
|Time complexity |O(1). |
|Command description |Modify the attributes of the target Skey in the specified Pkey. Currently, only modifying the expiration time (i.e., `RETENTION time`) is supported. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `RETENTION time`: The relative expiration time of Datapoint data. Unit: milliseconds. The value cannot exceed 1 trillion milliseconds. If this parameter is not filled in, it indicates no expiration time is set, that is, the data will not expire.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When all Datapoint data in the Skey has expired, the Skey will be automatically deleted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When there is no Skey in the Pkey, the Pkey will be automatically deleted.   </div><br>    |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Change the expiration time of the Skey named `volume` in `test_exts` to 15,000,000.<br><br>```Bash```<br>```EXTS.ALTER test_exts volume RETENTION 15000000```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="exts-add"></span>
### EXTS.ADD


|Category |Description |
|---|---|
|Command syntax |`EXTS.ADD Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |
|Time complexity |O(1). |
|Command description |Insert a Datapoint into the target Skey within the specified Pkey. If Pkey or Skey does not exist, it will be automatically created. Attributes such as the expiration time of Skey, whether compression is enabled, and labels only take effect when Skey needs to be automatically created. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be inserted. Unit: milliseconds. The symbol `*` is supported to represent the current system timestamp.<br><br>* `value`: The data value to be inserted into the Datapoint, with a data type of Double.<br><br>* `RETENTION time`: The relative expiration time of Datapoint data. Unit: milliseconds. The value cannot exceed 1 trillion milliseconds. If this parameter is not filled in, it indicates no expiration time is set, that is, the data will not expire.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When all Datapoint data in the Skey has expired, the Skey will be automatically deleted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When there is no Skey in the Pkey, the Pkey will be automatically deleted.   </div><br>   <br><br>* `CHUNK_SIZE size`: The size of a single chunk for storing Datapoint data. Default value: 256.<br><br>   The meanings of `CHUNK_SIZE size` vary with different chunk encoding modes. For more details about `CHUNK_SIZE size`, refer to [Introduction to ExTimeSeries](https://docs.byteplus.com/en/docs/redis/exts#.5Yqf6IO95Y6f55CG).<br><br>* `ENCODING`: Set whether to enable compression for Skey. If this parameter is not filled in, it means that compression is enabled by default (that is, `COMPRESSED`).<br><br>* `LABELS`: Labels for Skey, which supports setting multiple sets of labels simultaneously. For each set of labels, the corresponding label name and label value need to be set at the same time. For example, `LABELS stockid A issuer 1`. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Create an Skey named `issuer` for the existing ExTimeSeries with Pkey named `test_exts`, and insert a Datapoint data with a value of `66.0` and a timestamp of the current system timestamp for this Skey. When creating the Skey, set its relative expiration time to 10,000,000 milliseconds and include the `stockid A` label.<br><br>```Bash```<br>```EXTS.ADD test_exts issuer * 66.0 RETENTION 10000000 LABELS stockid A```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="exts-modify"></span>
### EXTS.MODIFY


|Category |Description |
|---|---|
|Command syntax |`EXTS.MODIFY Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |
|Time complexity |O(1). |
|Command description |Modify the Datapoint data value at the specified time point in the target Skey. If Pkey or Skey does not exist, it will be automatically created. Attributes such as the expiration time of Skey, whether compression is enabled, and labels only take effect when Skey needs to be automatically created. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be updated. Unit: milliseconds.<br><br>* `value`: The data value to be updated in the Datapoint, with a data type of Double.<br><br>* `RETENTION time`: The relative expiration time of Datapoint data. Unit: milliseconds. The value cannot exceed 1 trillion milliseconds. If this parameter is not filled in, it indicates no expiration time is set, that is, the data will not expire.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When all Datapoint data in the Skey has expired, the Skey will be automatically deleted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When there is no Skey in the Pkey, the Pkey will be automatically deleted.   </div><br>   <br><br>* `CHUNK_SIZE size`: The size of a single chunk for storing Datapoint data. Default value: 256.<br><br>   The meanings of `CHUNK_SIZE size` vary with different chunk encoding modes. For more details about `CHUNK_SIZE size`, refer to [Introduction to ExTimeSeries](https://docs.byteplus.com/en/docs/redis/exts#.5Yqf6IO95Y6f55CG).<br><br>* `ENCODING`: Set whether to enable compression for Skey. If this parameter is not filled in, it means that compression is enabled by default (that is, `COMPRESSED`).<br><br>* `LABELS`: Labels for Skey, which supports setting multiple sets of labels simultaneously. For each set of labels, the corresponding label name and label value need to be set at the same time. For example, `LABELS stockid A issuer 1`. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Change the Datapoint data value of Skey `closing_price` in `test_exts` at the specified time point to 89.0.<br><br>```Bash```<br>```EXTS.MODIFY test_exts closing_price 1744255211538 89.0```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="exts-incrby"></span>
### EXTS.INCRBY


|Category |Description |
|---|---|
|Command syntax |`EXTS.INCRBY Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |
|Time complexity |O(1). |
|Command description |Insert a Datapoint into the target Skey in the specified Pkey, and increment it by adding the value in the command to the value set for the **latest** Datapoint in the target Skey. If you specify the value in the command as a negative number, it will be decremented.<br><br>If Pkey or Skey does not exist, it will be automatically created. The initial value of Datapoint in the newly created Skey is set to 0 by default.<br><br>The attributes of Skey, such as expiration time, whether compression is enabled, and labels, only take effect when Skey needs to be automatically created. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be updated. Unit: milliseconds. The symbol `*` is supported to represent the current system timestamp.<br><br>* `value`: The value to be incremented, with a data type of Double. If you specify the value as a negative number, it will be decremented.<br><br>* `RETENTION time`: The relative expiration time of Datapoint data. Unit: milliseconds. The value cannot exceed 1 trillion milliseconds. If this parameter is not filled in, it indicates no expiration time is set, that is, the data will not expire.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When all Datapoint data in the Skey has expired, the Skey will be automatically deleted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When there is no Skey in the Pkey, the Pkey will be automatically deleted.   </div><br>   <br><br>* `CHUNK_SIZE size`: The size of a single chunk for storing Datapoint data. Default value: 256.<br><br>   The meanings of `CHUNK_SIZE size` vary with different chunk encoding modes. For more details about `CHUNK_SIZE size`, refer to [Introduction to ExTimeSeries](https://docs.byteplus.com/en/docs/redis/exts#.5Yqf6IO95Y6f55CG).<br><br>* `ENCODING`: Set whether to enable compression for Skey. If this parameter is not filled in, it means that compression is enabled by default (that is, `COMPRESSED`).<br><br>* `LABELS`: Labels for Skey, which supports setting multiple sets of labels simultaneously. For each set of labels, the corresponding label name and label value need to be set at the same time. For example, `LABELS stockid A issuer 1`. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |For example, the value of the most recent Datapoint of Skey `closing_price` in `Pkey test_exts` is `8.0`. You can increment the value of this Skey through the following command.<br><br>```Bash```<br>```EXTS.INCRBY test_exts closing_price * 3```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br><br><br>If the command `EXTS.GET test_exts closing_price` is executed at this time, the following results will be returned.<br><br>```Bash```<br>```1) (integer) 1744254273078```<br>```2) "11"```<br> |


<span id="exts-incrby-ts"></span>
### EXTS.INCRBY_TS


|Category |Description |
|---|---|
|Command syntax |`EXTS.INCRBY_TS Pkey Skey timestamp value [RETENTION time] [CHUNK_SIZE size] [ENCODING <COMPRESSED\|UNCOMPRESSED>] [LABELS label1 val1 ...]` |
|Time complexity |O(1). |
|Command description |Increment by adding the value in the command to the value set for the Datapoint at the **specified time point** in the target Skey. If you specify the value in the command as a negative number, it will be decremented.<br><br>If Pkey or Skey does not exist, it will be automatically created. The initial value of Datapoint in the newly created Skey is set to 0 by default.<br><br>The attributes of Skey, such as expiration time, whether compression is enabled, and labels, only take effect when Skey needs to be automatically created. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be updated. Unit: milliseconds.<br><br>* `value`: The value to be incremented, with a data type of Double. If you specify the value as a negative number, it will be decremented.<br><br>* `RETENTION time`: The relative expiration time of Datapoint data. Unit: milliseconds. The value cannot exceed 1 trillion milliseconds. If this parameter is not filled in, it indicates no expiration time is set, that is, the data will not expire.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When all Datapoint data in the Skey has expired, the Skey will be automatically deleted.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When there is no Skey in the Pkey, the Pkey will be automatically deleted.   </div><br>   <br><br>* `CHUNK_SIZE size`: The size of a single chunk for storing Datapoint data. Default value: 256.<br><br>   The meanings of `CHUNK_SIZE size` vary with different chunk encoding modes. For more details about `CHUNK_SIZE size`, refer to [Introduction to ExTimeSeries](https://docs.byteplus.com/en/docs/redis/exts#.5Yqf6IO95Y6f55CG).<br><br>* `ENCODING`: Set whether to enable compression for Skey. If this parameter is not filled in, it means that compression is enabled by default (that is, `COMPRESSED`).<br><br>* `LABELS`: Labels for Skey, which supports setting multiple sets of labels simultaneously. For each set of labels, the corresponding label name and label value need to be set at the same time. For example, `LABELS stockid A issuer 1`. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |For example, in Pkey `test_exts`, the Datapoint value of Skey `closing_price` at the specified time point is 70.0. You can use the following command to decrease the value of this Skey.<br><br>```Bash```<br>```EXTS.INCRBY_TS test_exts closing_price 1744254890238 -30.0```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br><br><br>If the command `EXTS.GET test_exts closing_price` is executed at this time, the following results will be returned.<br><br>```Bash```<br>```1) (integer) 1744254890238```<br>```2) "40"```<br> |


<span id="exts-madd"></span>
### EXTS.MADD


|Category |Description |
|---|---|
|Command syntax |`EXTS.MADD Pkey Skey timestamp value [Skey timestamp value ...]` |
|Time complexity |O(N), where N is the number of Datapoints to be inserted. |
|Command description |Insert Datapoint data for multiple Skeys in the specified Pkey respectively.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be inserted. Unit: milliseconds. The symbol `*` is supported to represent the current system timestamp.<br><br>* `value`: The data value to be inserted into the Datapoint, with a data type of Double. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Insert a Datapoint for `volume` and `closing_price` Skeys in Pkey `test_exts` respectively.<br><br>```Bash```<br>```EXTS.MADD test_exts volume * 66.0 closing_price * 8.0```<br><br><br>Response example.<br><br>```Bash```<br>```1) OK```<br>```2) OK```<br> |


<span id="exts-mmodify"></span>
### EXTS.MMODIFY


|Category |Description |
|---|---|
|Command syntax |`EXTS.MMODIFY Pkey Skey timestamp value [Skey timestamp value ...]` |
|Time complexity |O(N), where N is the number of Datapoints to be inserted. |
|Command description |Modify the data values of Datapoints at the specified time points in multiple Skeys in batches.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be updated. Unit: milliseconds.<br><br>* `value`: The data value to be updated in the Datapoint, with a data type of Double. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Change the Datapoint data values of the two Skeys, `closing_price` and `volume` in `test_exts` to 56.0 and 70.0 respectively.<br><br>```Bash```<br>```EXTS.MMODIFY test_exts closing_price 1744255211538 56.0 volume 1744254890238 70.0```<br><br><br>Response example.<br><br>```Bash```<br>```1) OK```<br>```2) OK```<br> |


<span id="exts-mincrby"></span>
### EXTS.MINCRBY


|Category |Description |
|---|---|
|Command syntax |`EXTS.MINCRBY Pkey Skey timestamp value [Skey timestamp value ...]` |
|Time complexity |O(N), where N is the number of Datapoints to be inserted. |
|Command description |Insert a Datapoint for each of the multiple Skeys in the specified Pkey, and increment by adding the value in this command to the value of the **latest** Datapoint in each Skey. If you specify the value in the command as a negative number, it will be decremented.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be updated. Unit: milliseconds. The symbol `*` is supported to represent the current system timestamp.<br><br>* `value`: The value to be incremented, with a data type of Double. If you specify the value as a negative number, it will be decremented. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```EXTS.MINCRBY test_exts closing_price * -3.0 volume * 4.0```<br><br><br>Response example.<br><br>```Bash```<br>```1) OK```<br>```2) OK```<br> |


<span id="exts-mincrby-ts"></span>
### EXTS.MINCRBY_TS


|Category |Description |
|---|---|
|Command syntax |`EXTS.MINCRBY_TS Pkey Skey timestamp value [Skey timestamp value ...]` |
|Time complexity |O(1). |
|Command description |Modify the value of Datapoint in multiple target Skeys in batches. The value in this command will be added to the value set by the Datapoint at the **specified time point** in ** ** the target Skey to achieve an increment. If you specify the value in the command as a negative number, it will be decremented.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The Skey must exist, otherwise an error will occur when executing the command.</div><br> |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `timestamp`: The Unix timestamp of the Datapoint to be updated. Unit: milliseconds.<br><br>* `value`: The value to be incremented, with a data type of Double. If you specify the value as a negative number, it will be decremented. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```EXTS.MINCRBY_TS test_exts closing_price 1744257305364 -25.0 volume 1744254890238 62.0```<br><br><br>Response example.<br><br>```Bash```<br>```1) OK```<br>```2) OK```<br> |


<span id="exts-del"></span>
### EXTS.DEL


|Category |Description |
|---|---|
|Command syntax |`EXTS.DEL Pkey Skey` |
|Time complexity |O(1). |
|Command description |Delete the target Skey in the specified Pkey, including all Datapoint data in this Skey.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When there is no Skey in the Pkey, the Pkey will be automatically deleted.</div><br> |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey. |
|Response |* `OK`: Execution succeeded.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```EXTS.DEL test_exts closing_price```<br><br><br>Response example.<br><br>```Bash```<br>```OK```<br> |


<span id="exts-get"></span>
### EXTS.GET


|Category |Description |
|---|---|
|Command syntax |`EXTS.GET Pkey Skey` |
|Time complexity |O(1). |
|Command description |Query the latest Datapoint data in the target Skey of the specified Pkey. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey. |
|Response |* Execution succeeded: Return the corresponding Datapoint data.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```EXTS.GET test_exts closing_price```<br><br><br>Response example.<br><br>```Bash```<br>```1) (integer) 1744254402895```<br>```2) "8"```<br> |


<span id="exts-info"></span>
### EXTS.INFO


|Category |Description |
|---|---|
|Command syntax |`EXTS.INFO Pkey Skey` |
|Time complexity |O(1). |
|Command description |Query the attribute information of the target Skey in the specified Pkey, including the number of Datapoints, the timestamp and value of the latest Datapoint, and the labels of the Skey. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey. |
|Response |* Execution succeeded: return the information list of the Skey.<br><br>* Other cases reply corresponding exception information. |
|Example |Command example.<br><br>```Bash```<br>```EXTS.INFO test_exts closing_price```<br><br><br>Response example.<br><br>```Bash```<br>```1) totalDataPoints```<br>```2) (integer) 4```<br>```3) maxDataPoints```<br>```4) (integer) 0```<br>```5) maxDataPointsPerChunk```<br>```6) (integer) 256```<br>```7) dataPointsExpireTime```<br>```8) (integer) 0```<br>```9) lastTimestamp```<br>```10) (integer) 1744254402895```<br>```11) chunkCount```<br>```12) (integer) 1```<br>```13) lastValue```<br>```14) (integer) 8```<br>```15) labels```<br>```16) 1) 1) "stockid"```<br>```      2) "A"```<br>```   2) 1) "issuer"```<br>```      2) "1"```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter description of the return result is as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>totalDataPoints</code>: The number of Datapoints currently stored in the Skey.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>maxDataPoints</code>: The upper limit of the number of Datapoints that can be stored in the current Skey. The default value is 0, indicating no upper limit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>maxDataPointsPerChunk</code>: The chunk size (<code>CHUNK_SIZE size</code>) set when creating the Skey.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>dataPointsExpireTime</code>: The relative expiration time (<code>RETENTION time</code>) of the current Skey, in milliseconds. 0 means it will not expire.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>lastTimestamp</code>: The Unix timestamp of the latest Datapoint. Unit: milliseconds.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>chunkCount</code>: The number of chunks in the current Skey.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>lastValue</code>: The value of the latest Datapoint.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>labels</code>: Information about the label set (including label names and label values) set for the current Skey.</div><br> |


<span id="exts-queryindex"></span>
### EXTS.QUERYINDEX


|Category |Description |
|---|---|
|Command syntax |`EXTS.QUERYINDEX Pkey filter1 [filter2 ...]` |
|Time complexity |O(N), where N is the maximum number of sets matching the filter criteria. |
|Command description |Query Skeys that meet the custom filtering criteria (filter) from the specified Pkey. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `filter`: Filter conditions. Cache for Redis supports the use of multiple commands and command combinations in custom filter conditions (filter), but must include at least one of the `EQ`, `CONTAINS`, `LIST_MATCH` logics. For more details about `filter`, refer to [Conditional query syntax](https://docs.byteplus.com/en/docs/redis/exts#.5p2h5Lu25p-l6K-i6K-t5rOV). |
|Response |* If the execution is successful, it will return the Skey that meets the filter conditions.<br><br>* Other cases reply corresponding exception information. |
|Example |* Command example 1<br><br>   Filter out all Skeys from Pkey `test_exts` where the `stockid` tag is `A` or `B`, and the `issuer` label is not `1`.<br><br>   ```Bash```<br>```   EXTS.QUERYINDEX test_exts stockid=(A,B) issuer!=1```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   1) "closing_price"```<br>```   2) "volume2"```<br>```   ```<br>   <br><br>* Command example 2<br><br>   Filter out all Skeys that contain the `stockid` label from Pkey `test_exts`.<br><br>   ```Bash```<br>```   EXTS.QUERYINDEX test_exts stockid!=```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   1) "closing_price"```<br>```   2) "closing_price2"```<br>```   3) "volume1"```<br>```   4) "volume2"```<br>```   5) "isser"```<br>```   ```<br>    |


<span id="exts-range"></span>
### EXTS.RANGE


|Category |Description |
|---|---|
|Command syntax |`EXTS.RANGE Pkey Skey fromTimestamp toTimestamp [COUNT count] [AGGREGATION aggregationType timeBucket]` |
|Time complexity |O(N), where N is the number of data chunks of the target Datapoint. |
|Command description |Query Datapoint data within the specified time period (that is, including the specified time point) in the target Skey. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `Skey`: The name of Skey.<br><br>* `fromTimestamp`: Start time of query, in the format of Unix timestamp. Unit: milliseconds.<br><br>* `toTimestamp`: End time of query, in the format of Unix timestamp. Unit: milliseconds. The symbol `*` is allowed to represent the current system timestamp. If this value is equal to `fromTimestamp`, it means the query only includes Datapoint data at that specific time point.<br><br>* `COUNT count`: Specify the upper limit of the number of Datapoints that can be returned. The value must not exceed 100,000. If this parameter is not filled, it means that a maximum of 100,000 Datapoint data can be returned.<br><br>* `AGGREGATION`: Set the aggregation query conditions for Skey, including:<br><br>   * `aggregationType`: Aggregation type. For example, you can aggregate by maximum value (`MAX`), minimum value (`MIN`), average value (`AVG`) and so on.<br><br>   * `timeBucket`: Sampling interval. Unit: milliseconds. The minimum sampling interval is 1,000 milliseconds.<br><br>      Cache for Redis will aggregate the data within the sampling interval according to the specified type and return the result. The returned time point is the start time of the sampling interval. For example, `AGGREGATION MAX 3000` means that the maximum value within every 3,000 milliseconds will be returned. For more details, refer to [Aggregation query syntax](https://docs.byteplus.com/en/docs/redis/exts#.6IGa5ZCI5p-l6K-i6K-t5rOV). |
|Response |* Execution succeeded: Return Datapoint data that meets the query conditions. If an aggregation query condition is specified in the command, return the aggregated result.<br><br>* Other cases reply corresponding exception information. |
|Example |Query the maximum value every 3,000 milliseconds within the specified time period from the Skey `closing_price` of Pkey `test_exts`, and allow a maximum of 2 pieces of data to be returned.<br><br>```Bash```<br>```EXTS.RANGE test_exts closing_price 1743566159000 * COUNT 2 AGGREGATION MAX 3000```<br><br><br>Response example.<br><br>```Bash```<br>```1) 1) 1) (integer) 1744255152000```<br>```      2) "73"```<br>```   2) 1) (integer) 1744255167000```<br>```      2) "76"```<br>```2) (integer) 1```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The information on the last line of the returned result can be used to determine whether all Datapoint data that meet the conditions have been displayed. Among them:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>0</code>: All data has been displayed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>1</code>: Some data that meets the criteria has not been displayed. If you need to obtain more Datapoint data that meets the query criteria, you can use the timestamp of the last Datapoint in the returned results as the start time of the next query and continue the traversal query, which helps you achieve batch aggregation.</div><br> |


<span id="exts-mrange"></span>
### EXTS.MRANGE


|Category |Description |
|---|---|
|Command syntax |`EXTS.MRANGE Pkey fromTimestamp toTimestamp [COUNT count] [AGGREGATION aggregationType timeBucket] [WITHLABELS] FILTER filter1 [filter2 ...]` |
|Time complexity |O(N), where N is the number of data chunks of the target Datapoint. |
|Command description |Query the detailed information of Skeys that meet the custom filtering criteria (filter) within a specified time period (including the specified time point) in the target Pkey, including the Skey name, contained labels, and Datapoint data. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `fromTimestamp`: Start time of query, in the format of Unix timestamp. Unit: milliseconds.<br><br>* `toTimestamp`: End time of query, in the format of Unix timestamp. Unit: milliseconds. The symbol `*` is allowed to represent the current system timestamp. If this value is equal to `fromTimestamp`, it means the query only includes Datapoint data at that specific time point.<br><br>* `COUNT count`: Specify the upper limit of the number of Datapoints that can be returned. The value must not exceed 100,000. If this parameter is not filled, it means that a maximum of 100,000 Datapoint data can be returned.<br><br>* `AGGREGATION`: Set the aggregation query conditions for Skey, including:<br><br>   * `aggregationType`: Aggregation type. For example, you can aggregate by maximum value (`MAX`), minimum value (`MIN`), average value (`AVG`) and so on.<br><br>   * `timeBucket`: Sampling interval. Unit: milliseconds. The minimum sampling interval is 1,000 milliseconds.<br><br>      Cache for Redis will aggregate the data within the sampling interval according to the specified type and return the result. The returned time point is the start time of the sampling interval. For example, `AGGREGATION MAX 3000` means that the maximum value within every 3,000 milliseconds will be returned. For more details, refer to [Aggregation query syntax](https://docs.byteplus.com/en/docs/redis/exts#.6IGa5ZCI5p-l6K-i6K-t5rOV).<br><br>* `WITHLABELS`: Set whether the label information is included in the return result. If this parameter is not filled, it means that the label information is not displayed by default.<br><br>* `Filter`: Filter condition. Cache for Redis supports the use of multiple commands and command combinations in custom filter conditions (filter), but must include at least one of the `EQ`, `CONTAINS`, `LIST_MATCH` logics. For more details about `filter`, refer to [Conditional query syntax](https://docs.byteplus.com/en/docs/redis/exts#.5p2h5Lu25p-l6K-i6K-t5rOV). |
|Response |* Execution succeeded: Return the list of Skey information that meets the query criteria.<br><br>* Other cases reply corresponding exception information. |
|Example |* Command example 1<br><br>   Query Pkey `test_exts` for the sum every 3,000 milliseconds within a specified time range, including a list of Skeys where the label `stockid` is `B`, and each Skey is allowed to return a maximum of 2 Datapoint data.<br><br>   ```Bash```<br>```   EXTS.MRANGE test_exts 1743566159000 * COUNT 2 AGGREGATION SUM 3000 FILTER stockid=B```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   1) 1) "closing_price"```<br>```      2) (empty array)```<br>```      3) 1) 1) (integer) 1744254909000```<br>```            2) "107"```<br>```      4) (integer) 0```<br>```   2) 1) "closing_price2"```<br>```      2) (empty array)```<br>```      3) 1) 1) (integer) 1744255152000```<br>```            2) "73"```<br>```         2) 1) (integer) 1744255167000```<br>```            2) "76"```<br>```      4) (integer) 1```<br>```   3) 1) "volume"```<br>```      2) (empty array)```<br>```      3) 1) 1) (integer) 1744254906000```<br>```            2) "107"```<br>```      4) (integer) 0```<br>```   ```<br>   <br><br>* Command example 2<br><br>   Query Pkey `test_exts` for the count of values every 5,000 milliseconds within a specified time range. The query must include a list of Skey information where the label `stockid` is `B` and the label `issuer` is not `1`. The label information must also be displayed in the response.<br><br>   ```Bash```<br>```   EXTS.MRANGE test_exts 1743566159000 * AGGREGATION COUNT 5000 WITHLABELS FILTER stockid=B issuer!=1```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   1) 1) "volume"```<br>```      2) 1) 1) "stockid"```<br>```            2) "B"```<br>```         2) 1) "issuer"```<br>```            2) "2"```<br>```      3) 1) 1) (integer) 1744254900000```<br>```            2) "1"```<br>```      4) (integer) 0```<br>```   ```<br>   <br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The last line of information in each Skey list of the return result can be used to determine whether all Datapoint data that meet the criteria have been displayed. Among them:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>0</code>: All data has been displayed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>1</code>: Some data that meets the criteria has not been displayed.</div><br><br><br>   <div data-tips="true" data-tips-type="tip">For more details about this field, refer to the response description in <a href="https://docs.byteplus.com/en/docs/redis/exts#exts-range">EXTS.RANGE</a>.   </div><br>    |


<span id="exts-prange"></span>
### EXTS.PRANGE


|Category |Description |
|---|---|
|Command syntax |`EXTS.PRANGE Pkey fromTimestamp toTimestamp pkeyAggregationType pkeyTimeBucket [COUNT count] [AGGREGATION aggregationType timeBucket] [WITHLABELS] FILTER filter1 [filter2 ...]` |
|Time complexity |O(N), where N is the number of data chunks of the target Datapoint. |
|Command description |Aggregate Datapoint data that meets the custom filtering criteria (filter) within a specified time period at the Pkey level in the target Pkey.<br><br>If you specify aggregations at both the Pkey and Skey levels simultaneously, the aggregation at the Skey level will be performed first (the usage method is the same as the [EXTS.MRANGE](https://docs.byteplus.com/en/docs/redis/exts#exts-mrange) command), and then a secondary aggregation will be performed on the result of the first aggregation at the Pkey level. |
|Option |* `Pkey`: The name of the Pkey, used to specify the ExTimeSeries as the object of the command call.<br><br>* `pkeyAggregationType`: Aggregation type for Pkey. For more details, refer to [Aggregation query syntax](https://docs.byteplus.com/en/docs/redis/exts#.6IGa5ZCI5p-l6K-i6K-t5rOV).<br><br>* `pkeyTimeBucket`: Sampling interval for Pkey. Unit: milliseconds. The minimum sampling interval is 1,000 milliseconds.<br><br>* `fromTimestamp`: Start time of query, in the format of Unix timestamp. Unit: milliseconds.<br><br>* `toTimestamp`: End time of query, in the format of Unix timestamp. Unit: milliseconds. The symbol `*` is allowed to represent the current system timestamp. If this value is equal to `fromTimestamp`, it means the query only includes Datapoint data at that specific time point.<br><br>* `COUNT count`: Specify the upper limit of the number of Datapoints that can be returned. The value must not exceed 100,000. If this parameter is not filled, it means that a maximum of 100,000 Datapoint data can be returned.<br><br>* `AGGREGATION`: Set the aggregation query conditions for Skey, including:<br><br>   * `aggregationType`: Aggregation type. For example, you can aggregate by maximum value (`MAX`), minimum value (`MIN`), average value (`AVG`) and so on.<br><br>   * `timeBucket`: Sampling interval. Unit: milliseconds. The minimum sampling interval is 1,000 milliseconds.<br><br>      Cache for Redis will aggregate the data within the sampling interval according to the specified type and return the result. The returned time point is the start time of the sampling interval. For example, `AGGREGATION MAX 3000` means that the maximum value within every 3,000 milliseconds will be returned. For more details, refer to [Aggregation query syntax](https://docs.byteplus.com/en/docs/redis/exts#.6IGa5ZCI5p-l6K-i6K-t5rOV).<br><br>* `WITHLABELS`: Set whether the label information is included in the return result. If this parameter is not filled, it means that the label information is not displayed by default.<br><br>* `Filter`: Filter condition. Cache for Redis supports the use of multiple commands and command combinations in custom filter conditions (filter), but must include at least one of the `EQ`, `CONTAINS`, `LIST_MATCH` logics. For more details about `filter`, refer to [Conditional query syntax](https://docs.byteplus.com/en/docs/redis/exts#.5p2h5Lu25p-l6K-i6K-t5rOV). |
|Response |* Execution succeeded: Return the aggregation result that meets the query criteria.<br><br>* Other cases reply corresponding exception information. |
|Example |In the Pkey `test_exts`, perform the following aggregation operations on the Datapoint data within the specified time period:<br><br><br>* The Datapoint data should come from Skeys that have the label `stockid` set to `B`, and each Skey is allowed to return a maximum of 2 Datapoint records.<br><br>* First, sum the filtered Datapoint data at the Skey level every 3,000 milliseconds.<br><br>* Then, sum the above\-aggregated data at the Pkey level every 5,000 milliseconds.<br><br><br>```Bash```<br>```EXTS.PRANGE test_exts 1743566159000 * SUM 5000 COUNT 2 AGGREGATION SUM 3000 FILTER stockid=B```<br><br><br>Response example.<br><br>```Bash```<br>```1) 1) 1) (integer) 1744254905000```<br>```      2) "214"```<br>```   2) 1) (integer) 1744255150000```<br>```      2) "73"```<br>```2) (integer) 1```<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details on parameter descriptions in the response, refer to the response description in <a href="https://docs.byteplus.com/en/docs/redis/exts#exts-range">EXTS.RANGE</a>.</div><br> |


<span id=".5p-l6K-i6K-t5rOV"></span>
## Query syntax

<span id=".5p2h5Lu25p-l6K-i6K-t5rOV"></span>
### Conditional query syntax

The ExTimeSeries of Cache for Redis supports using the labels of Skey as filtering conditions (filter) to quickly query the target Skey. The syntax of the filtering conditions (filter) supported by ExTimeSeries is shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Cache for Redis supports the use of all commands and command combinations in the following table in custom filtering conditions (filter), but must include at least one of the logics of <code>EQ</code>, <code>CONTAINS</code>, and <code>LIST_MATCH</code>.</div>


* <div data-tips="true" data-tips-type="tip">For the command syntax in the following table, the definitions are as follows:</div>


   * <div data-tips="true" data-tips-type="tip"><code>L</code>: Label name.</div>


   * <div data-tips="true" data-tips-type="tip"><code>V</code>: Label value.</div>




|Conditional logic |Filter command syntax |Syntax explanation |
|---|---|---|
|EQ(equals) |`L=V` |Filter out the Skey with the label value of V from label L. |
|CONTAINS |`L!=` |Filter out the Skeys with non\-NULL label values from label L, that is, all Skeys that contain label L. |
|LIST_TMATCH |`L=(V1,V2,...)` |Filter out the Skeys with label values of V1, V2, and so on, from label L. |
|NOEQ(equals) |`L!=V` |Filter out the Skey with a label value not equal to V from label L. |
|NOCONTAINS |`L=` |Filter Skeys with a tag value of NULL from tag L, i.e., all Skeys that do not contain tag L. |
|LIST_NOTMATCH |`L!=(V1,V2,...)` |Filter out the Skeys whose label values are not V1, V2, and so on, from label L。 |


<span id=".6IGa5ZCI5p-l6K-i6K-t5rOV"></span>
### Aggregation query syntax

The ExTimeSeries of Cache for Redis supports aggregation query operations for sampling intervals (timeBucket). The aggregation types supported by ExTimeSeries are shown in the following table.


|Aggregation syntax |Syntax explanation |
|---|---|
|`MAX` |Maximum value. |
|`MIN` |Minimum value. |
|`AVG` |Average value. |
|`SUM` |Sum. |
|`FIRST` |The first value. |
|`LAST` |The last value. |
|`RANGE` |Range (Maximum value ~ Minimum value). |
|`COUNT` |Value quantity. |
|`STD.P` |Population variance. |
|`STD.S` |Sample variance. |
|`VAR.P` |Population standard deviation. |
|`VAR.S` |Sample standard deviation. |
