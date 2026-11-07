---
title: "MySQL 5.7 Test Result"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_result_of_mysql_5_7"
---

This topic introduces the MySQL 5.7 performance test result.

<span id="DW02QvpQ"></span>
## Memory\-bound


|**Product type** |**Specification code** |**Node specification** |**Single table data volume** |**number of tables** |**Max connections** |**thread count** |**TPS** |**QPS** |
|---|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |rds.mysql.d1.n.1c2g |1 core 2 GiB |3000000 |1 |600 |16 |1487 |29741 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.1c2g ||||||1266 |25321 |
|Double\-node Local Disk Type |rds.mysql.d1.n.2c4g |2 cores 4 GiB |3000000 |2 |1200 |32<br><br> |2256 |45121 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.2c4g ||||||2190 |43800 |
|Double\-node Local Disk Type |rds.mysql.d1.n.4c16g |4 cores 16 GiB<br><br> |6000000 |4 |4000 |64<br><br> |4433 |88662 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.4c16g ||||||3697 |73933 |
|Double\-node Local Disk Type |rds.mysql.d1.n.8c32g |8 cores 32 GiB<br><br> |6000000 |8 |8000 |128 |6569 |131384 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.8c32g ||||||5383 |107657 |
|Double\-node Local Disk Type |rds.mysql.d1.n.16c64g |16 cores 64 GiB |6000000<br><br> |16 |16000 |256 |10011 |200221 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.16c64g ||||||6647 |132946 |
|Double\-node Local Disk Type |rds.mysql.d1.n.32c128g |32 cores 128 GiB |6000000 |32 |32000 |512 |10754 |215074 |


<span id="sqesZiwE"></span>
## Disk I/O\-bound


|**Product type** |**Specification code** |**Node specification** |**Single table data volume** |**number of tables** |**Max connections** |**thread count** |**TPS** |**QPS** |
|---|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |rds.mysql.d1.n.1c2g |1 core 2 GiB |16000000 |1 |600 |16 |1333 |26665 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.1c2g ||||||1050 |20996 |
|Double\-node Local Disk Type |rds.mysql.d1.n.2c4g |2 cores 4 GiB |16000000 |2 |1200 |32 |2048 |40950 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.2c4g ||||||1862 |37244 |
|Double\-node Local Disk Type |rds.mysql.d1.n.4c16g |4 cores 16 GiB<br><br> |32000000 |4 |4000 |64 |4224 |84471 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.4c16g ||||||3064 |61285 |
|Double\-node Local Disk Type |rds.mysql.d1.n.8c32g |8 cores 32 GiB<br><br> |32000000 |8 |8000 |128 |5982 |119638 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.8c32g ||||||4311 |86223 |
|Double\-node Local Disk Type |rds.mysql.d1.n.16c64g |16 cores 64 GiB |32000000 |16 |16000<br><br> |256 |8921 |178415 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.16c64g ||||||6345 |126907 |
|Double\-node Local Disk Type |rds.mysql.d1.n.32c128g |32 cores 128 GiB |32000000 |32 |32000 |512 |11402 |228033 |
