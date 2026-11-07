---
title: "Product specifications"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications"
---

This topic describes the instance specifications of RDS for MySQL. Refer to this topic to learn about the detailed configuration of each specification.

<span id=".6KeE5qC85YiG57G7"></span>
## Specification types

MySQL instances support two specification types: Dedicated type (formerly 'General type') and General type (formerly 'Shared type'). The features of each type are as follows:


* General type:

   * Exclusive use of allocated memory and storage resources, shares CPU resources with other shared instances in the same physical machine.

   * CPU utilization is maximized through resource reuse, with high cost performance.

   * In some cases, instances will compete for CPU resources.


<span id="MCsYFmcE"></span>
## Storage types

RDS for MySQL offers four storage types: Local SSD, High performance cloud disk, Cloud ESSD FlexPL, and Cloud ESSD PL0.


* Local SSD disk: An SSD disk on the same node as the database engine. Storing data on the local SSD disk reduces I/O latency.

* Cloud ESSD FlexPL: High throughput, high IOPS, and low latency, suitable for large I/O\-intensive business scenarios.

* Cloud ESSD PL0: Balanced IOPS and throughput, and low latency, suitable for scenarios with certain IO performance requirements.

* High performance cloud disk: Built on Cloud ESSD FlexPL, it provides additional IO bursting capabilities to meet IO demands during business peaks. Suitable for scenarios with high I/O loads and I/O fluctuations.


<span id=".6KeE5qC85YiX6KGo"></span>
## Specifications

RDS for MySQL offers different specifications for different storage types.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can modify the maximum number of connections for RDS for MySQL. A larger number of connections consumes more instance resources. Configure this setting with caution. For details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_maximum_connectio">Modifying the maximum number of connections</a>.</div>


* <div data-tips="true" data-tips-type="tip">As of April 21, 2025, RDS for MySQL upgrades the specification IDs for dedicated Local SSD specifications from rds.mysql.<code>xx</code>c<code>xx</code>g to rds.mysql.d1.<code>xx</code>c<code>xx</code>g to align them with billing items in orders. These adjustments do not affect the operation or functionality of the instance.</div>


* <div data-tips="true" data-tips-type="tip">Starting from November 15, 2024 (UTC+8), the 'Shared type' specification type for RDS for MySQL will be renamed to 'General type', and the 'General type' specification type will be renamed to 'Dedicated type'. For more information, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/annoucement_of_specification_type_update">Announcement on the name change of RDS for MySQL specification types</a>.</div>


* <div data-tips="true" data-tips-type="tip">The baseline performance of a cloud disk increases with its capacity until a maximum limit is reached. Therefore, MySQL no longer provides maximum IOPS data for each cloud disk volume specification. For more details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume">ESSD FlexPL volume</a> and <a href="https://docs.byteplus.com/en/docs/ecs/esd_pl0_volume">ESSD PL0 volume</a>.</div>


   * <div data-tips="true" data-tips-type="tip">The IOPS calculation formula for a Cloud ESSD FlexPL instance is <code>IOPS=min{1800+50*Capacity (GiB),50000}</code>. For a Cloud ESSD FlexPL instance with 100 GiB of storage space, the maximum IOPS is <code>min{1800+50*100, 50000}</code>, which is 6800.</div>


   * <div data-tips="true" data-tips-type="tip">The IOPS calculation formula for a Cloud ESSD PL0 instance is <code>IOPS=min{1800+12*Capacity (GiB),10000}</code>. If a Cloud ESSD PL0 instance has 1,000 GiB of storage space, its maximum IOPS is <code>min{1800+12*1000, 10000}</code>, which is 10,000.</div>


   * <div data-tips="true" data-tips-type="tip">The IOPS calculation formula for a High performance cloud disk instance is <code>IOPS=min(1000 * Capacity (GiB), 50000)</code>. If a High performance cloud disk instance has 20 GiB of storage space, its maximum IOPS is <code>min{1000*20,10000}</code>, which is 20,000.</div>


