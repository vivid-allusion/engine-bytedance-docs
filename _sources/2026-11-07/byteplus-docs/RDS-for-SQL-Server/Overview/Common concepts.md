---
title: "Common concepts"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/common-concepts"
---

This article summarizes the glossary of cloud database instances of RDS for SQL Server.


|term |concept |
|---|---|
|Region |The geographical location where the data is located. |
|Availability Zones |AZ for short. Each region has multiple isolated zones, called availability zones. |
|Main Instance |RDS for SQL Server is the basic unit for cloud resource management. The specifications of the instance (e.g. CPU cores, memory size, etc.) vary, and the performance of the instance also varies. For more information on instance specifications, see [Product Specifications](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/master-instance-specification). |
|Read\-only instance |A read\-only instance is a copy of the primary instance and is primarily used to handle read requests, but not write requests. Read\-only instances maintain data consistency with the master instance by periodically replicating data from the master instance. A read\-only instance can perform read operations independently of the primary instance without affecting the performance of the primary instance. |
|Instance Type |Different choices of SQL Server instances in terms of node specifications, capabilities, and types. |
|Primary Node |The master data node is the base node for SQL Server instances to provide services externally. |
|Secondary Node |Standby data node, when the master node fails, it can switch to a standby node that provides services to the master node and externally. |
|Private Network (VPC) |Virtual Private Cloud (VPC) is an isolated network environment with higher security and performance than traditional classical networks. |
|High Availability |Abbreviated as HA. The business stability is guaranteed through the master and standby architecture. After the master node fails, it will automatically detect and complete the second\-level master and standby switching. |
|Private Internet Address (Internal Address) |The connection address when accessing a SQL Server instance over a private network, such as when ECS and SQL Server instances are in the same VPC. |
