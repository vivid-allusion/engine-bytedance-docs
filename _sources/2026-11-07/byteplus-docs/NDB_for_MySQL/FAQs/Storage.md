---
title: "Storage"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Storage"
---

<span id="elTjNfGP"></span>
### How to reduce instance disk usage?


* If you delete a database or table directly, the used storage space will automatically decrease.

* If you use the `DELETE` statement to delete data, the space occupied by the table is not automatically released. Subsequent operations like `INSERT` and `UPDATE` will reuse this space. To reduce disk usage, you can rebuild the table by running the `alter table xxx engine=innodb;` statement to release fragmented space. This action locks the table.

* If the billing method of the instance is subscription and the used storage is less than the total storage capacity selected when the instance was created, you can modify the storage space based on actual usage. For details, refer to [Changing node specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Changing_node_specifications).


<span id="ALnDc1X8"></span>
### The storage space usage metric on the monitoring and alert dashboard has not been updated for a long time?

For small size instances with over 100,000 tables, the initial statistics collection after a restart can take hours to complete. This is because the current system scans tablespace information serially, and the initial scan time is positively correlated with the number of tables.

<span id="LWo8JRy4"></span>
### How to view the size of each table in NDB for MySQL?

You can log in to the DBW console to view table space usage by using the **Space analysis** function. For details, refer to [Space analysis management](https://docs.byteplus.com/en/docs/DBW/Space_analysis_management).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">A maximum of 2,000 table space data entries can be displayed.</div>


* <div data-tips="true" data-tips-type="default">The data is based on the system database <code>information_schema.tables</code>.</div>



<span id="hGEe8xbZ"></span>
### Storage type comparison

NDB for MySQL provides two storage types for different business scenarios that differ in price and performance. This topic describes the differences between the two storage types to help you make a selection.

<span id="sZuUnB5G"></span>
#### Introduction

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



<span id="JuAcL8zz"></span>
#### Price

The following table compares the prices of IO performance and intelligent compressed storage:


|**Type** |**Pay\-as\-you\-go (** USD **/GiB/hour)**  |||**Subscription (** USD **/GiB/month)**  |||
|---|---|---|---|---|---|---|
||**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |
|IOOptimizedStorage |0.00077 |||0.30972067 |||
|IntelligentCompressedStorage |0.0005082 |||0.204415642 |||


<span id="2Ncpa0nU"></span>
#### **Performance metric differences**


|**Specification type** |**Specification code** |**CPU** |**Memory** |**Default max connections** |IO performance storage |||**Intelligent compression storage type** |||**Storage space** |
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


<span id="l23B6WBC"></span>
#### Upgrade storage type

Upgrading the storage type from intelligent compression to IO\-performance is supported. For detailed instructions, refer to [Upgrading storage type](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Upgrading_storage_type).
