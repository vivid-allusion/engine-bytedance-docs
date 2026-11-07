---
title: "Flink & Paimon FAQ"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Flink_Paimon_FAQ"
---

<span id="13be636c"></span>
## 1. Insufficient disk space

**Common Scenario**: Using Flink for Paimon batch processing tasks (such as Hive batch file conversion, etc.), local disks are used during Shuffle, but a single container's disk is insufficient for the data volume of Shuffle files.

**Log Error**: Caused by: java.io.IOException: No space left on device.


* **Reason**: Too many slots per single TM Pod, insufficient TM disk.

* **Solution**: Adjust the slots of the single TM's Pod to 1, recommended parallelism \>= number of Paimon Buckets (the main reason for more than Paimon Bucket number is to enhance the throughput from TOS);


<span id="2bd00251"></span>
## 2. Insufficient JVM heap memory

**Common Scenario**: Using Flink for Paimon's streaming and batch processing, memory shortages may occur due to large data volumes or insufficient resources. Streaming.

**Log Error**: Caused by: java.lang.OutOfMemoryError: Java heap space.


* **Reason**: Too many individual TM Pod Slots, insufficient TM memory.

* **Solution**: Adjust the slots of individual TM's Pod to 1 and recommend a parallelism \>= number of Paimon Buckets (primarily to enhance the throughput from TOS fetching).


**Error Log**: GC overhead limit exceeded.


* **Reason**: Too many individual TM Pod Slots, insufficient TM memory.

* **Solution**: Adjust the slots of individual TM's Pod to 1 and recommend a parallelism \>= number of Paimon buckets (primarily to enhance the throughput from TOS fetching).


<span id="82909887"></span>
## 3. High data volume in a single Paimon bucket, resulting in persistent OOM.

**Scenario Description**: Adjust Flink job concurrency to the number of Paimon Buckets, with each TM Slot set to 1. Observations through Flink UI show some tasks running, but issues like OOM still occur.


* **Reason**: For example, a few tables found with 900 million records, amounting to over 150GB; only 13 Paimon buckets available with excessive data volume per bucket.

