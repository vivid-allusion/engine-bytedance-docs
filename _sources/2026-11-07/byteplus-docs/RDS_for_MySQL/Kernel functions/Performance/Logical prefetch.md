---
title: "Logical prefetch"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Logical_prefetch"
---

This topic describes the logical prefetch feature of RDS for MySQL.

<span id="8llmz4IE"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20260215 and above.

* MySQL 8.0 with a kernel version of MySQL 8.0.43_20251215 or later.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id="HU2fxEoh"></span>
## Background

MySQL natively supports linear prefetching. It predicts the pages that need to be read based on their physical location and asynchronously loads them into the buffer pool. This allows subsequent read requests from user threads to directly hit the buffer pool, reducing the I/O latency of user SQL queries. However, for instances that use volumes, adjacent data pages may not be contiguous in the actual storage. As a result, the native linear prefetching mechanism of MySQL provides suboptimal optimization.

RDS for MySQL introduces a logical prefetching feature. This feature accurately predicts the pages that need to be read based on user SQL queries to reduce the I/O latency of SQL queries for instances that use volumes.

<span id="fT0P6zhh"></span>
## Feature description

The logical pre\-read capability scans indexes through a background thread, accurately predicts the pages that user threads need to read based on the index, and asynchronously loads them into the buffer pool.

Logical pre\-read supports the following scenarios:


* Primary key range scan (Suitable for scenarios with a high volume of primary key index scans)

* Secondary index range scan (Suitable for scenarios with a high volume of secondary covering index scans)

* Covering index scan (Suitable for scenarios with a high volume of secondary covering index scans)

* Secondary index range scan with primary key lookup (Suitable for scenarios with a poor secondary index filtering rate)


To optimize the read performance of BLOB data, this iteration of MySQL 8.0 also implements the prefetching capability for BLOB objects.

<span id="mlyZKVKB"></span>
## Instructions

<span id="XkM7LafO"></span>
### Parameter description

RDS for MySQL provides the following modifiable parameters to configure the logical prefetch feature.


|**Parameter name** |**Supported version** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|loose_enable_logical_prefetch_page |MySQL 5.7，MySQL 8.0，MySQL 8.4<br><br> |OFF |No |[ON\|OFF] |GLOBAL/SESSION |Enables or disables the logical prefetch feature. Values:<br><br><br>* `ON`: enable.<br><br>* `OFF`: disable. |
|loose_logical_prefetch_rows_threshold<br><br> |MySQL 5.7，MySQL 8.0，MySQL 8.4<br><br> |OFF<br><br> |No<br><br> |[ON\|OFF] |GLOBAL/SESSION |The minimum number of scanned rows for executing a logical prefetch. Logical prefetch is executed only if the estimated number of scanned rows in the execution plan exceeds the value of this parameter. |
|loose_enable_blob_prefetch |MySQL 8.0，MySQL 8.4<br><br> |OFF |No |[ON\|OFF] |GLOBAL/SESSION |Enables or disables the blob prefetch feature. Values:<br><br><br>* `ON`: enable.<br><br>* `OFF`: disable. |
|loose_enable_track_index_io |MySQL 5.7，MySQL 8.0，MySQL 8.4<br><br> |OFF |No |[ON\|OFF] |GLOBAL/SESSION |Enables or disables the IO metric monitoring feature of `information_schema.rds_io_trace_stats`. |


<span id="e1ikxug5"></span>
### Examples

Before application, you can use Database Workshop to manually connect to the secondary instance and execute prefetch SQL to test the optimization effect. This avoids putting heavy pressure on the primary instance from large\-scale scans.

```SQL
SET SESSION loose_enable_logical_prefetch_page=ON;        # 当前连接开启逻辑预读功能
SET SESSION loose_logical_prefetch_rows_threshold=100000; # 设置预估扫描行数阈值为 100,000 行
SET SESSION loose_enable_track_index_io=ON;               # 用于观察预取 IO 统计信息，存在一定开销，请避免在生产环境全局开启

select sum(k) from test.sbtest1 where (k > 1 and k < 200000); # 测试 SQL
```


