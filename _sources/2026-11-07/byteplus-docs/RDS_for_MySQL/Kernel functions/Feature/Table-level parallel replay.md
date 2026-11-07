---
title: "Table-level parallel replay"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Table-level_parallel_replay"
---

This topic describes the table\-level parallel replay feature provided by RDS for MySQL, its applicable scenarios, supported versions, and optimization effects on the binlog copy link.

<span id="WYGRFka9"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20260215 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20260215 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id="3VVe2w4q"></span>
## Background

In the following two typical scenarios, the performance of the binlog copy capability is lower than expected. In these two scenarios, if the parallel copy algorithm is set to `DATABASE` (database\-level concurrency), binlog replay on the secondary instance degenerates into a serial model because all write operations are performed on the same database. This leads to a significant increase in primary\-secondary latency when the load on the primary instance increases. If the algorithm is changed to `LOGICAL_CLOCK` (which requires the calculation of `WRITESET`), the large number of transaction conflicts on the primary instance significantly increases the overhead of transaction dependency calculation, which impacts normal business operations.

First, almost all user writes are concentrated in multiple tables within the same database, and cross\-table access is rare.

Second, a large number of transaction conflicts occur on a single table, and the primary database consumes significant resources when calculating transaction dependencies.

<span id="s4iZtGxa"></span>
## Feature description

To address the shortcomings of `LOGICAL_CLOCK` and `DATABASE` in specific scenarios, we propose a table\-based (`TABLE`) parallel replay strategy. The core idea is to allow transactions on different tables to be replayed in parallel on the secondary database without relying on the logical clock calculation of the primary database. This strategy does not require the primary database to perform row\-level conflict detection, which significantly reduces the performance overhead of the primary database. It also significantly improves the replay efficiency of the secondary database by replaying transactions on different tables in parallel.

<span id="2fXBAGuO"></span>
## Instructions

<span id="lNBNv7CB"></span>
### Parameter description

RDS for MySQL provides the following modifiable parameters to configure the parallel replay feature. For more information about modifying parameters, see [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).


|**Parameter name** |**Supported version** |**Default value** |**Whether an instance restart is required for the change to take effect** |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|slave_parallel_type<br><br> |MySQL 5.7<br><br> |LOGICAL_CLOCK |Yes<br><br> |[DATABASE\|LOGICAL_CLOCK\|TABLE] |GLOBAL<br><br> |The parallel strategy for transactions when a replica instance replicates binlogs. |
|replica_parallel_type |MySQL 8.0<br><br> ||||||


<span id="M0CWQ0Mz"></span>
### Precautions

In most cases, the performance of TABLE\-based parallel copy **is not significantly** better than that of LOGICAL_CLOCK\-based parallel copy.

Before using the table\-level parallel replay feature, confirm that the service model falls within the scope of models described in the background information. In addition, confirm that the LOGICAL_CLOCK (WRITESET)\-based parallel copy capability has impacted the performance of the primary database, the copy efficiency of the secondary database does not meet expectations, and the problem of excessive primary\-secondary latency frequently occurs.
