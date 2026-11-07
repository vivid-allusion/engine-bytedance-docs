---
title: "About RDS for SQL Server"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/about-RDS-for-SQL-Server"
---

<span id="product-definition"></span>
## Product Definition

RDS for SQL Server is a stable, reliable and scalable online database service created by BytePlus based on the world\-class commercial database product Microsoft SQL Server. SQL Server instances are deployed in a cloud\-native manner, providing high\-performance read and write capabilities by combining extremely fast SSD cloud disks. RDS for SQL Server is fully compatible with various applications under the Microsoft ecosystem, and provides a complete set of solutions for instance management, backup and recovery, log management, monitoring and alerting, data migration, etc., to help enterprises simplify complex database management and operation and maintenance tasks, so that enterprises have more time and resources to focus on their core business.

<span id="product-architecture"></span>
## Product Architecture

RDS for SQL Server supports the creation of instances of Basic, High Availability, and Cluster architecture types.

<span id="infrastructure"></span>
### infrastructure

The RDS for SQL Server provides the infrastructure architecture, also known as the stand\-alone architecture, which only provides a single\-node deployment method and does not promise SLAs. The advantages, disadvantages, and applicable scenarios of the infrastructure are as follows:


* Advantages: Cost\-effective.

* Disadvantages: When the stand\-alone version malfunctions, there is no guarantee that the business can be restored in a timely manner.

* Applicable scenarios: The infrastructure is suitable for personal learning, microsites, SME development and testing environments, etc.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fbe82c0a0cb3559765bee55e6173366.png) </span>

<span id="high-availability-architecture"></span>
### High Availability Architecture

RDS for SQL Server provides a primary and secondary high availability architecture type that supports high availability across AZs such as primary and secondary availability zones supported in different availability zones (AZs), promising SLAs. The advantages, disadvantages, and applicable scenarios of a high\-availability architecture are as follows:


* Advantages: The high\-availability architecture supports the automatic handover of the master and standby nodes when the master node fails, achieving high service availability. The high availability architecture promises SLAs.

* Disadvantages: When the master node fails, the main and standby switching will cause a short service interruption of about 30s to 60s. If there is a replication delay, the primary and secondary switch may take a little longer, and you need to ensure that the client side of the database you are using supports reconnection.

* Applicable scenarios: The high\-availability architecture is suitable for the production databases of large and medium\-sized enterprises, such as the Internet, Internet of Things, retail e\-commerce, logistics, gaming, and other industries.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ebdf1c35fa56542e8b22163f26f5b6e.png) </span>

<span id="cluster-architecture"></span>
### cluster architecture

RDS for SQL Server provides a cluster version architecture, which supports one master, one spare and multiple read\-only on the basis of supporting high availability. You can create multiple read\-only instances on demand to achieve read\-write separation load balancing and commit to SLAs. The advantages, disadvantages, and applicable scenarios of the clustered architecture are as follows:


* Advantages: Higher availability, reliability, and scalability.

* Disadvantages: When the master node fails, the main and standby switching will cause a short service interruption of about 30s to 60s. If there is a replication delay, the primary and secondary switch may take a little longer, and you need to ensure that the client side of the database you are using supports reconnection.

* Applicable scenarios: The cluster version architecture is suitable for industries such as finance, the Internet, hotels, and online education.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3700d7b22c1a8f9fccf6dbde05528e08.png) </span>

<span id="core-component"></span>
## core component

**master node**

The Primary Node is the basic node for SQL Server instances to provide services to the outside world, and other components rely on the Primary Node to function. In the high availability architecture, the master node receives all read and write requests of the service; in the read\-write separation architecture, the master node receives all write requests and partial read requests of the service. The master node records the data modification log and transmits the log to other nodes to achieve data synchronization between nodes.

**standby node**

Secondary Node is an important node in SQL Server instance's high availability architecture to ensure the high availability of instances. The standby node receives the log transmitted by the master node and replays it to ensure the consistency of data between the master and standby nodes; when the master node fails, the standby node can quickly switch the master node and provide services to the outside world to ensure the stable operation of the business.

**Read only node**

A read\-only node (ReadOnly Node) is an important node in the read\-write separation architecture of RDS for SQL Server instances, responsible for processing read\-only requests. The read\-only node is mainly used to share the reading pressure of the master node. When there are a large number of read requests in the database, a master node may not be able to meet the pressure of a large number of read and write requests at the same time. Read\-only nodes can help you reduce the read pressure of the master node and improve the overall processing power of the system.

<span id="product-advantage"></span>
## Product advantage

RDS for SQL Server offers the following product advantages:


* **Easy to buy**

   RDS for SQL Server has Microsoft's genuine license license, which can be purchased on demand, quickly created and used, and avoids complicated business agreements.

* **high availability**

   Cloud database SQL Server version adopts hot standby architecture, automatic inspection, and second\-level switching of failures to effectively ensure application SLA compliance.

* **high reliability**

   RDS for SQL Server uses Tinder Object Storage (TOS) to achieve low\-cost database backup and support recovery to any point in time.

* **High security**

   * RDS for SQL Server supports multi\-dimensional monitoring, custom resource definition threshold alarms, and provides online query and download capabilities for a variety of logs.

   * RDS for SQL Server supports public and private network access, and realizes encrypted transmission and secure access control capabilities through whitelisting.
