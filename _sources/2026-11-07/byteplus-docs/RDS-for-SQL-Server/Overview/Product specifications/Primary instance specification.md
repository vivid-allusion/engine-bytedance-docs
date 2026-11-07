---
title: "Primary instance specification"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification"
---

This topic describes the performance and specifications of RDS for SQL Server primary instances.

<span id="EtVOZ87I"></span>
## Description

RDS for SQL Server supports three edition types: Standard Edition, Enterprise Edition, and Web Edition. SQL Server instance types support Single\-node Edition, High\-availability Edition, and Cluster Edition. The High\-availability and Cluster editions use a high\-availability architecture with one primary and one standby node. By default, the specifications of the secondary node are the same as those of the primary node. Specification types support General Type II and Exclusive Type II.

<span id="svT2X36y"></span>
## Specification series 

SQL Server primary instances support the following specifications:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">SQL Server 2019 Standard Edition, SQL Server 2022 Standard Edition, hereinafter referred to as Standard Edition.</div>


* <div data-tips="true" data-tips-type="default">SQL Server 2019 Enterprise Edition, SQL Server 2022 Enterprise Edition, hereinafter referred to as Enterprise Edition.</div>


* <div data-tips="true" data-tips-type="default">SQL Server 2019 Web Edition, SQL Server 2022 Web Edition are hereinafter referred to as Web Edition.</div>




<Tabs>
<Tab zoneid="rFbD5Psm" title="Standard edition">
<TabTitle>Standard edition</TabTitle>


|**Instance type** |**Specification type** |**Node specification** |**CPU** |**Memory** |**Cloud disk IOPS** |**Cloud disk** bandwidth |**Storage space** |
|---|---|---|---|---|---|---|---|
|**High availability** |**General Type II** |rds.mssql.3il.s2.medium.s2 |2 Cores |4 GiB |10,000 |1.5 Gbit/s |20 GiB ~ 4000 GiB |
|||rds.mssql.3il.s2.large.s2 |4 Cores |8 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s2.xlarge.s2 |8 Cores |16 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s2.2xlarge.s2 |16 Cores |32 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.s4.medium.s2 |2 Cores |8 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s4.large.s2 |4 Cores |16 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s4.xlarge.s2 |8 Cores |32 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s4.2xlarge.s2 |16 Cores |64 GiB |40,000 |5 Gbit/s ||
||**Exclusive Type II** |rds.mssql.3il.x8.medium.s2 |2 Cores |16 GiB |10,000 |1 Gbit/s ||
|||rds.mssql.3il.x8.large.s2 |4 Cores |32 GiB |20,000 |1.5 Gbit/s ||
|||rds.mssql.3il.x8.xlarge.s2 |8 Cores |64 GiB |30,000 |2 Gbit/s ||
|||rds.mssql.3il.x8.2xlarge.s2 |16 Cores |128 GiB |40,000 |3 Gbit/s ||
|||rds.mssql.3il.x8.3xlarge.s2 |24 Cores |192 GiB |80,000 |5 Gbit/s ||
|**Single node edition** |**General Type II** |rds.mssql.3il.s2.medium.s1 |2 Cores |4 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s2.large.s1 |4 Cores |8 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s2.xlarge.s1 |8 Cores |16 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s2.2xlarge.s1 |16 Cores |32 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.s4.medium.s1 |2 Cores |8 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s4.large.s1 |4 Cores |16 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s4.xlarge.s1 |8 Cores |32 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s4.2xlarge.s1 |16 Cores |64 GiB |40,000 |5 Gbit/s ||
||**Exclusive Type II** |rds.mssql.3il.x8.medium.s1 |2 Cores |16 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.x8.large.s1 |4 Cores |32 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.x8.xlarge.s1 |8 Cores |64 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.x8.2xlarge.s1 |16 Cores |128 GiB |40,000 |5 Gbit/s ||





</Tab>
<Tab zoneid="E5UOvgop" title="Enterprise edition">
<TabTitle>Enterprise edition</TabTitle>


|**Instance type** |**Specification type** |**Node specification** |**CPU** |**Memory** |**Cloud disk IOPS** |**Cloud disk** bandwidth |**Storage space** |
|---|---|---|---|---|---|---|---|
|**Cluster edition** |**Exclusive Type II** |rds.mssql.3il.x4.medium.e2 |2 Cores |8 GiB |10,000 |1.5 Gbit/s |20 GiB ~ 4000 GiB |
|||rds.mssql.3il.x4.large.e2 |4 Cores |16 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.x4.xlarge.e2 |8 Cores |32 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.x4.2xlarge.e2 |16 Cores |64 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.x4.4xlarge.e2 |32 Cores |128 GiB |80,000 |6 Gbit/s ||
|||rds.mssql.3il.x4.8xlarge.e2 |64 Cores |256 GiB |170,000 |10 Gbit/s ||
|||rds.mssql.3il.x8.medium.e2 |2 Cores |16 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.x8.large.e2 |4 Cores |32 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.x8.xlarge.e2 |8 Cores |64 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.x8.2xlarge.e2 |16 Cores |128 GiB |40,000 |5 Gbit/s ||
|||rds.mssql.3il.x8.4xlarge.e2 |32 Cores |256 GiB |80,000 |6 Gbit/s ||
|**Single node edition** |**General Type II** |rds.mssql.3il.s2.medium.e1 |2 Cores |4 GiB |10,000 |1 Gbit/s ||
|||rds.mssql.3il.s2.large.e1 |4 Cores |8 GiB |20,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s2.xlarge.e1 |8 Cores |16 GiB |30,000 |2 Gbit/s ||
|||rds.mssql.3il.s2.2xlarge.e1 |16 Cores |32 GiB |40,000 |3 Gbit/s ||
|||rds.mssql.3il.s4.medium.e1 |2 Cores |8 GiB |10,000 |1 Gbit/s ||
|||rds.mssql.3il.s4.large.e1 |4 Cores |16 GiB |20,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s4.xlarge.e1 |8 Cores |32 GiB |30,000 |2 Gbit/s ||
|||rds.mssql.3il.s4.2xlarge.e1 |16 Cores |64 GiB |40,000 |3 Gbit/s ||





</Tab>
<Tab zoneid="ERHExINd" title="Web edition">
<TabTitle>Web edition</TabTitle>


|**Instance type** |**Specification type** |**Node specification** |**CPU** |**Memory** |**Cloud disk IOPS** |**Cloud disk** bandwidth |**Storage space** |
|---|---|---|---|---|---|---|---|
|**Single node edition** |**General Type II** |rds.mssql.3il.s2.medium.w1 |2 Cores |4 GiB |10,000 |1 Gbit/s |20 GiB ~ 4000 GiB |
|||rds.mssql.3il.s2.large.w1 |4 Cores |8 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s2.xlarge.w1 |8 Cores |16 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s2.2xlarge.w1 |16 Cores |32 GiB |40,000 |4 Gbit/s ||
|||rds.mssql.3il.s4.medium.w1 |2 Cores |8 GiB |10,000 |1.5 Gbit/s ||
|||rds.mssql.3il.s4.large.w1 |4 Cores |16 GiB |20,000 |2 Gbit/s ||
|||rds.mssql.3il.s4.xlarge.w1 |8 Cores |32 GiB |30,000 |3 Gbit/s ||
|||rds.mssql.3il.s4.2xlarge.w1 |16 Cores |64 GiB |40,000 |5 Gbit/s ||





</Tab>
</Tabs>


<span id="DaiWYUON"></span>
## Related documents

[Read-only instance specifications](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/read-only-instance-specification?lang=zh)
