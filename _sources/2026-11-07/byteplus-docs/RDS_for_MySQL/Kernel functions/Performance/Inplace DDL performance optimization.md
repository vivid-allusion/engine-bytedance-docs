---
title: "Inplace DDL performance optimization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Inplace_DDL_performance_optimization"
---

This topic describes the inplace DDL performance optimization feature of RDS for MySQL.

<span id="KpZR63vc"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20251015 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.43_20251215 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id="DrcnGIXB"></span>
## Background

In some DDL scenarios, the performance of community MySQL 8.0 is lower than that of MySQL 5.7. Creating an index in MySQL involves the scan, sort, insert, and flush stages. The time statistics for each stage show that the sort and insert stages are the most time\-consuming. For example, in community MySQL 8.0, when creating an index on 40 million rows of Sysbench data with a single thread, the sort and insert stages account for up to 72% of the total execution time.

<span id="GbuWJX8w"></span>
## Feature description

RDS for MySQL has optimized some hot\-spot functions, such as removing unnecessary page validation in the insert stage, optimizing the two\-way merge sort algorithm, and optimizing the execution path.

<span id="0clfPXiv"></span>
## Instructions

<span id="1DqQFaGR"></span>
### Parameter description

RDS for MySQL provides a modifiable parameter for MySQL 8.0 and MySQL 8.4 instances to enable or disable the Inplace DDL optimization feature.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In RDS for MySQL 5.7 instances, there is no separate modifiable parameter for setting the Inplace DDL optimization feature. If the <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/Parallel_DDL">Parallel DDL</a> feature is enabled on a MySQL 5.7 instance, the Inplace DDL optimization feature is enabled by default.</div>



|**Parameter name** |**Type** |**Default value** |**Does it need instance restart to take effect?**  |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|loose_innodb_inplace_ddl_optimize |bool<br><br> |OFF<br><br> |No |[ON/OFF] |GLOBAL/SESSION<br><br> |Enables or disables the inplace DDL optimization feature. Values:<br><br><br>* `ON`: enable.<br><br>* `OFF`: disable. |


<span id="WACThzqW"></span>
### Examples

To use the Inplace DDL optimization feature in RDS for MySQL 8.0 and MySQL 8.4 instances, perform the following steps.


1. Modify the `loose_innodb_inplace_ddl_optimize` parameter to `ON`. For more information about modifying parameters, see [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

2. Use Inplace DDL optimization to create an index.


Create the index.

```SQL
CREATE INDEX <index_name> ON <table_name>(<column_name>);
```



3. Use the Inplace DDL optimization feature to execute the DDL for rebuilding the table.


The DDL statement for Inplace DDL optimization is as follows.

```SQL
ALTER TABLE <table_name> ADD COLUMN <column_name> <column_type>, ALGORITHM=INPLACE;
```


<span id="ZSNgpmdj"></span>
## Performance test

<span id="ag0vF9uO"></span>
### Test Environment


* Instance specification: RDS for MySQL 32C64G

* Instance version: MySQL 8.0

* Test data: 8 GiB of Sysbench data


<span id="zfZkCJy0"></span>
### Test steps

Create indexes for the test data by using different concurrency levels in a Community Edition MySQL 8.0 instance and an RDS for MySQL 8.0 instance. Record the total time for index creation and the sum of the time for the sorting and insertion phases.

<span id="tBgw2aWp"></span>
### The test results are as follows.


* Index creation time



|Concurrency |MySQL 8.0 Community Edition (Unit: Second) |RDS for MySQL 8.0 (Unit: Second) |Performance improvement percentage |
|---|---|---|---|
|1 |<div style="text-align: right"><br>110.76</div><br> |<div style="text-align: right"><br>81.27</div><br> |<div style="text-align: right"><br>36.20%</div><br> |
|2 |<div style="text-align: right"><br>69.19</div><br> |<div style="text-align: right"><br>51.25</div><br> |<div style="text-align: right"><br>35%</div><br> |
|4 |<div style="text-align: right"><br>51.52</div><br> |<div style="text-align: right"><br>43.73</div><br> |<div style="text-align: right"><br>17.80%</div><br> |
|8 |<div style="text-align: right"><br>43.3</div><br> |<div style="text-align: right"><br>36.33</div><br> |<div style="text-align: right"><br>19.10%</div><br> |
|16 |<div style="text-align: right"><br>40.59</div><br> |<div style="text-align: right"><br>35.26</div><br> |<div style="text-align: right"><br>15.10%</div><br> |
|32 |<div style="text-align: right"><br>42.95</div><br> |<div style="text-align: right"><br>36.06</div><br> |<div style="text-align: right"><br>19.10%</div><br> |



* Sum of the time for the sorting and insertion phases



|Concurrency |MySQL 8.0 Community Edition (Unit: Second) |RDS for MySQL 8.0 (Unit: Second) |Performance improvement percentage |
|---|---|---|---|
|1 |<div style="text-align: right"><br>79.9</div><br> |<div style="text-align: right"><br>51</div><br> |<div style="text-align: right"><br>56.60%</div><br> |
|2 |<div style="text-align: right"><br>50.15</div><br> |<div style="text-align: right"><br>32.03</div><br> |<div style="text-align: right"><br>56.50%</div><br> |
|4 |<div style="text-align: right"><br>40.31</div><br> |<div style="text-align: right"><br>30.53</div><br> |<div style="text-align: right"><br>32.03%</div><br> |
|8 |<div style="text-align: right"><br>35.93</div><br> |<div style="text-align: right"><br>28.53</div><br> |<div style="text-align: right"><br>25.90%</div><br> |
|16 |<div style="text-align: right"><br>35.23</div><br> |<div style="text-align: right"><br>28.55</div><br> |<div style="text-align: right"><br>23.30%</div><br> |
|32 |<div style="text-align: right"><br>37.27</div><br> |<div style="text-align: right"><br>30.82</div><br> |<div style="text-align: right"><br>20.90%</div><br> |
