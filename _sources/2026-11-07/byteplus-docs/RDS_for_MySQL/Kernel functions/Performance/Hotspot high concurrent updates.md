---
title: "Hotspot high concurrent updates"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Hotspot_high_concurrent_updates"
---

This topic describes the hotspot high concurrent updates feature provided by RDS for MySQL.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Flash sale scenarios are common business scenarios where a database experiences a large number of concurrent updates to the same row of data. The core problem of hot data updates is row lock conflicts. To solve this problem, RDS for MySQL adopts the method of batch execution for updates to the same hot rows. After SQL statements with hotspot update identifiers enter the database, the database merges the SQL statements that update the same data, thereby improving the performance of hotspot high concurrent updates.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20241215 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20230615 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limitation


* Only single\-table update operations are supported.

* Tables with triggers are not supported.

* Partitioned tables are not supported.

* `UPDATE` statements that contain `OFFSET/LIMIT/ORDER BY` are not supported.

* Queries must include a `WHERE` clause, and it must be an equality condition on an index.

* When you use the flash sale feature in a transaction block, the flash sale statement must be the last SQL statement in the transaction block.

* The columns in the UPDATE clause cannot include the primary key or the currently used index columns, unless the `where` clause fully hits the index.

* This feature is not supported on instances that run the 8.0.26 series of RDS for MySQL.


<span id=".5L2_55So6K-05piO"></span>
## Instructions


* A user specifies the flash sale update operation by using an SQL HINT. The HINT keyword is `LOGIC_UPDATE`:

   ```sql
   update /*+ LOGIC_UPDATE */ t_stock set num = num - 1 where id = X and num > 0;
   ```
   

* The batch execution design only supports hotspot update operations in non\-transactional blocks. To use flash sales within a transaction, add the HINT keyword `AUTO_LOGIC_COMMIT_ROLLBACK`, and make the hotspot update SQL the last SQL statement in the transaction. With this HINT, the database automatically commits or rolls back the transaction based on whether the UPDATE operation succeeds.

   ```sql
   begin; 
   insert into t_order(userid, stockid, num) values(X, X, X); 
   update /*+ LOGIC_UPDATE AUTO_LOGIC_COMMIT_ROLLBACK */ t_stock set num = num - 1 where id = X and num > 0;
   commit;
   ```
   


<span id=".5oCn6IO95rWL6K-V"></span>
## Performance test

The test environment is a 48\-core, 502 GiB MySQL 5.7 instance.

```sql
CREATE TABLE sbtest(id INT UNSIGNED NOT NULL AUTO_INCREMENT, c BIGINT UNSIGNED NOT NULL, PRIMARY KEY (id));

UPDATE /*+ LOGIC_UPDATE */ sbtest SET c=c-1 WHERE id = 1;
```


The test results are as follows. Without hotspot update optimization, QPS drops sharply as concurrency increases. With the optimization enabled, QPS remains stable.


|<div style="text-align: center"><br></div><br> ||<div style="text-align: center"><br>16</div><br> |<div style="text-align: center"><br>32</div><br> |<div style="text-align: center"><br>64</div><br> |<div style="text-align: center"><br>128</div><br> |<div style="text-align: center"><br>256</div><br> |<div style="text-align: center"><br>512</div><br> |<div style="text-align: center"><br>1024</div><br> |<div style="text-align: center"><br>2048</div><br> |<div style="text-align: center"><br>4096</div><br> |
|---|---|---|---|---|---|---|---|---|---|---|
|Disable flash sale |QPS |<div style="text-align: right"><br>8309.06</div><br> |<div style="text-align: right"><br>7708.74</div><br> |<div style="text-align: right"><br>6408.44</div><br> |<div style="text-align: right"><br>4006.42</div><br> |<div style="text-align: right"><br>1786.19</div><br> |<div style="text-align: right"><br>606.19</div><br> |<div style="text-align: right"><br>247.76</div><br> |<div style="text-align: right"><br>243.04</div><br> |<div style="text-align: right"><br>245.75</div><br> |
||pct99/ms |<div style="text-align: right"><br>2.78ms</div><br> |<div style="text-align: right"><br>5.03ms</div><br> |<div style="text-align: right"><br>11.61ms</div><br> |<div style="text-align: right"><br>36.68ms</div><br> |<div style="text-align: right"><br>147.62ms</div><br> |<div style="text-align: right"><br>863.30ms</div><br> |<div style="text-align: right"><br>6464.70ms</div><br> |<div style="text-align: right"><br>10195.54ms</div><br> |<div style="text-align: right"><br>18021.98ms</div><br> |
|Enable flash sale |QPS |<div style="text-align: right"><br>13002.15</div><br> |<div style="text-align: right"><br>25056.90</div><br> |<div style="text-align: right"><br>39866.60</div><br> |<div style="text-align: right"><br>64778.30</div><br> |<div style="text-align: right"><br>94073.50</div><br> |<div style="text-align: right"><br>85589.48</div><br> |<div style="text-align: right"><br>79741.77</div><br> |<div style="text-align: right"><br>76620.24</div><br> |<div style="text-align: right"><br>75845.25</div><br> |
||pct99/ms |<div style="text-align: right"><br>1.30ms</div><br> |<div style="text-align: right"><br>1.37ms</div><br> |<div style="text-align: right"><br>2.67ms</div><br> |<div style="text-align: right"><br>3.03ms</div><br> |<div style="text-align: right"><br>4.81ms</div><br> |<div style="text-align: right"><br>11.03ms</div><br> |<div style="text-align: right"><br>23.26ms</div><br> |<div style="text-align: right"><br>42.14ms</div><br> |<div style="text-align: right"><br>74.00ms</div><br> |
