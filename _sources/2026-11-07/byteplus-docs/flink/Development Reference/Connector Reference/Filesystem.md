---
title: "Filesystem"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Filesystem"
---

The Filesystem Connector provides read and write capabilities for common file systems, such as CloudFS, and supports use as both source tables and result tables. You can create a source stream to fetch data from a filesystem directory as input data for jobs; you can also write job output data to a specified directory in the filesystem.

<span id="7ffbc91f"></span>
## DDL Definition

<span id="b9094f25"></span>
### Used as a Data Source

```sql
CREATE TABLE filesystem_source (
    name String,
    score INT
 ) WITH (
     'connector' = 'filesystem',
     'path' = '<yourfilepath>'
 );
```


<span id="847c44ce"></span>
### Used as a Data Sink

```SQL
CREATE TABLE filesystem_sink (
    name String,
    score INT
 ) WITH (
     'connector' = 'filesystem',
     'path' = '<yourfilepath>',
     'sink.rolling-policy.file-size' = '1M',
     'sink.rolling-policy.rollover-interval' = '10 min',
     'format' = 'json' 
 );
```


<span id="710b16dd"></span>
## WITH Parameters


|**Parameter** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Yes |(none) |String |Specifies the connector to use, which is the Filesystem connector here. |
|path |Is |(none) |String |File path.<br><br>For example, when using object storage TOS, the path format is `tos://*bucket_name*/file_path/`. |
|sink.rolling\-policy.file\-size |No |128MB |MemorySize |Maximum file memory limit.<br><br>When the size of the current file being written reaches the threshold, the file will be closed, and a new file will be opened for writing.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When writing files, if you need to see the written files in the filesystem sooner, additional configurations are required. You can set the connector's <strong>sink.rolling\-policy.file\-size</strong>, <strong>sink.rolling\-policy.rollover\-interval</strong> parameters, and enable Checkpoint in Flink settings.</div><br><br><br><div data-tips="true" data-tips-type="warning">For detailed information about the Filesystem connector's rolling policy, please refer to the open\-source document <a href="https://nightlies.apache.org/flink/flink-docs-release-1.11/zh/dev/table/connectors/filesystem.html#rolling-policy">Filesystem\-Rolling Policy</a>.</div><br> |
|sink.rolling\-policy.rollover\-interval |No |30min |Duration |Maximum continuous file writing time.<br><br>When the current writing time exceeds the threshold, the file being written will be closed, and a new file will be opened for writing.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When writing files, if you need to see the written files in the filesystem as soon as possible, additional configurations must be added. You can set the connector's <strong>sink.rolling\-policy.file\-size</strong>, <strong>sink.rolling\-policy.rollover\-interval</strong> parameters, and enable Checkpoint in the Flink settings.</div><br><br><br><div data-tips="true" data-tips-type="warning">For detailed information about the Filesystem connector's rolling policy, please refer to the open\-source document <a href="https://nightlies.apache.org/flink/flink-docs-release-1.11/zh/dev/table/connectors/filesystem.html#rolling-policy">Filesystem\-Rolling Policy</a>.</div><br> |
|sink.rolling\-policy.check\-interval |No |1min |Duration |File check interval.<br><br>The FileSystem checks the write time of files at this interval to see if they meet the closure conditions and closes the files that do. |
|sink.partition\-commit.trigger |No |process\-time |String |Partition closure strategy. The values are as follows:<br><br><br>* process\-time: Close the partition after it has been created for a certain period of time, with the partition creation time being the physical time at creation.<br><br>* partition\-time: Close the partition after it has existed for a certain period of time, with the partition creation time derived from within the partition.<br><br>   partition\-time relies on watermark generation and requires coordination with watermark to support automatic partition discovery. When the watermark time exceeds the sum of `the time extracted from the partition` and `the delay parameter configuration time`, the partition is committed. |
|sink.partition\-commit.delay |No |0s |Duration |Partition shutdown delay.<br><br>The partition will be closed after being created for a certain period of time. |
|partition.time\-extractor.kind |No |default |String |Partition time extraction method.<br><br>This configuration only takes effect when **sink.partition\-commit.trigger** is set to **partition\-time**. If the user has a custom partition time extraction method, it should be set to **custom**. |
|partition.time\-extractor.class |No |(none) |String |Partition time extraction class. |
|partition.time\-extractor.timestamp\-pattern |No |(none) |String |Format for extracting partition timestamps. It needs to be in the format yyyy\-MM\-dd HH:mm:ss, and use the corresponding partition fields in the Hive table as placeholders. The default first field is supported as yyyy\-mm\-dd hh:mm:ss.<br><br><br>* If the timestamp should be extracted from a single partition field 'dt', it can be configured as '$dt'.<br><br>* If the timestamp should be extracted from multiple partition fields such as 'year', 'month', 'day', and 'hour', it can be configured as '$year\-$month\-$day $hour:00:00'.<br><br>* If the timestamp should be extracted from two partition fields such as 'dt' and 'hour', it can be configured as '$dt $hour:00:00'. |
|sink.partition\-commit.policy.kind |Yes |(none) |String |Policy for committing partitions. The values are as follows:<br><br><br>* Success\-file: A _success file will be generated in the corresponding directory when a partition is closed.<br><br>* Custom: User\-defined partition submission strategy. |
|sink.partition\-commit.policy.class |No |(none) |String |Partition commit class.<br><br>This class must implement PartitionCommitPolicy. |


<span id="525d5ff4"></span>
## Sample Code


* Result Table

   ```sql
   CREATE TABLE datagen_source (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar
     )
   WITH
     (
       'connector' = 'datagen',
       'rows-per-second' = '1',
       'fields.order_status.length' = '3',
       'fields.order_id.min' = '1',
       'fields.order_id.max' = '1000',
       'fields.order_product_id.min' = '1',
       'fields.order_product_id.max' = '100',
       'fields.order_customer_id.min' = '1',
       'fields.order_customer_id.max' = '1000'
     );
   
   
   CREATE TABLE file_sink (
       order_id bigint,
       order_product_id bigint,
       order_customer_id bigint,
       order_status varchar
     )
   WITH
     (
       'connector' = 'filesystem',
       'path' = 'tos://doc-test/test_write_tos/',
       'format' = 'json'
     );
   
   
   INSERT INTO file_sink
   SELECT * FROM datagen_source;
   ```
   

* Source Table

   ```SQL
   CREATE TABLE file_source(
     order_id bigint, 
     order_product_id bigint,
     order_customer_id bigint,
     order_status varchar
   ) WITH (
       'connector' = 'filesystem',
       'path' = 'tos://doc-test/test_write_tos/',
       'format' = 'json'
   );
   create table print_sink (
     order_id bigint, 
     order_product_id bigint,
     order_customer_id bigint,
     order_status varchar
     )
   with
     ('connector' = 'print');
   
   
   insert into print_sink
   SELECT * FROM file_source;
   ```