* Local SSD

   RDS for MySQL provides the following specifications for the Local SSD storage type:

   
   |**Specification types** |**Specification ID** |**CPU** |**Memory (** GiB **)**  |**Max connections default value** |**Maximum IOPS** |**Storage space (** GiB **)**  |
   |---|---|---|---|---|---|---|
   |Dedicated type |rds.mysql.d1.2c4g |2 |4 |1200 |16000 |20~3000 |
   ||rds.mysql.d1.2c8g |2 |8 |2000 |22000 |20~3000 |
   ||rds.mysql.d1.2c16g |2 |16 |4000 |32000 |20~3000 |
   ||rds.mysql.d1.4c8g |4 |8 |2000 |32000 |20~3000 |
   ||rds.mysql.d1.4c16g |4 |16 |4000 |45000 |20~3000 |
   ||rds.mysql.d1.4c32g |4 |32 |8000 |65000 |40~3000 |
   ||rds.mysql.d1.8c16g |8 |16 |4000 |50000 |20~12000 |
   ||rds.mysql.d1.8c32g |8 |32 |8000 |65000 |40~12000 |
   ||rds.mysql.d1.8c64g |8 |64 |16000 |95000 |200~12000 |
   ||rds.mysql.d1.16c32g |16 |32 |8000 |65000 |40~12000 |
   ||rds.mysql.d1.16c64g |16 |64 |16000 |80000 |100~12000 |
   ||rds.mysql.d1.16c96g |16 |96 |24000 |80000 |100~12000 |
   ||rds.mysql.d1.16c128g |16 |128 |32000 |110000 |200~12000 |
   ||rds.mysql.d1.32c64g |32 |64 |16000 |85000 |200~16000 |
   ||rds.mysql.d1.32c128g |32 |128 |32000 |110000 |200~16000 |
   ||rds.mysql.d1.32c256g |32 |256 |48000 |140000 |300~16000 |
   ||rds.mysql.d1.64c128g |64 |128 |32000 |150000 |200~16000 |
   ||rds.mysql.d1.64c256g |64 |256 |48000 |150000 |300~16000 |
   ||rds.mysql.d1.64c512g |64 |512 |96000 |150000 |600~16000 |
   ||rds.mysql.d1.88c720g |88 |720 |150000 |150000 |800~16000 |
   |General type |rds.mysql.d1.n.1c1g |1 |1 |300 |1200 |20~3000 |
   ||rds.mysql.d1.n.1c2g |1 |2 |600 |2000 |20~3000 |
   ||rds.mysql.d1.n.2c4g |2 |4 |1200 |4000 |20~3000 |
   ||rds.mysql.d1.n.2c8g |2 |8 |2000 |6000 |20~3000 |
   ||rds.mysql.d1.n.4c8g |4 |8 |2000 |8000 |20~3000 |
   ||rds.mysql.d1.n.4c16g |4 |16 |4000 |14000 |20~3000 |
   ||rds.mysql.d1.n.8c16g |8 |16 |4000 |20000 |20~12000 |
   ||rds.mysql.d1.n.8c32g |8 |32 |8000 |28000 |40~12000 |
   ||rds.mysql.d1.n.16c32g |16 |32 |8000 |32000 |40~12000 |
   ||rds.mysql.d1.n.16c64g |16 |64 |16000 |40000 |100~12000 |
   ||rds.mysql.d1.n.32c64g |32 |64 |16000 |60000 |100~16000 |
   ||rds.mysql.d1.n.32c128g |32 |128 |32000 |80000 |200~16000 |
   |General type (ARM) |rds.mysql.d1.n.arm.2c4g |2 |4 |1200 |4000 |20~3000 |
   ||rds.mysql.d1.n.arm.2c8g |2 |8 |2000 |6000 |20~3000 |
   ||rds.mysql.d1.n.arm.4c8g |4 |8 |2000 |8000 |20~3000 |
   ||rds.mysql.d1.n.arm.4c16g |4 |16 |4000 |14000 |20~3000 |
   ||rds.mysql.d1.n.arm.8c16g |8 |16 |4000 |20000 |20~12000 |
   ||rds.mysql.d1.n.arm.8c32g |8 |32 |8000 |28000 |40~12000 |
   ||rds.mysql.d1.n.arm.16c32g |16 |32 |8000 |32000 |40~12000 |
   ||rds.mysql.d1.n.arm.16c64g |16 |64 |16000 |40000 |100~12000 |
   ||rds.mysql.d1.n.arm.32c64g |32 |64 |16000 |60000 |100~16000 |
   ||rds.mysql.d1.n.arm.32c128g |32 |128 |32000 |80000 |200~16000 |
   ||rds.mysql.d1.n.arm.32c256g |32 |256 |48000 |90000 |300~16000 |
   

