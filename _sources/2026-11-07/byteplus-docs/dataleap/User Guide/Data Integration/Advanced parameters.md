---
title: "Advanced parameters"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/advanced_parameters"
---

This article introduces data integration tasks and the advanced parameter configurations used in different scenarios, as well as explanations related to these configurations.

<span id="6cac38ef"></span>
## Usage prerequisites

[Batch data synchronization](https://docs.byteplus.com/docs/dataleap/batch_data_synchronization),[Streaming data synchronization](https://docs.byteplus.com/docs/dataleap/streaming_data_synchronization), [solution tasks](https://docs.byteplus.com/en/docs/dataleap/data_synchronization_solutions), and other task types have been created as needed.

<span id="_2-资源使用相关参数"></span>
## Advanced parameter configuration steps

<span id="_4-1-离线集成任务配置说明"></span>
### Configuration instructions for offline integration tasks

Parameters for offline task execution, data source parameters, and resource usage parameters are all configured in the area marked by the red box in the diagram below.


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Select the project to which the task belongs, enter the data development interface, and open the task that requires advanced parameter configuration.

3. In 【**Task Run Parameters \> Custom Parameter Settings**】, add the relevant advanced parameters and add an example:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d095171978b4ce2a5c6f06635708133~tplv-goo7wpa0wc-image.image) </span>


<span id="f3a9e8a7"></span>
### Configuration instructions for streaming integration tasks


1. The way parameters related to data sources, task execution, and so on are configured is consistent with the method used in offline integration tasks.

2. The resource parameters for streaming integration tasks can be visually configured directly in the area highlighted by the red box in the diagram below:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97704a44a2ca4abcb494a3731354c7ea~tplv-goo7wpa0wc-image.image) </span>

3. Other advanced parameters for streaming integration tasks can be added in 【**Task Run Parameters \> Advanced Parameters**】.

   Example of adding:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16d742389ce1491eac0e23e24ce8b243~tplv-goo7wpa0wc-image.image) </span>


<span id="6c70442b"></span>
### Solution parameter configuration instructions

You can configure advanced parameter settings for the DataSail solution in the advanced configuration section of the solution's resource group.


1. Log in to the [DataLeap Tenant Console](https://console.byteplus.com/dataleap/console/region:dataleap-console+ap-southeast-1/project/list?administrator=mine&current=1&isMine=true&pageSize=20&projectName=&projectOrOwnerName=&sortColumn=createTime&sortOrder=desc).

2. Select the project to which the task belongs, enter the data development interface, and access the Data synchronization solution configuration interface at the top.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c847f2b11c2148238b4dc5b60d425c70~tplv-goo7wpa0wc-image.image) </span>

3. Enter the solution's creation or editing interface. In the solution interface, you can configure advanced parameters through the following two entry points:

   * Entry 1: In **Basic Configuration \> Resource Group Advanced Config**, add the corresponding offline and real\-time advanced parameter settings.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51b72066337a4bdea87701b7893e3bd2~tplv-goo7wpa0wc-image.image) </span>

   * Entry point 2: In **Mapping config \> Advanced params**, add the corresponding advanced parameter settings.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/670c1b0fafdd458993dbfa04d082f74a~tplv-goo7wpa0wc-image.image) </span>


<span id="f1aaaf18"></span>
## General parameters

<span id="629b1415"></span>
### Offline task runtime parameters


|Parameter name |Description of parameters |The default value |
|---|---|---|
|job.common.dirty_record_skip_enabled |Whether to skip dirty data. |true |
|* job.common.reader_transport_channel_speed_record<br><br>* job.common.writer_transport_channel_speed_record |Read/write rate limiting parameter. This sets a limit on the number of read and write operations per second. The default value is \-1, which means no limit is applied. When the value is set greater than 0, the rate limit is enabled. |\-1 |
|* job.common.reader_transport_channel_speed_byte<br><br>* job.common.writer_transport_channel_speed_byte |The read/write speed limit parameter specifies the maximum number of bytes that can be read or written per second. The default value is \-1, which means there is no limit. When the parameter is set to a value greater than 0, the speed limit is enabled. |\-1 |
|* job.reader.reader_parallelism_num<br><br>* job.writer.writer_parallelism_num |The read concurrency and write concurrency of the connector are only applicable to **offline tasks**.<br><br>Configuration is not recommended, as improper configuration may result in waste of resources or slow down execution. |There is no default value; the system automatically determines the concurrency level based on the data volume. |
|job.writer.case_insensitive |Case\-insensitive.<br><br>When reading from or writing to data sources such as TOS, OSS, ES, and Kafka, if you encounter case conversion issues, it is recommended to configure to be case\-sensitive by setting job.writer.case_insensitive=false. |true |
|job.writer.pre_sql_list |SQL list for preprocessing before writing to the data source. The format is a JSON array, for example:<br><br>job.writer.pre_sql_list=["delete from xx where id=xxx","delete from xx where id=xxx"] |Empty |


<span id="8c76b974"></span>
### Streaming task runtime parameters


|Parameter name |Parameter descriptions |Default value |
|---|---|---|
|job.common.global_parallelism_num |The global concurrency of the connector applies only to **streaming tasks**.<br><br>This parameter determines how many TaskManagers are started.<br><br><br>* If the traffic in MQ is low, you can control the global concurrency of the job by specifying this parameter in the task's advanced parameters.<br><br>* If the number of partitions in MQ is large but the data throughput is not high, you can also use this parameter to reduce the execution resources required for the task. |Number of MQ partitions / 4 |
|job.common.checkpoint_interval |By default, a Checkpoint is performed every 900,000 milliseconds (15 minutes). This applies only to **streaming jobs**. |900000 |
|job.common.checkpoint_timeout |The checkpoint timeout, in milliseconds, applies only to **streaming jobs**. |600000 |


<span id="52816a1a"></span>
### Solution\-related parameters


