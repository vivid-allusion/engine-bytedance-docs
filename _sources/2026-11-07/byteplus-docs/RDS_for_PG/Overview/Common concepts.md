---
title: "Common concepts"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/common_concepts"
---

This topic summarizes common concepts and specific explanations of RDS for PostgreSQL instances.


|Term |Concept |
|---|---|
|Region |The geographical location of the data. |
|Availability zones |Abbreviated as AZ. Each region has multiple zones isolated from each other called availability zones. |
|Instance |The basic unit of resource management for RDS for PostgreSQL. Different specifications of instances have varying performance (such as CPU cores and memory). For more information on the instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications). |
|Instance type |Different choices of node specification capabilities and types for PostgreSQL instances. |
|Primary node |The primary data node, the basic node of a PostgreSQL instance for providing services to external parties. |
|Secondary node |The secondary node is a backup data node. When the primary node fails, it can switch to the primary node and provide services to the outside world. |
|Read\-only node |Nodes that provide read\-only capabilities, handle read\-only requests, and share the data read load of the primary node. |
|High availability |Abbreviated as HA. Once the primary node suffers a fault, the system automatically detects the fault and completes the primary/secondary switchover within seconds. |
|Private network address |Connection address when accessing PostgreSQL instances through the virtual private cloud (for example, when ECS and PostgreSQL instances are in the same VPC). |
|Public network address |connection address for public network access to the PostgreSQL instance. |
|Replication slot |Replication slot is a unique mechanism of PostgreSQL database, which is used to avoid data loss or duplicate replication in streaming replication and improve the reliability of data replication. |
|WAL |WAL stands for Write Ahead Log, which is the online redo log in PostgreSQL used to ensure data durability in the database. |