After enabling IO metric observation by running `SET SESSION loose_enable_track_index_io=ON`, you can execute `SELECT * FROM information_schema.rds_io_trace_stats WHERE thread_id = connection_Id()` to check whether the current thread performed a logical prefetch, the details of the logical prefetch, and the possible reason for not supporting it:


|**Metrics to observe** |**Description of indicators** |
|---|---|
|prepare_logical_prefetch.is_exceed_max_parallel |Whether the number of concurrent operations exceeds the current supported maximum value. |
|prepare_logical_prefetch.btr_root_level |Pre\-reading is not supported if the index tree has only one layer (small data volume). |
|finish_logical_prefetch.n_ctx_async_read_page_request |The quantity of asynchronous read requests that the logical prefetch tries to issue. |
|finish_logical_prefetch.n_ctx_async_read_page_success |The quantity of asynchronous read requests successfully issued by logical prefetch. |
|finish_logical_prefetch.ctx_execute |The overall elapsed time of the logical prefetch process can represent the overall latency of the query. |


<span id="fA7iGya4"></span>
### Precautions


* Enabling the logical prefetch feature increases IO/CPU resource consumption due to prefetch threads, which might impact other concurrent SQL operations. Therefore, enable this feature selectively only for the required SQL statements.

* Logical prefetch is not currently supported for compressed tables, partitioned tables, or non\-InnoDB tables.

* Logical prefetch is not currently supported for multi\-valued indexes, virtual generated column indexes, spatial indexes, full\-text indexes, or vector indexes.

* In MySQL 5.7, BLOB data can only be read sequentially, so prefetching for BLOB objects is not currently supported.


<span id="uLw80tmo"></span>
## Performance data


* Test Environment


An RDS for MySQL 8.0 instance with a 2C4G node specification and a 10 TB cloud disk.


* Test table data


Use `sysbench prepare` to insert data that is five times the number of rows in the test range.


* Test method and results


Restart the MySQL process before each test to ensure that the memory `buffer_pool` contains no cached data, which allows for testing the actual improvement in execution efficiency.


|**Scan range (unit: row)**  |**Prefetch (Second)**  |**Non\-prefetch (Unit: Second)**  |**Elapsed time comparison** |
|---|---|---|---|
|<div style="text-align: right"><br>100,000</div><br> |<div style="text-align: right"><br>0.44</div><br> |<div style="text-align: right"><br>0.62</div><br> |<div style="text-align: right"><br>\-29.04%</div><br> |
|<div style="text-align: right"><br>500,000</div><br> |<div style="text-align: right"><br>2.20</div><br> |<div style="text-align: right"><br>3.03</div><br> |<div style="text-align: right"><br>\-27.40%</div><br> |
|<div style="text-align: right"><br>2,000,000</div><br> |<div style="text-align: right"><br>9.05</div><br> |<div style="text-align: right"><br>13.48</div><br> |<div style="text-align: right"><br>\-32.87%</div><br> |
|<div style="text-align: right"><br>5,000,000</div><br> |<div style="text-align: right"><br>21.48</div><br> |<div style="text-align: right"><br>30.16</div><br> |<div style="text-align: right"><br>\-28.78%</div><br> |
|<div style="text-align: right"><br>10,000,000</div><br> |<div style="text-align: right"><br>43.14</div><br> |<div style="text-align: right"><br>62.17</div><br> |<div style="text-align: right"><br>\-30.61%</div><br> |
|<div style="text-align: right"><br>50,000,000</div><br> |<div style="text-align: right"><br>209.44</div><br> |<div style="text-align: right"><br>302.33</div><br> |<div style="text-align: right"><br>\-30.73%</div><br> |
|<div style="text-align: right"><br>100,000,000</div><br> |<div style="text-align: right"><br>424.69</div><br> |<div style="text-align: right"><br>737.57</div><br> |<div style="text-align: right"><br>\-42.42%</div><br> |