* **Parameters for offline full synchronization in the real\-time entire database**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To configure advanced parameters for offline full synchronization of additional data sources, see <a href="https://docs.byteplus.com/docs/dataleap/advanced_parameters#629b1415">Offline task runtime parameters</a> and <a href="https://docs.byteplus.com/docs/dataleap/advanced_parameters#1944c6db">Data source parameters</a>.   </div>
   

   
   |Parameter name |Parameter descriptions |Default value |
   |---|---|---|
   |job.common.is_use_batch_mode |Enable batch mode:<br><br><br>* true: In Flink batch mode, when resources are limited, some taskmanagers can also run tasks.<br><br>* false: In Flink task pipeline mode (suitable for large data volumes), reading and writing are performed simultaneously. |true |
   |job.reader.enable_string_compatible |In the **PostgreSQL2Hudi real\-time sharding and table synchronization** solution, if there are PostgreSQL data types at the source that cannot currently be recognized, you can add this parameter based on your actual business requirements to determine whether to convert them to string type.<br><br><br>* false: No conversion will be performed, and an error will occur during job execution.<br><br>* true: When converted to string type, the job runs normally.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is only applicable to the <strong>PostgreSQL2Hudi real\-time database and table sharding</strong> synchronization solution.</div><br> |false |
   

