---
title: "Product specifications"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications"
---

This topic describes the specifications of NDB for MySQL instances and their specific configurations.

<span id=".6KeE5qC857G75Z6L"></span>
## Storage type

NDB for MySQL provides two storage types, as shown in the table below:


|**Storage type** |**Features** |**Applicable scenarios** |
|---|---|---|
|IOOptimizedStorage<br><br> |The default storage type of the instance. It provides good performance and enhanced reliability and availability. |For business scenarios with high performance and reliability requirements and database\-centric systems, such as finance, e\-commerce, government services, and large\- and medium\-sized internet businesses. |
|IntelligentCompressedStorage |A new storage type that uses intelligent compression algorithms to compress and decompress data at the physical SSD disk level. This lowers the storage cost per unit of capacity while keeping performance impact manageable. |Application scenarios that require cost reduction and high cost\-effectiveness. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Storage type conversion rules:</div>


   * <div data-tips="true" data-tips-type="default">It supports upgrading the storage type, that is, intelligent compression storage can be upgraded to IO performance storage. For details, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Upgrading_storage_type">Upgrading storage type</a>.</div>


   * <div data-tips="true" data-tips-type="default">You cannot downgrade the storage type from IO performance storage to intelligent compressed storage.</div>


* <div data-tips="true" data-tips-type="default">To switch from IO performance storage to intelligent compressed storage, purchase a new instance and use Data Transmission Service (DTS) to migrate the data from the original instance to the new instance. For the procedure, refer to <a href="https://docs.byteplus.com/en/docs/DTS/Migrating_to_Volcano_Engine_veDB_for_MySQL">Migrating to BytePlus NDB for MySQL</a>.</div>



<span id="vNLOrX0l"></span>
## Specification type

NDB for MySQL supports two types of specifications: general type and exclusive type. The detailed information is shown in the following table:


|**Specification type** |**Description** |**Applicable scenarios** |
|---|---|---|
|General type |Exclusive access to allocated memory, sharing CPU resources with other generic instances on the same physical machine. Enjoy scale dividends through resource reuse, with high cost performance. |General\-purpose specification examples are suitable for application scenarios that require low performance stability and high cost performance. |
|Exclusive type |Completely exclusive CPU and memory, long\-term stable performance, will not be affected by the behavior of other instances on the physical machine. The top of the exclusive specification is exclusive TCE\-metal, completely monopolizing all the resources of a TCE\-metal. |Business scenarios with database as the core system. For example, finance, e\-commerce, government affairs, and large and medium\-sized Internet businesses. |


<span id="KbJgRWQF"></span>
## Node specification

Compute node specifications are detailed in the following table:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The maximum IOPS value is the sum of reads and writes, that is, maximum IOPS = maximum read IOPS + maximum write IOPS.</div>


* <div data-tips="true" data-tips-type="tip">Reading 16KB is recorded as 1 IO, and writing 4KB is recorded as 1 IO.</div>


* <div data-tips="true" data-tips-type="tip">NDB for MySQL supports modifying the maximum number of connections The larger the number of connections, the more instance resources will be consumed. It is recommended to configure carefully. For details, refer to <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_maximum_connections">Modifying the maximum number of connections</a>.</div>


* <div data-tips="true" data-tips-type="tip">To use the oversize <code>vedb.mysql.x8.11xlarge</code> and <code>vedb.mysql.x8.27large</code>, please <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support.</div>




|**Specification type** |**Specification code** |**CPU** |**Memory** |**Default max connections** |IO performance storage |||**Intelligent compression storage** |||**Storage space** |
|---|---|---|---|---|---|---|---|---|---|---|---|
||||||Maximum IOPS |Read maximum IOPS |Write maximum IOPS |**Maximum IOPS** |**Read maximum IOPS** |**Write maximum IOPS** ||
|**Exclusive type** |vedb.mysql.x4.medium |2C |8 GiB |6000 |24000 |8000 |16000 |12000 |4000 |8000 |50 GiB~100,000 GiB |
||vedb.mysql.x4.large |4C |16 GiB |8000 |66000 |33000 |33000 |33000 |16500 |16500 |50 GiB~100,000 GiB |
||vedb.mysql.x8.large |4C |32 GiB |8000 |80000 |40000 |40000 |40000<br><br> |20000 |20000 |50 GiB~100,000 GiB |
||vedb.mysql.x4.xlarge |8C |32 GiB |16000 |98000 |49000 |49000 |49000 |24500 |24500 |50 GiB~100,000 GiB |
||vedb.mysql.x8.xlarge |8C |64 GiB |16000 |110000 |55000 |55000 |55000 |27500 |27500 |50 GiB~100,000 GiB |
||vedb.mysql.x4.2xlarge |16C |64 GiB |32000 |194000 |97000 |97000 |97000 |48500 |48500 |50 GiB~100,000 GiB |
||vedb.mysql.x8.2xlarge |16C |128 GiB |32000 |194000 |97000 |97000 |97000 |48500 |48500 |50 GiB~100,000 GiB |
||vedb.mysql.x4.4xlarge |32C |128 GiB |64000 |290000 |145000 |145000 |145000 |72500 |72500 |50 GiB~500,000 GiB |
||vedb.mysql.x8.4xlarge |32C |256 GiB |64000 |290000 |145000 |145000 |145000<br><br> |72500 |72500 |50 GiB~500,000 GiB |
||vedb.mysql.x8.6xlarge |48C |384 GiB |64000 |300000 |150000 |150000 |150000<br><br> |75000 |75000 |50 GiB~500,000 GiB |
||vedb.mysql.x4.8xlarge |64C |256 GiB |64000 |300000 |150000 |150000 |150000 |75000 |75000 |50 GiB~500,000 GiB |
||vedb.mysql.x8.8xlarge |64C |512 GiB |64000 |300000 |150000 |150000 |150000<br><br> |75000 |75000 |50 GiB~500,000 GiB |
||vedb.mysql.x8.11xlarge |88C |710 GiB |100000 |384000 |192000 |192000 |192000 |96000 |96000 |50 GiB~500,000 GiB |
||vedb.mysql.x8.27large |108C |864 GiB |100000 |523000 |261500 |261500 |261500<br><br> |130750 |130750 |50 GiB~500,000 GiB |
|**General type** |vedb.mysql.g2.medium |2C |4 GiB |1800 |12000 |4000 |8000 |6000 |2000 |4000 |50 GiB~100,000 GiB |
||vedb.mysql.g4.medium |2C |8 GiB |2000 |24000 |8000 |16000 |12000 |4000 |8000 |50 GiB~100,000 GiB |
||vedb.mysql.g4.large |4C |16 GiB |8000 |44000 |22000 |22000 |22000 |11000 |11000 |50 GiB~100,000 GiB |
||vedb.mysql.g4.xlarge |8C |32 GiB |16000 |56000 |28000 |28000 |28000<br><br> |14000 |14000 |50 GiB~100,000 GiB |
||vedb.mysql.g4.2xlarge |16C |64 GiB |32000 |65000 |32500 |32500 |32500 |16250 |16250 |50 GiB~100,000 GiB |
||vedb.mysql.g8.2xlarge |16C |128 GiB |32000 |65000 |32500 |32500 |32500 |16250 |16250 |50 GiB~100,000 GiB |
||vedb.mysql.g4.4xlarge |32C |128 GiB |64000 |86000 |43000 |43000 |43000 |21500 |21500 |50 GiB~500,000 GiB |
