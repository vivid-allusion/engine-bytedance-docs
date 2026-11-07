---
title: "Supported database types and features"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Supported_database_types_and_features"
---

This document describes the support of various features in Database Workshop DBW for different database types, helping you quickly confirm the compatibility of each feature with your database instances, thereby improving data operation and maintenance efficiency.

<span id="CwoyKlSn"></span>
## Supported database types


|Environment |Database type ||
|---|---|---|
||Relational databases |Non\-relational database |
|BytePlus Database |* RDS for MySQL<br><br>* veDB for MySQL<br><br>* RDS for SQL Server<br><br>* RDS for PostgreSQL |* Cache for Redis<br><br>* Document Database for MongoDB |
|Self\-built databases from other clouds or other vendors |* MySQL<br><br>* PostgreSQL |None |



<span id="ZMxDiibj"></span>
### Relational database feature support

For ease of browsing and content presentation, the tables in this document use the following conventions:


* ✔️ indicates that the feature is supported.

* ❌ indicates the feature is not supported.



|Function |||RDS for MySQL |veDB for MySQL |RDS for SQL Server |RDS for PostgreSQL |
|---|---|---|---|---|---|---|
|Instance list |Managed instance ||✔️ |✔️ |✔️ |✔️ |
||Security control ||✔️ |✔️ |✔️ |✔️ |
|Data management |SQL window ||✔️ |✔️ |✔️ |✔️ |
||Ticket list ||✔️ |✔️ |❌ |✔️ |
||||✔️ |✔️ |❌ |❌ |
|||Lock\-free schema change |✔️ |✔️ |❌ |❌ |
|||SQL review |✔️ |✔️ |❌ |✔️ |
|||Data cleanup and archiving |✔️ |✔️ |❌ |❌ |
|||Clear table ticket |✔️ |✔️ |❌ |❌ |
|||Data import/export |✔️ |✔️ |❌ |❌ |
|||Permission application |✔️ |✔️ |✔️ |✔️ |
||Task management ||✔️ |❌ |❌ |❌ |
|&nbsp;<br><br>Operation and maintenance management |Observation and diagnosis<br><br> |Session management |✔️ |✔️ |❌ |✔️ |
|||Transactions and locks |✔️ |✔️ |✔️ |✔️ |
|||Spatial analysis |✔️ |✔️ |❌ |✔️ |
|||Alerts and monitoring \> Monitoring panel |✔️ |✔️ |✔️ |✔️ |
|||Alerts and monitoring \-\> Anomaly detection |✔️ |✔️ |❌ |❌ |
|||Log management \> Slow log details |✔️ |✔️ |✔️ |✔️ |
|||Log management \> Slow log diagnosis |✔️ |✔️ |❌ |❌ |
|||Log management \> Error log details |✔️ |✔️ |❌ |✔️ |
|||Diagnosis |✔️ |✔️ |❌ |✔️ |
|||Database audit |✔️ |✔️ |❌ |✔️ |
|||SQL insights and auditing |✔️ |✔️ |❌ |✔️ |
|||AutoOps \> Compute scaling |✔️ |❌ |❌ |❌ |
|||AutoOps \> Storage expansion |✔️ |❌ |❌ |✔️ |
|||AutoOps \-\> Index created automatically |✔️ |✔️ |❌ |❌ |
|||AutoOps \> Auto\-throttling |✔️ |✔️ |❌ |❌ |
|||AutoOps \> Node specification scaling |❌ |✔️ |❌ |❌ |
|||AutoOps \> Scheduled scaling |❌ |✔️ |❌ |❌ |
||Database inspection ||✔️ |✔️ |❌ |✔️ |
|Corporate security |Security rules ||✔️ |✔️ |✔️ |✔️ |


&nbsp;





<span id="TEfxdFEJ"></span>
### Non\-relational database feature support

For ease of browsing and content presentation, the tables in this document use the following conventions:


* ✔️ indicates that the feature is supported.

* ❌ indicates the feature is not supported.



|Feature |||Cache for Redis |Document Database for MongoDB |
|---|---|---|---|---|
|Instances |Managed instance ||✔️ |✔️ |
||Security control ||✔️ |✔️ |
|Data management |SQL window ||✔️ |✔️ |
||Ticket list |Data import/export |❌ |✔️ |
|Operation and maintenance management |Observation and diagnosis<br><br> |Session management |❌ |✔️ |
|||Spatial analysis |❌ |✔️ |
|||Alerts and monitoring \> Monitoring panel |✔️ |✔️ |
|||Alerts and monitoring \-\> Anomaly detection |❌ |❌ |
|||Log management |❌ |✔️ |
|||Database audit |✔️ |✔️ |
|||AutoOps \> Storage expansion |❌ |✔️ |
|||AutoOps \> Bandwidth auto\-scaling |✔️ |✔️ |
||Database inspection ||✔️ |❌ |
|Corporate security |Security rules ||✔️ |✔️ |






<span id="noeTBQg1"></span>
### Self\-built databases from other clouds or other vendors

For ease of browsing and content presentation, the tables in this document use the following conventions:


* ✔️ indicates that the feature is supported.

* ❌ indicates the feature is not supported.


&nbsp;


|Function | |User self\-built MySQL |User\-built PostgreSQL |
|---|---|---|---|
|Instance list |Managed instance |✔️ |✔️ |
||Security control |✔️ |✔️ |
|Data management |SQL window |✔️ |✔️ |
