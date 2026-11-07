---
title: "Read-only instance specifications"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/read-only-instance-specification"
---

This topic describes the specifications and performance of read\-only instances for RDS for SQL Server.


|**Instance type** |**Specification type** |**Node pecification** |**CPU **  |**Memory** |**Volume IOPS **  |Volume bandwidth  |**Storage space** |
|---|---|---|---|---|---|---|---|
|**Read\-only instance** |**Exclusive Type II** |rds.mssql.3il.x8.medium.ro |2 cores |16 GiB |10,000 |1.5 Gbit/s |20 GiB ~ 4000 GiB |
|||rds.mssql.3il.x8.large.ro |4 cores |32 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.x8.xlarge.ro |8 cores |64 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.x8.2xlarge.ro |16 cores |128 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.x8.4xlarge.ro |32 cores |256 GiB |80,000 |6 Gbit/s ||
||**General Type II** |rds.mssql.3il.s2.medium.ro |2 cores |4 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s2.large.ro |4 cores |8 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s2.xlarge.ro |8 cores |16 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s2.2xlarge.ro |16 cores |32 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.s4.medium.ro |2 cores |8 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s4.large.ro |4cores |16 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s4.xlarge.ro |8 cores |32 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s4.2xlarge.ro |16 cores |64 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.s4.4xlarge.ro |32 cores |128 GiB |80,000 |6 Gbit/s ||