* FlexPL cloud disk

   RDS for MySQL provides the following specifications for the Cloud ESSD FlexPL storage type:

   
   |**Specification types** |**Specification ID** |**CPU** |**Memory (** GiB **)**  |**Max connections default value** |**Storage space (** GiB **)**  |
   |---|---|---|---|---|---|
   |Dedicated type |rds.mysql.c.x.2c4g |2 |4 |4000 |20~32000 |
   ||rds.mysql.c.x.2c8g |2 |8 |6000 |20~32000 |
   ||rds.mysql.c.x.2c16g |2 |16 |8000 |20~32000 |
   ||rds.mysql.c.x.4c8g |4 |8 |6000 |20~32000 |
   ||rds.mysql.c.x.4c16g |4 |16 |8000 |20~32000 |
   ||rds.mysql.c.x.4c32g |4 |32 |12000 |40~32000 |
   ||rds.mysql.c.x.8c16g |8 |16 |12000 |20~32000 |
   ||rds.mysql.c.x.8c32g |8 |32 |12000 |40~32000 |
   ||rds.mysql.c.x.8c64g |8 |64 |16000 |100~32000 |
   ||rds.mysql.c.x.16c32g |16 |32 |16000 |40~32000 |
   ||rds.mysql.c.x.16c64g |16 |64 |20000 |100~32000 |
   ||rds.mysql.c.x.16c128g |16 |128 |32000 |200~32000 |
   ||rds.mysql.c.x.32c64g |32 |64 |32000 |100~32000 |
   ||rds.mysql.c.x.32c128g |32 |128 |40000 |200~32000 |
   ||rds.mysql.c.x.32c256g |32 |256 |64000 |300~32000 |
   ||rds.mysql.c.x.64c128g |64 |128 |64000 |200~32000 |
   ||rds.mysql.c.x.64c256g |64 |256 |80000 |300~32000 |
   ||rds.mysql.c.x.64c512g |64 |512 |128000 |600~32000 |
   ||rds.mysql.c.x.128c256g |128 |256 |128000 |300~32000 |
   ||rds.mysql.c.x.128c512g |128 |512 |128000 |600~32000 |
   |General type |rds.mysql.c.s.1c2g |1 |2 |2000 |20~32000 |
   ||rds.mysql.c.s.2c4g |2 |4 |4000 |20~32000 |
   ||rds.mysql.c.s.2c8g |2 |8 |6000 |20~32000 |
   ||rds.mysql.c.s.2c16g |2 |16 |8000 |20~32000 |
   ||rds.mysql.c.s.4c8g |4 |8 |6000 |20~32000 |
   ||rds.mysql.c.s.4c16g |4 |16 |8000 |20~32000 |
   ||rds.mysql.c.s.4c32g |4 |32 |12000 |40~32000 |
   ||rds.mysql.c.s.8c16g |8 |16 |8000 |20~32000 |
   ||rds.mysql.c.s.8c32g |8 |32 |10000 |40~32000 |
   ||rds.mysql.c.s.8c64g |8 |64 |16000 |100~32000 |
   ||rds.mysql.c.s.16c32g |16 |32 |10000 |40~32000 |
   ||rds.mysql.c.s.16c64g |16 |64 |16000 |100~32000 |
   ||rds.mysql.c.s.16c128g |16 |128 |32000 |200~32000 |
   

* PL0 cloud disk

   RDS for MySQL provides the following specifications for the Cloud ESSD PL0 storage type:

   
   |**Specification types** |**Specification ID** |**CPU** |**Memory (** GiB **)**  |**Max connections default value** |**Storage space (** GiB **)**  |
   |---|---|---|---|---|---|
   |Dedicated type |rds.mysql.c.x.2c4g |2 |4 |4000 |20~16000 |
   ||rds.mysql.c.x.2c8g |2 |8 |6000 |20~16000 |
   ||rds.mysql.c.x.2c16g |2 |16 |8000 |20~16000 |
   ||rds.mysql.c.x.4c8g |4 |8 |6000 |20~16000 |
   ||rds.mysql.c.x.4c16g |4 |16 |8000 |20~16000 |
   ||rds.mysql.c.x.4c32g |4 |32 |12000 |40~16000 |
   ||rds.mysql.c.x.8c16g |8 |16 |12000 |20~16000 |
   ||rds.mysql.c.x.8c32g |8 |32 |12000 |40~16000 |
   ||rds.mysql.c.x.8c64g |8 |64 |16000 |100~16000 |
   ||rds.mysql.c.x.16c32g |16 |32 |16000 |40~16000 |
   ||rds.mysql.c.x.16c64g |16 |64 |20000 |100~16000 |
   ||rds.mysql.c.x.16c128g |16 |128 |32000 |200~16000 |
   ||rds.mysql.c.x.32c64g |32 |64 |32000 |100~16000 |
   ||rds.mysql.c.x.32c128g |32 |128 |40000 |200~16000 |
   ||rds.mysql.c.x.32c256g |32 |256 |64000 |300~16000 |
   ||rds.mysql.c.x.64c128g |64 |128 |64000 |200~16000 |
   ||rds.mysql.c.x.64c256g |64 |256 |80000 |300~16000 |
   ||rds.mysql.c.x.64c512g |64 |512 |128000 |600~16000 |
   ||rds.mysql.c.x.128c256g |128 |256 |128000 |300~16000 |
   ||rds.mysql.c.x.128c512g |128 |512 |128000 |600~16000 |
   |General type |rds.mysql.c.s.1c2g |1 |2 |2000 |20~16000 |
   ||rds.mysql.c.s.2c4g |2 |4 |4000 |20~16000 |
   ||rds.mysql.c.s.2c8g |2 |8 |6000 |20~16000 |
   ||rds.mysql.c.s.2c16g |2 |16 |8000 |20~16000 |
   ||rds.mysql.c.s.4c8g |4 |8 |6000 |20~16000 |
   ||rds.mysql.c.s.4c16g |4 |16 |8000 |20~16000 |
   ||rds.mysql.c.s.4c32g |4 |32 |12000 |40~16000 |
   ||rds.mysql.c.s.8c16g |8 |16 |8000 |20~16000 |
   ||rds.mysql.c.s.8c32g |8 |32 |10000 |40~16000 |
   ||rds.mysql.c.s.8c64g |8 |64 |16000 |100~16000 |
   ||rds.mysql.c.s.16c32g |16 |64 |10000 |40~16000 |
   ||rds.mysql.c.s.16c64g |16 |64 |16000 |100~16000 |
   ||rds.mysql.c.s.16c128g |16 |128 |32000 |200~16000 |
   

