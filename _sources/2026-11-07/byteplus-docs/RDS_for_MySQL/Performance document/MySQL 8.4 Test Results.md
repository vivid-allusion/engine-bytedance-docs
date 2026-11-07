---
title: "MySQL 8.4 Test Results"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_result_of_mysql_8_4"
---

This topic introduces the MySQL 8.4 performance test results.

<span id="EhjgEgfz"></span>
## Memory\-bound


|**Product type** |**Specification code** |**Node specification** |**Single table data volume** |**number of tables** |**Max connections** |**thread count** |**TPS** |**QPS** |
|---|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |rds.mysql.d1.n.1c2g |1 core 2 GiB |3000000 |1 |600 |16 |692 |13839 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.1c2g ||||||725 |14506 |
|Double\-node Local Disk Type |rds.mysql.d1.n.2c4g |2 cores 4 GiB |3000000 |2 |1200 |32 |953 |19055 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.2c4g ||||||1552 |31047 |
|Double\-node Local Disk Type |rds.mysql.d1.n.4c16g |4 cores 16 GiB<br><br> |6000000 |4 |4000 |64<br><br> |2277 |45540 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.4c16g ||||||2662 |53242 |
|Double\-node Local Disk Type |rds.mysql.d1.n.8c32g |8 cores 32 GiB<br><br> |6000000 |8 |8000 |128 |3709 |74182 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.8c32g ||||||4515 |90303 |
|Double\-node Local Disk Type |rds.mysql.d1.n.16c64g |16 cores 64 GiB |6000000 |16 |16000 |256 |5783 |115658 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.16c64g ||||||6372 |127440 |
|Double\-node Local Disk Type |rds.mysql.d1.n.32c128g |32 cores 128 GiB |6000000 |32 |32000 |512 |9336 |186715 |


<span id="RviOLkEg"></span>
## Disk I/O\-bound


|**Product type** |**Specification code** |**Node specification** |**Single table data volume** |**number of tables** |**Max connections** |**thread count** |**TPS** |**QPS** |
|---|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |rds.mysql.d1.n.1c2g |1 core 2 GiB |16000000 |1 |600 |16 |690 |13801 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.1c2g ||||||733 |14661 |
|Double\-node Local Disk Type |rds.mysql.d1.n.2c4g |2 cores 4 GiB |16000000 |2 |1200 |32 |902 |18047 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.2c4g ||||||1409 |28178 |
|Double\-node Local Disk Type |rds.mysql.d1.n.4c16g |4 cores 16 GiB<br><br> |32000000 |4 |4000 |64 |2135 |42710 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.4c16g ||||||2308 |46162 |
|Double\-node Local Disk Type |rds.mysql.d1.n.8c32g |8 cores 32 GiB<br><br> |32000000 |8 |8000 |128 |3680 |73598 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.8c32g ||||||3899 |77990 |
|Double\-node Local Disk Type |rds.mysql.d1.n.16c64g |16 cores 64 GiB |32000000 |16 |16000 |256 |5720 |114399 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.16c64g ||||||5737 |114749 |
|Double\-node Local Disk Type |rds.mysql.d1.n.32c128g |32 cores 128 GiB |32000000 |32 |32000 |512 |8879 |177580 |