* **Parameters for real\-time incremental synchronization of the entire database**

   
   |Parameter name |Parameters |Default value |
   |---|---|---|
   |job.common.checkpoint_interval |Set the Checkpoint refresh time. |900000 |
   |job.reader.poll_interval_ms |Set the refresh interval for reading the binlog. The default is 500 milliseconds.<br><br>Configuration scenario: Reduce this parameter to improve real\-time performance. |500 |
   |job.reader.debezium |* Ignore special DDL statements that cannot be parsed:<br><br>   "database.history.skip.unparseable.ddl": "true"<br><br>* Configuration for ignoring SQL operations in the binlog:<br><br>   "skipped.operations":"d"<br><br>   Possible values are: d, c, and u<br><br>   * `c` for inserts/create,<br><br>   * `u` for updates,<br><br>   * `d` for deletes,<br><br>   * `t` for truncates,<br><br>   * `none` to not skip any operations.<br><br><br>By default, truncate operations are skipped.<br><br>Configuration example: {"database.history.skip.unparseable.ddl":"true","skipped.operations":"d,u"}<br><br>For more information, refer to the official website: [https://debezium.io/documentation/reference/stable/connectors/mysql.html#mysql-property-skipped-operations](https://debezium.io/documentation/reference/stable/connectors/mysql.html#mysql-property-skipped-operations) |\- |
   |solution.writer.common.ddl.bytehouse.enable.binlog |If you want the table to support Binlog reading in the future when automatically creating ByteHouse CDW tables using the real\-time full\-database synchronization solution, you need to manually add the advanced parameter `solution.writer.common.ddl.bytehouse.enable.binlog=true`. Only tables created in this way will be able to support Binlog reading in the future. |\- |
   

* **Flink runtime parameters:** 

   
   |Parameter name |Parameter descriptions |Default value |
   |---|---|---|
   |taskmanager.memory.managed.size |The proportion of each Task Manager's managed memory to the total memory size<br><br>Recommended configuration: 200m (seldom used for real\-time tasks) |\- |
   |taskmanager.memory.network.fraction |The proportion of network memory for each Task Manager.<br><br>Recommended configuration: 0.05 (rarely used for real\-time tasks) |\- |
   


<span id="586b0951"></span>
### Resource usage parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Resource usage parameters are only applicable to offline integration tasks.</div>


<div data-tips="true" data-tips-type="tip">The resource parameters for streaming integration tasks can be simply selected and configured directly on the page according to the instructions in the section above <a href="https://docs.byteplus.com/docs/dataleap/advanced_parameters#f3a9e8a7">Configuration instructions for streaming integration tasks</a>.</div>



|Parameter name |Parameter description |Default value |
|---|---|---|
|job.common.flink_tm_vcores |The number of CPU cores used by each Task Manager.<br><br><br>* Value constraints: **Must be greater than or equal to 0.5 and must be a multiple of 0.5**. |1.0 |
|job.common.slots_per_tm |The default number of slots per Task Manager. |2 |
|job.common.flink_tm_slot_memory |The memory size of each slot in each Task Manager, measured in MB.<br><br><br>* Value description: The ratio of CPU to memory (GB) for each Task Manager must be either 1:2 or 1:4; that is, flink_tm_vcores : (flink_tm_slot_memory [GB] \* slots_per_tm) = 1:2 or 1:4.<br><br>* For example, if flink_tm_vcores is set to 4.0 and slots_per_tm is set to 2, then flink_tm_slot_memory must be either 4 GB or 8 GB, that is, set to 4096 or 8192. |2048 |
|job.common.flink_tm_task_off_heap_memory |The proportion of off\-heap memory to total memory for each Task Manager |0.125 |
|job.common.flink_tm_managed_memory_ratio |The proportion of managed memory to total memory for each Task Manager. |0.2 |
|job.common.flink_tm_network_max |The maximum network memory for each Task Manager, in GB.<br><br><br>* Value description: Use the lowercase letter 'g' when configuring, for example: 2g. |2g |
|job.common.flink_jm_vcores |Number of CPU cores for Flink Job Manager.<br><br><br>* Value description: **The value must not be less than 0.5 and must be a multiple of 0.5**. |1.0 |
|job.common.flink_jm_memory |Total memory size of Flink Job Manager, in MB.<br><br><br>* Description: The ratio of CPU to memory (GB) for the Job Manager must be either 1:2 or 1:4, that is, flink_jm_vcores : flink_jm_memory [GB] = 1:2 or 1:4.<br><br>* For example, if flink_jm_vcores is set to 2.0, then flink_jm_memory must be either 4 GB or 8 GB, that is, it must be configured as 4096 or 8192. |4096 |
|job.common.flink_jm_off_heap_memory |The proportion of off\-heap memory to total memory for Flink Job Manager |0.125 |


<span id="1944c6db"></span>
## Data source parameters

<span id="9e1cabcf"></span>
### ByteHouse CDW/CE

<span id="7e03264b"></span>
#### **ByteHouse_CDW/CE batch read**

When reading from ByteHouse_CDW, the following advanced parameters are supported and can be configured as appropriate:


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.split_config |Set the configuration parameter for the number of task shards.<br><br>Configuration example: job.reader.split_config = {"split_num": 10}<br><br>Scope: For integer\-type split keys, such as when the split key is of type int, the default number of shards is equal to the number of concurrent tasks. You can use this parameter to modify the number of shards: job.reader.split_config = |The number of shards is the same as the concurrency level. |
|job.reader.string_split_size |Set the shard size.<br><br>Scope: For split keys of string type, you can calculate the number of shards based on this value.<br><br>This value should not be too large or too small:<br><br><br>* If it is too small, there will be too many shards, and calculating the shards will take a long time.<br><br>* Excessive size or too many individual shards triggers a data read timeout. |1000000 |
|job.reader.customized_connection_properties |Read ByteHouse timeout setting parameters.<br><br>Configuration example: Timeout setting: job.reader.customized_connection_properties = | |
|job.reader.output_null_value |When reading data of the Nullable(T) type in ByteHouse CDW, rows without a specific value are, by default, read and returned as `null`. If you need to return 0 instead, you can configure the `job.reader.output_null_value=false` parameter, in which case null values will be returned as 0. |true |


<span id="d1db18b2"></span>
#### **ByteHouse_CDW/CE batch writes**

When performing batch writes to ByteHouse_CDW/CE, the following advanced parameters are supported and can be configured as appropriate:


|Parameter name |Description |Default value |
|---|---|---|
|job.writer.flush_interval |Refresh interval for the write buffer, default is 60,000 milliseconds |60000 |
|job.writer.buffer_count |Number of records written to the buffer, default: 8192 |8192 |
|job.writer.query_timeout |Set the query timeout period; the default is 30,000 milliseconds. |30000 |
|job.writer.skip_delete_task |Writing to ByteHouse CDW is performed by means of an **import task**. By default, the import task is deleted after execution. With this parameter, you can specify whether to skip deleting the import task.<br><br>Applicable scenario: When you need to view import service logs in ByteHouse CDW, if the parameter is set to true, the deletion of import tasks will be skipped. |false |
|job.writer.cfs_write_batch_size |* Dynamic partition default is 4096.<br><br>* The default for non\-dynamic partitions is 8192.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This advanced parameter must be used in conjunction with the CFS write mode.</div><br> |4096/8192 |
|job.writer.cfs_vw_id |When using the CFS method to write data to ByteHouse Cloud Data Warehouse Edition, it is recommended to add this advanced parameter in the custom parameter settings to specify the compute group information used by the data import service. The format is as follows:<br><br>job.writer.cfs_vw_id = vw\-21xxxxx57\-dts\-test. You need to replace this with the specific compute group information. You can go to the [ByteHouse Console](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/n/default/database) to obtain the corresponding compute group. For details, see [ByteHouse CDW Virtual Warehouses](https://docs.byteplus.com/en/docs/bytehouse/docs-virtual-warehouses). |None |
|job.writer.bh_ce_partition_type |The displayed specified partition field for ByteHouse is of string type. When a function is applied to the partition field, you need to use this advanced parameter. |string |
|job.writer.loading_mode |The advanced parameter job.writer.loading_mode can be set to "FULL_REFRESH" or "INCREMENTAL". The default is "INCREMENTAL":<br><br><br>* FULL_REFRESH: Supports clearing existing data from **non\-partitioned tables** before importing new data, which prevents data duplication.<br><br>* INCREMENTAL: When importing data into a **partitioned table**, the data in the corresponding partition is cleared before new data is imported. This does not apply to non\-partitioned tables.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This advanced parameter must be used in conjunction with the CFS write mode.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This advanced parameter is not applicable when writing to the ByteHouse CE data source.</div><br> |INCREMENTAL |
|job.writer.extraProperties |Adding this parameter enables atomic data import when importing data into ByteHouse CDW.<br><br>Configuration example:<br><br>job.writer.extraProperties = {"job_time":"${date}"} |None |
|job.writer.bh_connection_properties |A Map<String,String\> type.<br><br>In offline and real\-time solutions, when the target data source is ByteHouse CE or ByteHouse CDW, you can customize ByteHouse query parameters and set them in the properties of the JDBC connection.<br><br>The configuration example is as follows:<br><br>job.writer.bh_connection_properties=<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This advanced parameter must be used with the JDBC write mode.</div><br> |None |
|job.writer.session_properties |A Map<String,String\> type.<br><br>In offline and real\-time solutions, when the target data source is ByteHouse CE or ByteHouse CDW, you can set ByteHouse session parameters by executing a "set key=value" statement in the current session.<br><br>Configuration example as follows:<br><br>job.writer.session_properties= |None |
|job.writer.pre_sql_list |List of preprocessing SQL statements for writing to the ByteHouse CDW data source. The format is a JSON array, with multiple statements separated by commas. For example:<br><br>job.writer.pre_sql_list=["delete from table_name1 where id=xxx","delete from table_name2 where id=xxx"]<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This advanced parameter must be used in conjunction with the JDBC write method.</div><br> |None |


<span id="9ddcd8dd"></span>
### Elasticsearch

<span id="26cd30a8"></span>
#### Elasticsearch batch read


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.case_insensitive |Should field names be case sensitive when reading data?<br><br>When reading ES data sources, if any fields contain uppercase letters, it is recommended to configure the system to be case\-insensitive. that is, job.reader.case_insensitive=false |true |


<span id="1148ad64"></span>
### FTP/SFTP


* JSON data format parameters:

   
   |**Parameters** |**Description** |**Default value** |
   |---|---|---|
   |job.common.case_insensitive |Is JSON content parsing case sensitive for field keys? |true |
   |job.common.support_json_path |Does it support including `.` the field name. true indicates support; false indicates no support. |false |
   |job.common.json_serializer_features |Datasail uses [fastjson](https://github.com/alibaba/fastjson) to parse JSON content. Users can configure the JSON parsing features through this parameter; for more information, refer to [SerializerFeature - fastjson 1.2.83 javadoc](https://www.javadoc.io/doc/com.alibaba/fastjson/1.2.83/com/alibaba/fastjson/serializer/SerializerFeature.html). Separate multiple SerializerFeature items with commas. |None |
   |job.common.convert_error_column_as_null |Should fields that fail type conversion be set to null by default? |false |
   

* Parameters related to CSV and TXT data formats:

   
   |**Parameters** |**Description** |**Default value** |
   |---|---|---|
   |job.common.csv_escape |CSV escape characters |None |
   |job.common.csv_quote |The CSV quote character |None |
   |job.common.csv_with_null_string |Treat this field value in the CSV as null |None |
   

* Other parameters:

   
   |**Parameters** |**Description** |**Default value** |
   |---|---|---|
   |job.reader.skip_if_path_not_exists |Whether to skip the file if the file to be read from FTP/SFTP does not exist. By default, skipping does not occur; the task fails.<br><br>You can set this parameter to true as needed, in which case the file will be skipped and the task will still complete successfully. Set the format as follows: job.reader.skip_if_path_not_exists=true |false |
   


<span id="cbabc805"></span>
### HDFS

<span id="cd6afff6"></span>
#### General advanced parameters for HDFS


|**Parameters** |**Description** |**Default value** |
|---|---|---|
|job.common.case_insensitive |Is JSON content parsing case\-sensitive with respect to field keys? |true |
|job.common.support_json_path |Is it supported with `.`? field name. "true" indicates support; "false" indicates no support. |false |
|job.common.json_serializer_features |DataSail uses [fastjson](https://github.com/alibaba/fastjson) to parse JSON content. Users can configure the features for JSON parsing through this parameter. For more information, see [SerializerFeature - fastjson 1.2.83 javadoc](https://www.javadoc.io/doc/com.alibaba/fastjson/1.2.83/com/alibaba/fastjson/serializer/SerializerFeature.html). Separate multiple SerializerFeatures with commas. |None |
|job.common.convert_error_column_as_null |Whether to set fields that fail type conversion to null by default. |false |
|job.common.host_ips_mapping |When configuring an HDFS data source using a **connection string**, you need to configure the ip_mapping information in the advanced parameters to map the node domain names of the HDFS cluster to their IP addresses. For example:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18148be2d3794e1d98cea600e0a2127b~tplv-goo7wpa0wc-image.image) </span><br><br>```Shell```<br>```job.common.host_ips_mapping = {```<br>``` "master-1-1.emr-c7axxxxxxxxx9b.cn-beijing.emr-volces.com":"xxx.xx.x.xx",```<br>``` "master-1-3.emr-c7axxxxxxxxx9b.cn-beijing.emr-volces.com":"xxx.xx.x.xx",```<br>``` "core-1-1.emr-c7axxxxxxxxx9b":"xxx.xx.x.xx",```<br>``` "master-1-1.emr-c7axxxxxxxxx9b":"xxx.xx.x.xx",```<br>``` "core-1-1.emr-c7axxxxxxxxx9b.cn-beijing.emr-volces.com":"xxx.xx.x.xx",```<br>``` "core-1-2.emr-c7axxxxxxxxx9b":"xxx.xx.x.xx",```<br>``` "master-1-2.emr-c7axxxxxxxxx9b.cn-beijing.emr-volces.com":"xxx.xx.x.xx",```<br>``` "master-1-3.emr-c7axxxxxxxxx9b":"xxx.xx.x.xx",```<br>``` "core-1-2.emr-c7axxxxxxxxx9b.cn-beijing.emr-volces.com":"xxx.xx.x.xx",```<br>``` "master-1-2.emr-c7axxxxxxxxx9b":"172.16.1.68"```<br>``` }```<br> |None |


<span id="db79e782"></span>
#### HDFS Batch reads


|Parameters |Description |Default value |
|---|---|---|
|job.reader.parse_partition_from_path |In scenarios where you need to read and parse partition fields from the data source path, you can add this advanced parameter. After manually adding the partition field mapping, you will be able to read partition field data as expected.<br><br>The format is: job.reader.parse_partition_from_path=true |false |
|job.reader.partition_num |When reading partition field data, if you are reading data formats such as JSON that do not have a schema definition, you must add this advanced parameter to specify how many partition fields are included in the path configured for the current job.<br><br>The format is: job.reader.partition_num=n, where n is the number of partition fields. |None |


<span id="a3fa08aa"></span>
#### Real\-time write to HDFS


|**Parameters** |**Description** |**Default values** |
|---|---|---|
|job.writer.rolling.max_part_size |File split size (in bytes); default is 10 GB.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This refers to the size of the data read before compression, not the final file size in HDFS.</div><br> |10737418240 |
|job.writer.hdfs.replication |HDFS replication factor |3 |
|job.writer.hdfs.compression_codec |Supported HDFS compression formats<br><br><br>* snappy<br><br>* lz4<br><br>* zstd<br><br>* fourmc<br><br>* fourmz<br><br>* gzip<br><br>* None (no compression) |zstd |
|job.writer.dump.directory_frequency |Write frequency for HDFS folders; the following parameters are supported:<br><br><br>* Daily level: dump.directory_frequency.day<br><br>* Hourly level: dump.directory_frequency.hour |dump.directory_frequency.day |


<span id="6d9fc03c"></span>
### HIVE

<span id="a86ef7bb"></span>
#### Generaladvanced parameters for HIVE


|Parameter name |Parameter description |Default value |
|---|---|---|
|job.common.checkpoint_interval |Set the Checkpoint refresh interval. The default is 15 minutes. When writing to Hive in real time, the timing of the write operation is determined by this parameter. |900000 |
|job.common.host_ips_mapping |When connecting a Hive data source to a self\-built cluster using a connection string, you must configure the mapping between the host and the actual IP address using this advanced parameter. For example:<br><br>```JSON```<br>```{```<br>```  "core-1-1.emr-1": "1xx.xx.0.11",```<br>```  "core-1-2.emr-2": "1xx.xx.0.12",```<br>```  "master-1-1.emr-1": "1xx.xx.0.13"```<br>```}```<br> |None |


<span id="46f1f042"></span>
#### Hive batch writes


|Parameter name |Parameter descriptions |Default value |
|---|---|---|
|job.writer.partition_strategy |Parameter partitioning strategy<br><br>Parameter values: "partition_first", "partition_last"<br><br>Applicable scenario: When a streaming job is configured to write data with the partition_first setting, you can view the current Hive partition data in real time. |partition_last |
|job.writer.partition.date_format |Write using a dynamic date partition format, which can be configured as: yyyyMMdd or yyyy\-MM\-DD |yyyyMMdd |
|job.writer.partition.hour_format |Write using the dynamic hourly partition format, which can be configured as: "hh" or "HH" |HH |
|job.writer.null_string_as_null |By default, the string type in complex types writes null as an empty string. If you need to configure the default behavior to write null values, you can set this parameter to true. If there are columns in dirty data that cannot be converted, they will be automatically converted to null values. |false |
|job.writer.case_insensitive |By default, all data will be converted to lowercase. |true |
|job.writer.convert_error_column_as_null |Automatically convert columns in dirty data that cannot be converted to the required type to null. |false |
|job.writer.dump.directory_frequency |Frequency of writing to HDFS folders; the following parameters are supported:<br><br><br>* Daily: dump.directory_frequency.day<br><br>* Hourly: dump.directory_frequency.hour |dump.directory_frequency.day |


<span id="d2299c68"></span>
### Kafka

<span id="1eaa5990"></span>
#### Kafka streaming read


|Parameter name |Description |Default values |
|---|---|---|
|job.reader.connector.startup\-mode |Default consumption starting position parameters:<br><br><br>* "earliest\-offset" (the oldest): Setting job.reader.connector.startup\-mode=earliest\-offset specifies that consumption starts from the earliest available position.<br><br>* "latest\-offset" (latest): job.reader.connector.startup\-mode=latest\-offset, starts consuming from the latest offset.<br><br>* specific\-offsets: Specifies the starting position for consumption by partition offset. For example, job.reader.connector.connector.specific\-offsets = [{"partition":0,"offset":1},{"partition":1,"offset":2}...]<br><br>* "specific\-timestamp": Specifies the starting position for consumption using a timestamp. Set job.reader.connector.connector.specific\-timestamp = 1716292387000 (a timestamp representing a specific point in time, in milliseconds). | |
|job.reader.metadata_columns |Read Kafka metadata\-related information. Multiple metadata items can be separated by English commas. Configuration example: job.reader.metadata_columns = **timestamp**,**offset**,**key**,**value**,**partition**,**headers** | |


<span id="29fbaefa"></span>
#### Offline write to Kafka


|Parameter name |Description |Default value |
|---|---|---|
|job.common.host_ips_mapping |Kafka is accessed over the public network, and the Kafka broker address is specified as a domain name. You need to configure a mapping between the IP address and the domain name. An example is as follows:<br><br>{<br><br>"ukxxxxxxxx\-kafka1":"xxx.xx.xxx.xx",<br><br>"ukxxxxxxxx\-kafka2":"xxx.xx.xxx.xx",<br><br>"uxxxxxxxxx\-kafka3":"xxx.xx.xxx.xx",<br><br>} | |
|job.common.skip_dump_parse |To connect a Kafka data source over the public network, you must set this parameter to **true.**  when SASL_SSL authentication is enabled. |false |
|job.writer.properties |max.request.size: Message body size;<br><br>buffer.memory: Buffer size.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Scope of application: In the configuration of the DataSail full\-database solution, if a single message body is relatively large, you can adjust this parameter.</div><br> |{"max.request.size":1048576,"buffer.memory":*33554432*} |
|job.writer.compression_type |Message compression formats supported: none, snappy, gzip, and lz4<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In the configuration of the DataSail full\-database solution, you can specify the message compression format.</div><br> |snappy |


<span id="ae1e9dfc"></span>
### Mongo

<span id="c3dc4006"></span>
#### Read MongoDB solutions


|Parameter name |Description |Default value |
|---|---|---|
|solution.reader.ddl.external_schema_mode |Due to Mongo's flexible schema definition, the fields retrieved by Mongo Schema Fetcher are unordered and are not guaranteed to be consistent each time. This creates certain challenges for the automatic table creation capability in the **solution**.<br><br>Therefore, the platform provides this parameter, which is used to specify the fields to be fetched in Schema Fetcher and their order. Description of values is as follows:<br><br><br>* Replace：<br><br>   `solution.reader.ddl.external_schema_mode=Replace`<br><br>   You can use this value when there is a requirement for the order of fields or when you want to customize the source fields. At this point, all fields and field attributes returned by Mongo will be discarded. Therefore, you need to use the `solution.reader.ddl.external_schemas` parameter below in combination with your own definitions to specify the type of each field, as well as key fields such as isPrimaryKey, and provide the complete schema information.<br><br>* Merge：<br><br>   `solution.reader.ddl.external_schema_mode=Merge`<br><br>   When the order of the fields is not required and incremental fields are present in the scenario, this value can be used. In conjunction with the `solution.reader.ddl.external_schemas` parameter below, you can specify the insertion position of a new field in the schema by setting the field's position parameter. The possible values for the insertion order are as follows:<br><br>   * First: Place at the top of the Schema.<br><br>   * Last: Placed at the end of the Schema.<br><br>   * Before: You must specify a parameter. For example, Before(name) places it before the name field.<br><br>   * After: You must specify a parameter, such as After(name), which is placed after the name field. |MERGE |
|solution.reader.ddl.external_schemas |Custom Mongo Schema field information is as follows:<br><br><br>* solution.reader.ddl.external_schema_mode=Replace, full column replacement mode; the following is an example:<br><br>   ```JSON```<br>```   solution.reader.ddl.external_schemas={```<br>```           "dts_test_do_not_delete.mongo_sink": [{```<br>```                   "name": "_id",```<br>```                   "type": "objectid",```<br>```                   "isPrimaryKey": true```<br>```           }, {```<br>```                   "name": "address2",```<br>```                   "type": "string"```<br>```           }, {```<br>```                   "name": "price",```<br>```                   "type": "double"```<br>```           }]```<br>```   }```<br>```   ```<br>   <br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9fc1867def145329c6e26def9608a1b~tplv-goo7wpa0wc-image.image) </span><br><br>* solution.reader.ddl.external_schema_mode=Merge, merge mode. An example is as follows:<br><br>   ```JSON```<br>```   solution.reader.ddl.external_schemas={```<br>```           "*": [{```<br>```                   "name": "_id",```<br>```                   "type": "objectid",```<br>```                   "position": "first"```<br>```           }, {```<br>```                   "name": "address2",```<br>```                   "type": "string",```<br>```                   "isPrimaryKey": true,```<br>```                   "position": "before(_id)"```<br>```           }, {```<br>```                   "name": "price",```<br>```                   "type": "double",```<br>```                   "position": "last"```<br>```           }]```<br>```   }```<br>```   ```<br>   <br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/35135e81fdd94dc7827fe05146cb8db0~tplv-goo7wpa0wc-image.image) </span> |None |


<span id="105c440e"></span>
#### Majority read concern in MongoDB


|Parameter name |Description |Default value |
|---|---|---|
|reader_fetch_size |The number of doc documents read per batch. |100000 |
|filter |Specify the read filter condition in accordance with MongoDB syntax. For example, to read data where id = 1000, fill in as follows: |None |
|split_mode |Two sharding modes are supported:<br><br><br>1. paginating: The number of items in a single shard is *totalRecords / batchSize*<br><br>2. parallelism: If MongoDB supports the splitVector feature, use MongoDB's built\-in splitting functionality; otherwise, divide the data evenly by the number of documents divided by the parallelism value. The number of records per partition is: *totalRecords / parallelism*. paginating: Partition the data precisely by dividing the data volume by the fetch size.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>To disable sharding, set the concurrency level to 1.</strong></div><br> |parallelism |


<span id="21c006dc"></span>
#### MongoDB batch writes


|Parameter name |Description |Default value |
|---|---|---|
|max_connection_per_host |Maximum number of connections in the connection pool. |100 |
|connect_timeout_ms |Connection timeout period. |10000 |
|batch_size |Amount of data written to MongoDB per batch |100 |
|write_mode |Write method for advanced parameter settings:<br><br><br>* insert: Writes data directly without overwriting existing records. If a unique key conflict occurs, the task will fail.<br><br>* overwrite: When writing data, existing data is not cleared. If the unique key is the same, the new data overwrites the old data. If the unique key is different, the new data is inserted directly.<br><br>* insert_if_not_exists: When writing data, existing data is not cleared. If the unique key matches, the original data remains unchanged; if the unique key does not match, new data is inserted. |None |


<span id="d0898d3b"></span>
### MySQL

<span id="f4541b49"></span>
#### MySQL batch reads

Batch reading supports the following advanced parameters, which you can configure as needed:


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.init_sql |The SQL statement executed before reading data. Queries on views may require using an init SQL statement to initialize the environment. |None |
|job.reader.reader_fetch_size |The number of records fetched each time only applies when using accurate sharding. |10000 |
|job.reader.query_timeout_seconds |Read data using JDBC and set the read timeout in seconds. |300 |
|job.reader.shard_split_mode |JDBC connection sharding modes: precise sharding, concurrent sharding, and no sharding.<br><br><br>* Accurate sharding (default): Data is divided into different segments based on the configured sharding key. Except for the last segment, each segment contains exactly reader_fetch_size records. This mode is slower, but it ensures that the sizes of downstream files are generally consistent.<br><br>   * When retrieving large tables or when the sharding key is not a primary key or index key, the sharding time for this mode will be relatively long.<br><br>   * This sharding mode supports shard keys of integer and string data types.<br><br>   * Configuration method: Set this parameter to "accurate".<br><br>* Imprecise sharding mode: This mode is faster, but it cannot guarantee consistent downstream file sizes.<br><br>   * This sharding mode only supports shard keys of integer data type.<br><br>   * When the parameter is set to "parallelism", all data is divided into intervals, with the number of intervals determined by the degree of parallelism and the boundaries set by the table's maximum and minimum values.<br><br>   * When the parameter is set to quick, fuzzy partitioning is performed based on reader_fetch_size.<br><br>* No sharding: Sharding is not performed. This option is suitable for tables with a small amount of data, or for tables that do not have a primary key or index key.<br><br>   * Configuration method: Set this parameter to 'nosplit' or do not configure 'split_pk'. |Accurate partitioning |
|job.reader.customized_sql |Read SQL statements with custom queries. If the filter configuration option is not sufficient to describe the filtering conditions, you can use this option to define and execute more complex SQL queries.<br><br>For example: If you need to synchronize data after performing a multi\-table join, use select a, b from table_a join table_b on table_a.id = table_b.id.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After configuring this advanced parameter, you still need to configure required configuration items for the data synchronization task, such as table_name, columns, split_pk, shard_split_mode, and other required configuration items. However, during synchronization, the system ignores these configuration items and directly uses the settings specified in the advanced parameter item for data querying and filtering.</div><br> |None |


<span id="f49907ea"></span>
#### MySQL batch writing

Batch writing supports the following advanced parameters, which you can configure as needed:


|Parameter name |Description |Default value |
|---|---|---|
|job.writer.is_insert_ignore |In insert into mode, if a primary key or unique key conflict occurs, setting this parameter to false causes the task to fail, while setting it to true ignores the conflict and allows the task to continue executing normally. |false |
|job.writer.write_batch_interval |The number of data records submitted in each batch. This value can reduce the number of network interactions with MySQL and improve overall throughput. If this value is set too high, it may cause the data synchronization process to run out of memory (OOM). |100 |
|job.writer.write_retry_times |Number of retries for MySQL write failures. |3 |
|job.writer.retry_interval_seconds |The interval between two retry attempts after a write failure, measured in seconds. |write_batch_interval / 10 |
|job.writer.connection_parameters |All JDBC connection parameters can be appended after the default values:<br><br><br>* Use tcpRcvBuf when reading large amounts of data in a single line:<br><br>   tcpRcvBuf=1024000 （1MB）<br><br>* allowMultiQueries enables support for multiple SQL statements separated by semicolons: allowMultiQueries=true<br><br>* connectTimeout: Connection timeout duration, in milliseconds:<br><br>   connectTimeout=60000 |autoReconnect=true&useUnicode=true&characterEncoding=utf\-8&useSSL=false&zeroDateTimeBehavior=convertToNull |
|job.writer.table_pattern |Required parameters for writing data to multiple MySQL partitioned tables For details on precautions, see [5.3 Write data to multiple MySQL partitioned tables](https://docs.byteplus.com/docs/dataleap/69127#5aff6e49).<br><br>This parameter allows you to reference a field name from the source table as part of the target table name. For example, if the source table or source TOS file contains a field named table_name, then ${table_name} indicates that, at runtime, the value of this field in each data record will be automatically used to construct the target table name string.<br><br>Configuration example: job.writer.table_pattern=${table_name}_copy |None |
|job.writer.internal_columns |Optional parameters for writing data to multiple MySQL partitioned tables<br><br>This parameter allows you to specify that certain field data from the source table will not be written to the target table. For example, the table_name field that has already been selected as the target table name does not need to appear among the data fields actually written to the target table. You can set this parameter to: job.writer.internal_columns=[ "table_name" ] |None |


<span id="b97bd356"></span>
### StarRocks

<span id="55465a2f"></span>
#### Batch writing in StarRocks


|Parameter name |Parameter description |Default parameter values |
|---|---|---|
|job.writer.sink_flush_interval_ms |Write buffer flush interval, default: 60000 milliseconds |60000 |
|job.writer.sink_buffer_size |Write buffer size, default is 10485760 (10 MB) |10485760 |
|job.writer.sink_buffer_count |Number of records to write to the buffer (default: 8192) |8192 |
|job.writer.stream_load_properties |Data write method parameter specification<br><br>Example: Primary key conflict strategy<br><br><br>* Default: full row update<br><br>* {"partial_update":true} Partial update: only fields with column mappings are updated; supported only for tables with primary keys.<br><br>* {"insert_ignore":"ignore"} Ignores updates and ignores new data based on the primary key; only supported for tables with a primary key |Entire row update |
|job.writer.request_read_timeouts |Time to wait for a result after a write operation; the default is 60000 milliseconds.<br><br>Applicable scenario: When the data volume is large, write operations are slow, and timeouts may occur, it is recommended to increase this parameter. |60000 |
|job.writer.request_connect_timeouts |Set connection timeout (default: 60000 milliseconds) |60000 |
|job.writer.sink_enable_2PC |Tasks are committed in two phases during write operations; the default is false.<br><br>true: Applicable scenarios include streaming integration writing, two\-phase commit, and guaranteeing exactly\-once semantics for data. |false |


<span id="b5fc1f47"></span>
### Paimon

<span id="77555705"></span>
#### Paimon batch read


|**Advanced parameter key** |**Advanced parameter value** |
|---|---|
|job.reader.properties |Dynamically set the properties of a Paimon table at runtime (see [https://paimon.apache.org/docs/0.8/maintenance/configurations/](https://paimon.apache.org/docs/0.8/maintenance/configurations/)) as a JSON string of type Map<String, String\>. |
|job.reader.limit |Limits the number of rows to be read, typically used for data sampling or testing |


<span id="ce45d7c4"></span>
#### Paimon batch writing


|**Advanced parameter key** |**Advanced parameter value** |
|---|---|
|job.writer.properties |Dynamically set the properties of a Paimon table at runtime (see [https://paimon.apache.org/docs/0.8/maintenance/configurations/](https://paimon.apache.org/docs/0.8/maintenance/configurations/)), as a JSON string representing a Map<String, String\>. |
|job.writer.overwrite_partition |Overwrite specific partitions; this takes effect if and only if the write mode is set to "overwrite". The format is a JSON string of type Map<String, String\>. |
|job.common.checkpoint_interval |The snapshot generation interval for Flink streaming jobs is specified in milliseconds. The default value is 300,000 ms (300 seconds or 5 minutes).<br><br>When streaming writes are performed to Paimon, data is committed only after each snapshot is completed. Therefore, a shorter snapshot interval allows new data to be discovered by downstream systems more quickly.<br><br>However, an excessively short snapshot interval will generate a large number of small files, which can severely impact performance and query efficiency. Please set this value appropriately. |


<span id="ac018787"></span>
#### Advanced parameters for automatic table creation in the Paimon solution

In the refresh target table mapping interface of the solution, we can enter some advanced parameters to control table creation behavior. For details, see [Target database table mapping configuration](https://docs.byteplus.com/docs/dataleap/full_load_cdc_synchronization#e50a0601).


|**Advanced parameter key** |**Advanced Parameter Value** |
|---|---|
|solution.writer.common.ddl.buckets_num |Number of buckets for the target table. If not set, the default is \-1 (dynamic bucket). |
|solution.writer.paimon.ddl.bucket_keys |The bucket key of the target table. If there are multiple fields, you can separate them with a comma (for example, id,name).<br><br>If not specified, the default bucket key is the same as the primary key. If the table does not have a primary key, all fields are used as the bucket key by default. |
|solution.writer.paimon.ddl.options |Various optional parameters when creating a table (see [https://paimon.apache.org/docs/0.8/maintenance/configurations/](https://paimon.apache.org/docs/0.8/maintenance/configurations/)), provided as a JSON string representing a Map<String, String\> |


<span id="00b20348"></span>
### PostgreSQL

<span id="858bb066"></span>
#### PostgreSQL batch reads


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.init_sql |SQL statements executed before reading data. Querying views may require using an init SQL statement to initialize the environment. |None |
|job.reader.reader_fetch_size |The number of records fetched each time only applies to accurate sharding. |10000 |
|job.reader.shard_split_mode |Sharding modes: accurate sharding, concurrent sharding, and no sharding<br><br><br>* Accurate sharding (default): Data is divided into different ranges based on the configured sharding key. Except for the last range, each range contains exactly reader_fetch_size records.<br><br>   * When pulling data from large tables, or when the sharding key is not a primary key or index, the sharding time in this mode will be relatively long.<br><br>   * This sharding mode supports shard keys of integer and string data types.<br><br>   * Configuration method: Set this parameter to accurate.<br><br>* Concurrent sharding: Based on the maximum and minimum values of the table, all data is partitioned into intervals according to the number of concurrent tasks.<br><br>   * This sharding mode only supports shard keys of integer data type.<br><br>   * Configuration method: Set this parameter to parallelism.<br><br>* No sharding: Sharding is not performed. This applies to tables without primary keys or index keys.<br><br>   * Configuration method: Set this parameter to "nosplit" or leave "split_pk" unconfigured. |Accurate sharding |
|job.reader.customized_sql |Read SQL statements for custom queries The filter configuration option is not sufficient to describe the filtering conditions. You can use this option to define and execute more complex SQL queries.<br><br>For example, if you need to synchronize data after performing a multi\-table join, use the following statement: select a, b from table_a join table_b on table_a.id = table_b.id.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After configuring this advanced parameter, the data synchronization task still requires configuration of mandatory items such as table_name, column, split_pk, shard_split_mode, and others. However, during synchronization, the system ignores the information of these configuration items and directly uses the content configured in the advanced parameter item to query and filter data.</div><br> |None |


<span id="88abc9dc"></span>
#### PostgreSQL batch writing


|Parameter name |Description |Default value |
|---|---|---|
|job.writer.is_insert_ignore |In insert into mode, does the task fail or ignore the conflict when a primary key or unique key conflict occurs? |false |
|job.writer.write_batch_interval |The number of records submitted in a single batch. This value can reduce the number of network interactions with PostgreSQL and improve overall throughput. If this value is set too high, it may cause the data synchronization process to run out of memory. |100 |
|job.writer.write_retry_times |Number of retry attempts for PostgreSQL write failures. |3 |
|job.writer.retry_interval_seconds |Time interval between two retry attempts after a write failure, in seconds |write_batch_interval / 10 |


<span id="ad3adf01"></span>
### Redis

<span id="9c3036f2"></span>
#### Offline reads in Redis


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.key_pattens |The matching strategy for reading Redis keys defaults to '\*', which means all keys are read.<br><br>Supports exact matching and fuzzy matching:<br><br><br>* Exact match: For example, to synchronize only the keys for user_a and user_b, simply enter user_a,user_b;<br><br>* Fuzzy matching: For example, to synchronize only keys with the prefix user_info, simply enter user_info\*. |\* |
|job.reader.db_index |The Redis logical database index number defaults to 0. If your data is stored in another Redis DB, for example, in DB 6, just enter 6. |0 |
|job.reader.reader_parallelism_num |Number of Redis shards to read. Because the Redis service uses a single\-threaded model, it is recommended to set this value to 1. The default is 1. |1 |
|job.reader.client_timeout_ms |The timeout for creating a Redis connection, measured in milliseconds (ms). |60000 |
|job.reader.max_attempt_count |Maximum number of retries for each failed Redis command execution |3 |
|job.reader.read_mode |Specify a Redis read mode:<br><br><br>* Scan mode: When reading a large number of keys, tasks may encounter exceptions such as "JedisConnectionException: Unexpected end of stream." In such cases, it is recommended to use scan mode when reading from Redis. This mode reads keys in batches, retrieving a portion of the data with each batch, which improves synchronization performance.<br><br>* All mode: By default, all key contents are pulled from Redis at once and then processed. |all |
|job.reader.scan_batch_size |Use together with the job.reader.read_mode parameter. When job.reader.read_mode is set to scan, you must use this parameter to specify the size of each fetch. By default, 10,000 keys are read each time. |10000 |


<span id="8d65043d"></span>
#### Redis offline write


|Parameter Name |Description |Default value |
|---|---|---|
|job.writer.write_batch_interval |The number of data entries submitted in each batch; this value can reduce the number of network interactions with Redis and improve overall throughput. However, if this value is set too high, it may cause the data synchronization process to run out of memory (OOM). |50 |
|job.writer.database |Specify the database in Redis to write to. The default is 0. |0 |


<span id="fec40460"></span>
### TOS

<span id="7d4b20db"></span>
#### TOS offline read


|Parameter name |Description |Default value |
|---|---|---|
|job.reader.enable_success_file_check |If the task requires checking whether the prerequisite Success file is ready, you can add this advanced parameter. When set to True, Success file checking is enabled; the task will only be considered successful if the specified file exists. Default: false. No check is performed. |false |
|job.reader.success_file_path |Set the full path information for the Success file used in the check. | |
|job.reader.success_file_check_interval_ms |Set the interval for checking the Success file, in milliseconds. The default is 60000. |60000 |
|job.reader.success_file_check_times |Set the number of times to check the Success file (default: 60) |60 |
|job.reader.csv_delimiter_ascii |When the delimiter in a TOS file is an invisible ASCII character, you can use this advanced parameter and set it to the ASCII value of the corresponding character. For example, `job.reader.csv_delimiter_ascii=1` indicates that the file delimiter is the invisible control character SOH.<br><br>This parameter takes precedence over the delimiter set in the interface. |None |
