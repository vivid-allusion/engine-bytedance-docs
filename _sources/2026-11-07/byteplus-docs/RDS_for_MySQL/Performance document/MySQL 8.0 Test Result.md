---
title: "MySQL 8.0 Test Result"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/test_result_of_mysql_8_0"
---

This topic describes the MySQL 8.0 performance test results.

<span id="U36I3BVZ"></span>
## Memory\-bound


|**Product type** |**Specification code** |**Node specification** |**Single table data volume** |**number of tables** |**Max connections** |**thread count** |**TPS** |**QPS** |
|---|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |rds.mysql.d1.n.1c2g |1 core 2 GiB |3000000 |1 |600 |16 |642 |12830 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.1c2g ||||||826 |16514 |
|Double\-node Local Disk Type |rds.mysql.d1.n.2c4g |2 cores 4 GiB |3000000 |2 |1200 |32 |1192 |23844 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.2c4g ||||||1942 |38845 |
|Double\-node Local Disk Type |rds.mysql.d1.n.4c16g |4 cores 16 GiB<br><br> |6000000 |4 |4000 |64<br><br> |3171 |63418 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.4c16g ||||||3853 |77053 |
|Double\-node Local Disk Type |rds.mysql.d1.n.8c32g |8 cores 32 GiB<br><br> |6000000 |8 |8000 |128 |4739 |94775 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.8c32g ||||||5350 |106997 |
|Double\-node Local Disk Type |rds.mysql.d1.n.16c64g |16 cores 64 GiB |6000000 |16 |16000 |256 |7776 |155516 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.16c64g ||||||7289 |145771 |
|Double\-node Local Disk Type |rds.mysql.d1.n.32c128g |32 cores 128 GiB |6000000 |32 |32000 |512 |12927 |258548 |


<span id="Ifl2oCNz"></span>
## Disk I/O\-bound


|**Product type** |**Specification code** |**Node specification** |**Single table data volume** |**number of tables** |**Max connections** |**thread count** |**TPS** |**QPS** |
|---|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |rds.mysql.d1.n.1c2g |1 core 2 GiB |16000000 |1 |600 |16 |670 |13394 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.1c2g ||||||851 |17013 |
|Double\-node Local Disk Type |rds.mysql.d1.n.2c4g |2 cores 4 GiB |16000000 |2 |1200 |32 |1147 |22931 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.2c4g ||||||1845 |36895 |
|Double\-node Local Disk Type |rds.mysql.d1.n.4c16g |4 cores 16 GiB<br><br> |32000000 |4 |4000 |64 |3109 |62182 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.4c16g ||||||2914 |58286 |
|Double\-node Local Disk Type |rds.mysql.d1.n.8c32g |8 cores 32 GiB<br><br> |32000000 |8 |8000 |128 |4604 |92071 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.8c32g ||||||3995 |79899 |
|Double\-node Local Disk Type |rds.mysql.d1.n.16c64g |16 cores 64 GiB |32000000 |16 |16000 |256 |7577 |151531 |
|Double\-node Cloud Disk Type |rds.mysql.c.s.16c64g ||||||6032 |120636 |
|Double\-node Local Disk Type |rds.mysql.d1.n.32c128g |32 cores 128 GiB |32000000 |32 |32000 |512 |12436 |248715 |
