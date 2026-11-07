---
title: "Performance comparison"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Performance_comparison"
---

This topic describes the performance comparison results of MySQL 5.7, MySQL 8.0, and MySQL 8.4.

<span id="JXjEZ48G"></span>
## Memory\-bound


|**Product type** |**Node specification** |**Single table data volume** |**number of tables** |**thread count** |**MySQL 5.7 QPS** |**MySQL 8.0 QPS** |**MySQL 8.4 QPS** |
|---|---|---|---|---|---|---|---|
|Double\-node Cloud Disk Type |1 core 2 GiB |3000000 |1 |16 |25321 |16514 |14506 |
|Double\-node Cloud Disk Type |2 cores 4 GiB |3000000 |2 |32 |43800 |38845 |31047 |
|Double\-node Cloud Disk Type |4 cores 16 GiB |6000000 |4 |64 |73933 |77053 |53242 |
|Double\-node Cloud Disk Type |8 cores 32 GiB |6000000 |8 |128 |107657 |106997 |90303 |
|Double\-node Cloud Disk Type |16 cores 64 GiB |6000000 |16 |256 |132946 |145771 |127440 |



|**Product type** |**Node specification** |**Single table data volume** |**number of tables** |**thread count** |**MySQL 5.7 QPS** |**MySQL 8.0 QPS** |**MySQL 8.4 QPS** |
|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |1 core 2 GiB |3000000 |1 |16 |29741 |12830 |13839 |
|Double\-node Local Disk Type |2 cores 4 GiB |3000000 |2 |32 |45121 |23844 |19055 |
|Double\-node Local Disk Type |4 cores 16 GiB |6000000 |4 |64 |88662 |63418 |45540 |
|Double\-node Local Disk Type |8 cores 32 GiB |6000000 |8 |128 |131384 |94775 |74182 |
|Double\-node Local Disk Type |16 cores 64 GiB |6000000 |16 |256 |200221 |155516 |115658 |
|Double\-node Local Disk Type |32 cores 128 GiB |6000000 |32 |512 |215074 |258548 |186715 |


<span id="JCQepgN4"></span>
## Disk I/O\-bound


|**Product type** |**Node specification** |**Single table data volume** |**number of tables** |**thread count** |**MySQL 5.7 QPS** |**MySQL 8.0 QPS** |**MySQL 8.4 QPS** |
|---|---|---|---|---|---|---|---|
|Double\-node Cloud Disk Type |1 core 2 GiB |16000000 |1 |16 |20996 |17013 |14661 |
|Double\-node Cloud Disk Type |2 cores 4 GiB |16000000 |2 |32 |37244 |36895 |28178 |
|Double\-node Cloud Disk Type |4 cores 16 GiB |32000000 |4 |64 |61285 |58286 |46162 |
|Double\-node Cloud Disk Type |8 cores 32 GiB |32000000 |8 |128 |86223 |79899 |77990 |
|Double\-node Cloud Disk Type |16 cores 64 GiB |32000000 |16 |256 |126907 |120636 |114749 |



|**Product type** |**Node specification** |**Single table data volume** |**number of tables** |**thread count** |**MySQL 5.7 QPS** |**MySQL 8.0 QPS** |**MySQL 8.4 QPS** |
|---|---|---|---|---|---|---|---|
|Double\-node Local Disk Type |1 core 2 GiB |16000000 |1 |16 |26665 |13394 |13801 |
|Double\-node Local Disk Type |2 cores 4 GiB |16000000 |2 |32 |40950 |22931 |18047 |
|Double\-node Local Disk Type |4 cores 16 GiB |32000000 |4 |64 |84471 |62182 |42710 |
|Double\-node Local Disk Type |8 cores 32 GiB |32000000 |8 |128 |119638 |92071 |73598 |
|Double\-node Local Disk Type |16 cores 64 GiB |32000000 |16 |256 |178415 |151531 |114399 |
|Double\-node Local Disk Type |32 cores 128 GiB |32000000 |32 |512 |228033 |248715 |177580 |
