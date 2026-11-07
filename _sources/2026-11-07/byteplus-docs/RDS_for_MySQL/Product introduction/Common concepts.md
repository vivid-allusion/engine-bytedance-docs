---
title: "Common concepts"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/common_concepts"
---

This topic explains some of the terms used when discussing RDS for MySQL instances.


|**Term** |**Description** |
|---|---|
|Region |Geographical location of the data. |
|Availability zone |Abbreviated as AZ. Each region has multiple zones isolated from each other called availability zones. |
|Instance |The basic unit for managing cloud resources in RDS for MySQL. Different instance specifications have different performance levels (such as different numbers of CPU cores and memory sizes). For more information about instance specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/RDS_for_MySQL/product_specifications). |
|Instance type |Instance specifications refer to different options of MySQL instances in terms of node specifications and capacities. |
|Primary node |The primary data node, the basic node of a MySQL instance for providing services to external parties. |
|Secondary node |The secondary data node. A secondary node transforms into a primary one in case of a primary node fault to continue the services to external parties. |
|Read\-only node |Read\-only nodes provide read\-only capabilities and process read\-only requests to share the data read load of the primary node. |
|VPC |A **Virtual Private Cloud** or VPC. A VPC is an isolated network environment with higher security and performance than a classic network. |
|High availability |Abbreviated as HA. A primary/secondary system ensures service stability. Once the primary node suffers a fault, the system automatically detects the fault and completes the primary/secondary switchover within seconds. |
|Read/Write splitting |Through the read/write splitting proxy, some read requests are forwarded to the read\-only nodes, and the primary node only processes the write requests and a portion of the read requests. In this way, read\-only nodes share the data reading workload of the primary node. |
|Private address |The private address for accessing a MySQL instance (such as when the ECS and MySQL instances are within the same VPC). |
|Public address |The public address for accessing a MySQL instance. |