* **Solution**: Stop writing into Flink tasks, adjust bucketing (ALTER TABLE xxx SET TBLPROPERTIES ('bucket' = 'xxx'), recommend keeping individual bucket data between 1.5G and 2G ideally. More detailed operational methods can be found on the official website [Rescale Bucket](https://paimon.apache.org/docs/0.8/maintenance/rescale-bucket/).


<span id="cad6c95a"></span>
## 4. External data table fields are misaligned.

**The log error**: Caused by: org.apache.calcite.sql.validate.SqlValidatorException: Unknown target column 'order_id'


* **Reason**: The fields in Flink SQL and some field names in external target tables (such as in LAS Catalog) are not aligned.

* **Solution**: Check if the fields in Flink SQL and the external target tables are aligned and then modify the Flink SQL accordingly.


<span id="8b620095"></span>
## The number of fields is different

**The log error**: Cause: Different number of columns.


* **Reason**: The number of fields in external Sources and Sinks differs.

* **Solution**: Check if the fields in the Source table and Sink table are completely aligned.


<span id="f51d8f06"></span>
## The data in Paimon buckets is unbalanced

Flink UI shows that the data volume handled by different tasks varies by more than several times (data is severely imbalanced), which might cause OOM.


* **Reason**: Unreasonable primary key settings in Paimon lead to unbalanced data partitioning.

* **Solution**: Carefully recheck if the Paimon primary key settings are reasonable. If found unreasonable and if the table has no data, delete the original table and recreate it with the new primary key; if there is data, rebuild the table, stop writing data to the original table, then use a Flink Batch task to import to the new table, and finally, switch the incremental write job to the new table.


<span id="6d0c57c2"></span>
## 7. Common Issues with LAS Metadata Integration

<span id="21d93894"></span>
### 7.1 SQL Validation Error

When validating SQL (by clicking the verify button or during automatic SQL checks at launch) and encountering an error like `Caused by: org.apache.thrift.transport.TTransportException`, it indicates that the current connection to the LAS interface is different. Please do not panic; the current version temporarily cannot access LAS metadata during the SQL validation stage.

```Plain
org.apache.flink.table.api.ValidationException: Unable to create catalog 'paimon_test1'.

Catalog options are:
'hive-conf-dir'='/opt/tiger/workdir'
'metastore'='hive'
'type'='paimon'
'uri'='thrift://lakeformation.las.cn-beijing.byteplus.com:48869'
'warehouse'='tos://flink-cwz-paimon/paimon_test1'
        at org.apache.flink.table.factories.FactoryUtil.createCatalog(FactoryUtil.java:511)
        ...
Caused by: java.lang.RuntimeException: Failed to determine if database default exists
        at org.apache.paimon.hive.HiveCatalog.databaseExistsImpl(HiveCatalog.java:223)
        ... 9 more
Caused by: org.apache.thrift.transport.TTransportException
        at org.apache.thrift.transport.TIOStreamTransport.read(TIOStreamTransport.java:132)
        ... 15 more
```


Solution: During the task launch process, choose More Settings \- Skip the pre\-launch deep check.

<span id="2e62c28c"></span>
### 7.2 Runtime Failure to Access LAS Interface

After executing and starting the task, if the task fails and the logs report an error similar to the following, this issue indicates that the LAS interface is inaccessible.

```Plain
Caused by: org.apache.hadoop.hive.metastore.api.MetaException: Could not connect to meta store using any of the URIs provided. Most recent failure: org.apache.thrift.transport.TTransportException
```


Possible Causes


1. Not having uploaded the hive\-site.xml file, or the file name is incorrect.

   1. Solution: Check whether hive\-site.xml has been successfully uploaded to the dependencies, and ensure the filename precisely matches the requirements.

2. The AK/SK for accessing LAS is incorrect, failing to authenticate user information properly.

   1. Solution: Check if the AccessKey and AccessKeySecret in hive\-site.xml are correct.

3. The user accessing LAS does not have IAM's LASFullAccess permission; please contact the administrator to grant this permission.

   1. Solution: Contact the main account administrator to check if LASFullAccess permission has been granted to the user.


<span id="3ce382e2"></span>
### 7.3 No permission to access LAS API

After executing [6. Deploy Tasks](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog#f313ebc1) and starting the task, if you find that the task fails and similar errors are reported in the logs, it indicates that the LAS interface has not been authorized successfully.

```Plain
Caused by: org.apache.hadoop.hive.metastore.api.MetaException: Access denied: [DeniedPrivilege(resource:Resource{resourceScope='SCHEMA', catalogName='paimon_test1', schemaName='test_db'}, action:DESCRIBE)] for user: 31035840
```


Solution: This issue arises because the specified account has not been granted the necessary permissions in the LAS Catalog. Please combine the action suggested in the error log about granting the necessary permissions to the account.

<span id="6f400f2a"></span>
### 7.4 The task fails to start, reporting that the LAS database does not exist.

After executing [6. Deploy Tasks](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog#f313ebc1) and starting the task, if it is found that the task fails, and these errors are discovered in the **event log,**  `org.apache.flink.table.catalog.exceptions.DatabaseNotExistException`

Solution: This occurs because during the Flink task submission stage, SQL is statically parsed and current connections are not made to LAS to access existing databases. Simply include the following statement in the SQL code:

```Plain
CREATE TABLE IF NOT EXISTS test_db;
```


After resubmitting the task, it should return to normal.

<span id="cb44e40a"></span>
### 7.5 The format of hive\-site.xml is incorrect

After executing [6. Deploy Tasks](https://docs.byteplus.com/docs/flink/Paimon_with_LAS_Catalog#f313ebc1) and starting the task, if it is found that the task fails, and the following error is found in the logs, `com.ctc.wstx.exc.WstxParsingException`:

```Plain
Caused by: java.lang.RuntimeException: com.ctc.wstx.exc.WstxParsingException: Illegal processing instruction target ("xml"); xml (case insensitive) is reserved by the specs.
 at [row,col {unknown-source}]: [2,5]
```


Solution: This is because the format of the hive\-site.xml dependent on the LAS metadata may be incorrect. It is necessary to check if the XML file meets [syntactic standards](https://www.w3.org/TR/xml/). Common XML format issues can be referred to:


1. The content at the beginning of the file must be `<?xml ...` and must not contain any invisible characters, spaces, empty lines, etc., before the angle bracket.

2. XML documents must contain valid tags; special characters like `<`, `>`, and `&` should be marked as plain text using CDATA syntax if they appear.


<span id="6b148e2d"></span>
### How should one delete a LAS database table?

To delete a table from LAS metadata, you must manually remove both the table information from the LAS metadata and the table's file path in the TOS directory. Deleting only the LAS metadata or only the data in the TOS directory will lead to data inconsistency. This will result in errors similar to the following, causing the task to fail:


1. Deleting just the TOS file path without removing the LAS metadata

2. Deleting only the LAS metadata but not the TOS file data


Solution: Identify which scenario it is; removing both the existing LAS metadata and TOS file data will ensure that database tables continue to be written correctly.

<span id="17b2f12a"></span>
### The table in LAS is a non\-partitioned table, but there are partitions on the TOS file system.

If we use a partitioned table, but find that the table information in LAS and TOS is different:


1. The LAS interface displays the table as a partitioned table.

2. The data table displayed on the TOS interface has already generated partitions.


Solution: Paimon does not automatically synchronize the table's partition info to the LAS metadata management. If you want to see the partition fields of a data table in LAS metadata management, you need to add the following WITH parameters in the create table statement:

```Plain
'metastore.partitioned-table' = 'true' -- Determine whether to synchronize partition information to the LAS metadata management
```


> It is important to note that since the partition fields cannot be added dynamically, after adding the parameters, the existing data table must be cleared (including the LAS metadata and TOS data files), and then recreated.


<span id="857e7f3a"></span>
## 8. How to use the HNS hierarchical buckets of TOS

**Problem description**: Hierarchical Namespace (HNS, or hierarchical buckets) is a new bucket type based on hierarchical metadata management introduced by the object storage TOS. In addition to providing hierarchical namespace capabilities, it balances the scalability of flat objects, offers transparent interchangeability between object semantics and file semantics, achieving true "multiple access protocols for a single dataset", and enhancing data usability efficiency.

Compared to flat buckets, it supports directory\-level mv and rename operations well, optimizes common read operations like List and directory Head, enhances data processing efficiency and performance, and meets the usage scenarios of big data, data lake, and AI effectively.

Moreover, the combination of Paimon + HNS can truly utilize the atomic semantics of HNS, avoiding the need to introduce locking mechanisms to resolve conflicts when tasks in Flink are submitted simultaneously.

**Method of use**: Consistent with most normal Paimon usage methods, you can use it normally by adding custom parameters in the task configuration parameters.

```YAML
flink.plugins.filesystem.tos.proton.enabled: true
```


**Notice**: The current function only supports the Flink\-1.16\-byted version at the moment.

<span id="a09ff550"></span>
## 9. Issues relating to Flink CDC synchronization to Paimon

<span id="14d80aca"></span>
### 9.1 JDBC Driver not found error

**Problem symptom**: If the task fails to start, the following exception information appears in the logs `Caused by: java.lang.ClassNotFoundException: com.mysql.cj.jdbc.Driver`.

**Solution**: This issue is due to compliance reasons, as Flink CDC does not have a built\-in MySQL Driver. Please refer to [Use JDBC or MySQL-CDC data sources](https://docs.byteplus.com/docs/flink/Use_JDBC_or_MySQL-CDC_data_sources) the documentation, download the official MySQL Driver (recommended version 8.0.27), and upload it to the Flink CDC task dependencies.

<span id="e3e6adf6"></span>
### 9.2 After a fresh start of the Flink CDC task, new data cannot be added

**Problem symptom**: After the Flink CDC task has been running for a while, various reasons may necessitate discarding the original state and starting synchronization from a completely new initial stage. If the original Paimon table is not deleted at this time, there will be issues with writing new data.

**Solution**: This is because there is a flaw in the downstream data of Flink CDC for Paimon, with commit.user remaining fixed, resulting in snapshots starting from version 0 during writing to Paimon. As it lags behind the current version of the Paimon table, it will always be unable to release. There are two solutions:


1. Upon a fresh startup, it is necessary to delete all Paimon files on TOS to ensure a full synchronization from the beginning.

2. Upon a fresh startup, it is necessary to change commit.user to a new value, such as `commit.user: v2`, to ensure the new commit user snapshot can be published properly.


<span id="6a278de4"></span>
### There are differences between 9.3 MySQL Datetime and Paimon Timestamp types.

**Symptom**: MySQL's datetime is a timezone\-free data type, and many users use this type to store local time. For example, the time in UTC+8 zone is `2025-01-09 10:00:00`. Since the timezone cannot be confirmed, Flink & Paimon default to using the UTC timestamp in the conversion process. Therefore, after writing into Paimon, checking the time with UTC+8 shows the result as `2025-01-09 18:00:00`. This causes a discrepancy with the time in MySQL.

**Solution:** 


1. Avoid using datetime type fields in MySQL and opt for timestamp type fields with timezone information. This way, Flink can perform timezone conversion based on server\-time\-zone information.

2. If MySQL must use datetime type, store the time in UTC format in MySQL datetime fields, such as `2025-01-09 10:00:00` UTC+8, stored in the database as `2025-01-09 02:00:00`


<span id="a7c380e8"></span>
### 9.4 CDC task fails to start, indicating that dynamic bucket mode is not supported.

**The issue**: Flink CDC fails to start with a key error message: `Can't extract bucket from row in dynamic bucket mode` as shown below:

**The solution**: The current version of Flink CDC does not support Paimon's dynamic bucketing mode (bucket = \-1). Therefore, it is necessary to specify the following fixed bucketing parameters in Paimon Sink.

```YAML
# Specify the number of buckets when creating the table; it is recommended to set this reasonably based on the data volume
table.properties.bucket: 10
```


<span id="cf319f6e"></span>
### 9.5 How should changelog\-producer be selected

**Problem Description**: Paimon supports changelog\-producer options, generally recommending which option in CDC scenarios.

**The solution**: Paimon's changelog\-producer feature supports downstream Flink tasks reading complete change logs, which can be set with the following parameters:

```YAML
table.properties.changelog-producer: input
```


This option can be configured by referring to [Changelog output mechanism](https://docs.byteplus.com/docs/flink/Connector_Paimon#79d03b88) it in CDC scenarios where two common configurations exist:


1. `None`: If not needed downstream, set it to none, or leave it unset.

2. `Input`: If changelog is required downstream, as the upstream CDC is itself a changelog, simply choose input.
