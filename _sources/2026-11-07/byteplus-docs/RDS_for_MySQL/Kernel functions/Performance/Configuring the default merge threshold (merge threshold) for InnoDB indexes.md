---
title: "Configuring the default merge threshold (merge threshold) for InnoDB indexes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Configuring_the_default_merge_threshold_for_InnoDB_indexes"
---

This topic describes information about configuring the default merge threshold for InnoDB indexes.

<span id="ixpTQpaN"></span>
## Supported version


* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.

* MySQL 8.0 with a kernel minor version between MySQL 8.0.43_20251015 and MySQL 8.0.43_20260216.

* MySQL 5.7 with a kernel minor version between MySQL 5.7.44_20251015 and MySQL 5.7.44_20260216.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In MySQL 8.0 kernel minor version MySQL 8.0.43_20260415 and MySQL 5.7 kernel minor version MySQL 5.7.44_20260415, the fill logic for InnoDB indexes is optimized to reduce the frequency of index splits and merges. Therefore, for subsequent kernel versions, you <strong>do not need to manually</strong> configure the default merge threshold for InnoDB indexes.</div>


<span id="Ve2adkv4"></span>
## Background

In cloud disk scenarios, the IO bandwidth of the cloud disk often becomes a performance bottleneck.

Analysis shows that in scenarios with frequent updates, InnoDB B+\-tree index pages are frequently split and merged. Each time an index page is split or merged, many pages are modified and become dirty pages that need to be flushed to the cloud disk. In addition, a large number of redo logs are written when the index page is split or merged, which further increases the IO pressure on the cloud disk.

InnoDB B+\-tree indexes have a merge threshold property. When the fill factor of an index page is less than the merge threshold, InnoDB attempts to merge the page with an adjacent page. The default merge threshold for InnoDB B+ tree indexes is 50%, meaning InnoDB often merges two index pages with a fill rate of about 50% into a single page with a fill rate of nearly 100%. When new data is inserted, the newly merged page must split again, leading to frequent splits and merges.

Based on this analysis, lowering the merge threshold for B+ tree indexes can reduce the number of splits and merges, which alleviates cloud disk IO pressure and improves overall performance. MySQL allows setting the merge threshold by using COMMENT, for example:

```SQL
-- The merge threshold of pk is 40%, and the merge threshold of k1 is 30%
CREATE TABLE t(
  id INT,
  c1 INT,
  c2 INT,
  PRIMARY KEY pk(id) COMMENT 'MERGE_THRESHOLD=40',
  KEY k1(c1) COMMENT 'MERGE_THRESHOLD=30'
) ENGINE=innodb;
```


In addition, MySQL allows setting the merge threshold at the table level by using COMMENT, which affects all indexes in the table. For example:

```SQL
-- The index-level COMMENT has a higher priority, so the merge threshold of pk is 40%,
-- The merge threshold of k1 is 30%
CREATE TABLE t(
  id INT,
  c1 INT,
  c2 INT,
  PRIMARY KEY pk(id),
  KEY k1(c1) COMMENT 'MERGE_THRESHOLD=30'
) ENGINE=innodb COMMENT='MERGE_THRESHOLD=40';
```


<span id="mZRIPBWG"></span>
## Feature description

Although MySQL provides a method to configure the merge threshold, the default merge threshold was not configurable and was always 50% before this feature was introduced. This feature provides a way to configure the default merge threshold. It allows users to adjust the InnoDB index merge threshold more flexibly to achieve better performance in scenarios where input/output (IO) bandwidth, such as on a cloud disk, becomes a bottleneck.

<span id="wnZykSdB"></span>
## Instructions

<span id="LmQYcBYz"></span>
### Parameter description

RDS for MySQL provides the modifiable parameter loose_innodb_default_index_merge_threshold to configure the default merge threshold for InnoDB secondary indexes.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A change in the merge threshold of the primary key index may cause the space occupied by the table to expand significantly. Therefore, modifying loose_innodb_default_index_merge_threshold only impacts the default merge threshold for InnoDB secondary indexes. The default merge threshold for InnoDB primary key indexes is not affected and remains at 50%. To modify the default merge threshold of a primary key index, specify it manually in the index's COMMENT.</div>



|**Parameter name** |**Type** |**Default value** |**Does it need instance restart to take effect?**  |**Value range** |**Scope** |**Parameter description** |
|---|---|---|---|---|---|---|
|loose_innodb_default_index_merge_threshold |int |* When the storage type of the instance is local disk, the running value of the parameter is 50.<br><br>* When the instance storage type is , the running value of this parameter is 25. |No<br><br> |[1, 50] |GLOBAL \| SESSION |Used to set the default merge threshold for InnoDB secondary indexes. |


<span id="8nGyHouX"></span>
### Examples


1. Set the loose_innodb_default_index_merge_threshold parameter at the SESSION level.


```SQL
SET SESSION loose_innodb_default_index_merge_threshold = 40;
```



2. When an InnoDB secondary index is subsequently created in this SESSION, its merge threshold defaults to 40% if not specified:


```SQL
SET SESSION loose_innodb_default_index_merge_threshold = 40;

-- pk is the primary key index, merge threshold is 50%. k1 is a secondary index, merge threshold is 40%.
CREATE TABLE t(
  id INT,
  c1 INT,
  c2 INT,
  PRIMARY KEY pk(id),
  KEY k1(c1)
) ENGINE=innodb;

-- k2 is a secondary index, merge threshold is 40%.
CREATE INDEX k2 ON t(c2);
```


<span id="aNRKY1zJ"></span>
### Precautions


* loose_innodb_default_index_merge_threshold can only specify the default merge threshold for InnoDB secondary indexes and does not change the default merge threshold for InnoDB primary key indexes. The default merge threshold for InnoDB primary key indexes is currently fixed at 50%.

* loose_innodb_default_index_merge_threshold only impacts InnoDB B+ tree indexes. Spatial indexes, full\-text indexes, and vector indexes do not have the concept of a merge threshold and are therefore not impacted by this parameter.


<span id="RVUnYE09"></span>
## Performance data

<span id="8FimZM2q"></span>
### Test Environment


* Test version: Version 5.7

* Instance specification: RDS for MySQL, general\-purpose cloud disk, 8C32G

* Sysbench data volume: 16 sysbench tables with 2 million rows each (approximately 72 GB)

* Sysbench test case: oltp_update_index


<span id="fJoy49cy"></span>
### The test results are as follows.

In a  scenario, with loose_innodb_default_index_merge_threshold set to 50 and 25, the recorded TPS at different concurrency levels are shown in the figure below.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_762936659e652cb329a4f5a4334bd4ef.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_523882a06425ed40f0700a813d12e952.png) </span>

&nbsp;

At different concurrency levels, setting loose_innodb_default_index_merge_threshold to 25 results in a 5% to 20% higher TPS than setting it to 50.
