---
title: "Common concepts"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Common_concepts"
---

This topic explains some of the terms used when discussing NDB for MySQL instances.


|Concepts |Description |
|---|---|
|Region |The geographical location of the NDB for MySQL server. You can specify a region when creating the NDB for MySQL instance. After the instance is created, you cannot change the region. |
|Availability zone |Refers to a physical area in which electricity and network are isolated from each other in the same region. Internal network interoperability between availability zones results in smaller network latency and fault isolation between different availability zones. |
|Instance |Instance The basic unit for managing cloud resources in NDB for MySQL. |
|Instance name |You can customize the name of the NDB for MySQL instance. |
|Instance ID |After a user creates the NDB for MySQL instance, the system automatically generates an ID, which is globally unique. |
|Instance specification |NDB for MySQL resource configuration for each node in the instance, including CPU cores and memory size. |
|DB engine version |NDB for MySQL provides MySQL 5.7 and MySQL 8.0 versions, InnoDB engine. |
|Primary node |Also known as a read\-write node, it can provide read and write functions. There is only one primary node in the NDB for MySQL instance. |
|Read\-only node |Only read functionality is provided. NDB for MySQL instance can have up to 15 read\-only nodes simultaneously. |
|Switching between primary and secondary nodes |Refers to promoting a read\-only node to the primary node. When a system failure occurs, the NDB for MySQL instance automatically switches between the primary and secondary servers. You can also manually switch between primary and standby by designating a read\-only node as the new primary node. |
|Primary node endpoint |The primary endpoint proxies read and write requests that access only the primary node. In the event of a primary\-standby switch, the connection end point will automatically associate the new primary node. |
|Default endpoint |The default endpoint integrates the primary node and all read\-only nodes, and provides a unified read\-write address for accessing the NDB for MySQL instance. The default endpoint supports automatic elastic expansion, read and write separation, load balancing and other capabilities. |
|Virtual private cloud |A Virtual Private Cloud (VPC) A VPC is an isolated network environment with higher security and performance than a classic network. |
|Storage space |NDB for MySQL storage capacity size.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Pay\-as\-you\-go instances do not require storage space to be configured and are charged hourly based on actual usage.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The storage billing type of the subscription instance supports pay\-as\-you\-go or subscription:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">If you choose to pay\-as\-you\-go, you don't need to configure storage space, and you will be charged by the hour based on the actual usage.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">When selecting a subscription, you need to choose the storage size when creating the instance, and pay up front based on the storage size.</div><br> |
|Backup |A backup saves all the data in the NDB for MySQL instance at a certain point in time. NDB for MySQL provides two methods: automatic backup and manual backup, which can effectively prevent data loss and avoid the risks caused by misoperation. |
|Log |Logs are records of NDB for MySQL operations. |
