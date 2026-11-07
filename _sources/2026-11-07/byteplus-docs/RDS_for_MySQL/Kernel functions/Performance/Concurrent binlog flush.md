---
title: "Concurrent binlog flush"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Concurrent_binlog_flush"
---

This topic describes the binlog concurrent flush optimization feature provided by RDS for MySQL.

<span id="jOKleCYq"></span>
## Supported version


* MySQL 8.0 version, and the kernel version is MySQL 8.0.43_20251215 and above.

* MySQL 8.4 version, and the kernel version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id="4lCBQKT3"></span>
## Background

When a transaction is committed in MySQL, binlog events are written from the temporary cache of the current session to the binlog file. Since this operation is performed serially, writing to the binlog file often becomes a performance bottleneck for the entire instance.

<span id="oAu5MUqf"></span>
## Feature description

RDS for MySQL optimizes the process of writing transaction binlog events from the temporary cache of the current session to the binlog file. This allows binlog events to be written concurrently, which significantly improves instance performance.

<span id="kF5lhIF8"></span>
## Instructions

<span id="WW39m45l"></span>
### Parameter description

The following parameters can be modified to configure the concurrent binlog flush optimization.


|**Parameter name** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range**<br><br> |**Scope** |**Description** |
|---|---|---|---|---|---|
|loose_binlog_parallel_flush |OFF |Yes |[ON\|OFF] |Global |Enables or disables the binlog concurrent flush optimization feature. Values:<br><br><br>* `ON`: enable.<br><br>* `OFF`: disable. |


<span id="NnSDrOyX"></span>
### Precautions

To use the binlog concurrent flush optimization feature, the instance parameter configuration must meet the following conditions:


* The running value of the `sync_binlog` parameter is not `1`.

* The running value of the `innodb_flush_log_at_trx_commit` parameter is not `1`.

* The running value of the `binlog_order_commits` parameter is `OFF`.


<span id="HhpbSdQC"></span>
## Performance data

In tests using the Sysbench oltp_update_non_index script, enabling the binlog concurrent flush optimization feature reduces transaction commit latency and stabilizes QPS, typically improving performance by 10% to 20% in high\-concurrency scenarios.