* High performance cloud disk


RDS for MySQL provides the following specifications for the High performance cloud disk storage type:


|**Specification types** |**Specification ID** |**CPU** |**Memory (GiB)**  |**Max connections default value** |**Storage space (GiB)**  |
|---|---|---|---|---|---|
|Dedicated type |rds.mysql.c.x.2c4g |2 |4 |4000 |20~32000 |
||rds.mysql.c.x.2c8g |2 |8 |6000 |20~32000 |
||rds.mysql.c.x.2c16g |2 |16 |8000 |20~32000 |
||rds.mysql.c.x.4c8g |4 |8 |6000 |20~32000 |
||rds.mysql.c.x.4c16g |4 |16 |8000 |20~32000 |
||rds.mysql.c.x.4c32g |4 |32 |12000 |40~32000 |
||rds.mysql.c.x.8c16g |8 |16 |12000 |20~32000 |
||rds.mysql.c.x.8c32g |8 |32 |12000 |40~32000 |
||rds.mysql.c.x.8c64g |8 |64 |16000 |100~32000 |
||rds.mysql.c.x.16c32g |16 |32 |16000 |40~32000 |
||rds.mysql.c.x.16c64g |16 |64 |20000 |100~32000 |
||rds.mysql.c.x.16c128g |16 |128 |32000 |200~32000 |
||rds.mysql.c.x.32c64g |32 |64 |32000 |100~32000 |
||rds.mysql.c.x.32c128g |32 |128 |40000 |200~32000 |
||rds.mysql.c.x.32c256g |32 |256 |64000 |300~32000 |
||rds.mysql.c.x.64c128g |64 |128 |64000 |200~32000 |
||rds.mysql.c.x.64c256g |64 |256 |80000 |300~32000 |
||rds.mysql.c.x.64c512g |64 |512 |128000 |600~32000 |
||rds.mysql.c.x.128c256g |128 |256 |128000 |300~32000 |
||rds.mysql.c.x.128c512g |128 |512 |128000 |600~32000 |
|General type |rds.mysql.c.s.1c2g |1 |2 |2000 |20~32000 |
||rds.mysql.c.s.2c4g |2 |4 |4000 |20~32000 |
||rds.mysql.c.s.2c8g |2 |8 |6000 |20~32000 |
||rds.mysql.c.s.2c16g |2 |16 |8000 |20~32000 |
||rds.mysql.c.s.4c8g |4 |8 |6000 |20~32000 |
||rds.mysql.c.s.4c16g |4 |16 |8000 |20~32000 |
||rds.mysql.c.s.4c32g |4 |32 |12000 |40~32000 |
||rds.mysql.c.s.8c16g |8 |16 |8000 |20~32000 |
||rds.mysql.c.s.8c32g |8 |32 |10000 |40~32000 |
||rds.mysql.c.s.8c64g |8 |64 |16000 |100~32000 |
||rds.mysql.c.s.16c32g |16 |32 |16000 |40~32000 |
||rds.mysql.c.s.16c64g |16 |64 |20000 |100~32000 |
||rds.mysql.c.s.16c128g |16 |128 |32000 |200~32000 |
