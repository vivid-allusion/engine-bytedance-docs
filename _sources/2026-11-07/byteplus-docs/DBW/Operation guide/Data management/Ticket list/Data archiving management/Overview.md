---
title: "Overview"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/overview"
---

The Database Workshop (DBW) offers data cleaning and archiving functions. It can help you periodically filter and remove inactive data from the storage system, thereby reducing online storage costs and improving the database's query performance and operational efficiency.

<span id="use-cases"></span>
## **Application scenarios**

When dealing with systems that generate large volumes of daily data, accumulated historical information often becomes rarely accessed. DBW's data archiving and cleanup feature enables periodic maintenance of such historical data. Typical application scenarios include:


* Financial sector: transaction records, bills, securities trading, and other historical data.

* Healthcare: patient cases, diagnostic records, prescriptions, and other historical data.

* E\-commerce: order records, customer purchase history, inventory change records, and historical data.


<span id="advantages"></span>
## Advantages

The data cleaning and archiving feature has the following advantages.


* **Storage space optimization: ** Convert valuable primary storage space occupied by long\-term historical data into available space by archiving inactive data, significantly improving storage efficiency.

* **System performance improvement: ** Reduce the size of active datasets, resulting in noticeably faster query speeds and enhanced transaction processing performance for database systems.

* **Simplified data management: ** Help organizations better manage data lifecycles by removing inactive data, reducing data clutter, and improving overall data management efficiency.


<span id="the-difference-between-dbw-data-cleaning-archiving-and-dts-data-migration"></span>
## Differences between DBW data cleaning and archiving & DTS data migration

While both DBW's data cleaning/archiving and DTS's data migration involve moving data, they differ significantly in purpose, functionality, and application scenarios, as detailed in the following table.


|**Difference type** |**DBW data cleaning and archiving** |**DTS data migration** |
|---|---|---|
|**Purpose** |The main purpose of data cleaning and archiving is to relocate historical data that is no longer frequently accessed from primary storage systems. This process converts occupied storage space into available capacity while enhancing system performance, and ensures long\-term data preservation for compliance requirements.  |The main purpose of data migration is to move data between different data storage systems for system upgrades, data integration, data replication, and other purposes.  |
|**Application scenarios** |Data cleaning and archiving are suitable for removing infrequently accessed data such as historical transaction records, medical records, and log management. |Data migration is suitable for data cloud migration, cross\-account data migration within the Volcanic Engine, database splitting or expansion, and other business scenarios. |


<span id="precautions"></span>
## Precautions


* The data cleaning and archiving feature is currently only suitable for small\-scale data volumes. For large\-scale archiving operations that may fail, submit a ticket for technical support.

* Archive tasks may fail when processing tables containing large fields (such as BLOB and TEXT) or rows with substantial data volume. 

* Data cleaning and archiving may impact running business services. We recommend performing such operations during off\-peak hours.

* Currently, archiving of tables containing virtual columns is not supported. 

* The feature is exclusively available for cleaning and archiving data in BytePlus's RDS for MySQL and NDB for MySQL databases.

* The archived data is filtered based on the conditions specified in the ticket configuration, which operates on database query results. Ensure the filtering conditions deliver the intended query results.

* At present, data can only be backed up to the built\-in TOS in CSV format. Backup data will be automatically deleted after 30 days of retention.

* The download URL for backup data in the built\-in TOS can be obtained through the **View logs** option in the ticket details. To download backup data, [Submit a ticket](https://console.byteplus.com/workorder/create) promptly. For reimporting downloaded backup data into databases, refer to [Creating a data import ticket (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-a-data-import-ticket) or [Creating a data import ticket (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_a_data_import_ticket).

* Since backup data uses UTF\-8 character encoding, the exported data can only be imported into tables supporting UTF\-8 character sets.


<span id="guidance-on-archival-cleaning-paths"></span>
## Guidance


* [Creating a data cleaning and archiving ticket (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/create-data-cleansing-and-archiving-ticket-for-mysql)

* [Creating a data cleaning and archiving ticket (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/create-data-cleansing-and-archiving-ticket-for-mysql)
