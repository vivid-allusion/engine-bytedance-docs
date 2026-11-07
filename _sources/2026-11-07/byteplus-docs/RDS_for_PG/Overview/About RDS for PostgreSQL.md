---
title: "About RDS for PostgreSQL"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/about_rds_for_postgresql"
---

RDS for PostgreSQL is a flexible and reliable online relational database service built by BytePlus based on the open\-source database PostgreSQL. PostgreSQL instances are deployed in a cloud\-native manner with high read/write performance based on local SSD storage. They are fully compatible with the PostgreSQL engine and provide packaged solutions such as instance management and backup and recovery to streamline database management, operation, and maintenance tasks. As a result, enterprises can dedicate more time and resources to their core businesses.

<span id=".5Lqn5ZOB5p625p6E"></span>
## Product architecture

<span id=".6auY5Y-v55So5p625p6E"></span>
### High availability architecture

PostgreSQL provides a one\-primary and one\-secondary high\-availability architecture type. When the primary node fails, it automatically detects and completes a second\-level primary\-secondary switch without business interruption, ensuring stability. PostgreSQL supports backup capabilities, including data backup and log backup, and enables restore by backup set and by point in time to ensure data reliability.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_088defd63fb9d0dc92a9f546b393ac2d.png) </span>

<span id=".5LiA5Li75aSa6K-75p625p6E"></span>
### **One\-primary and multi\-read\-only architecture**

PostgreSQL supports one\-primary and multi\-read\-only architecture, allowing the attachment of read\-only nodes. Once read/write splitting is enabled, the architecture implements auto read/write splitting to easily cope with high request volumes.

<span id=".5qC45b-D57uE5Lu2"></span>
## Core components


* **Primary node**


The primary node is the basic node of a PostgreSQL instance, which provides services to external users. Other components depend on the primary node to function. In a high\-availability architecture, the primary node receives all read/write service requests. In a read/write split architecture, the primary node receives all the write requests and a portion of the read requests. The primary node stores the data modification log and syncs the log among nodes.


* **Secondary node**


The secondary node is an important node in the high\-availability architecture of a PostgreSQL instance, ensuring the instance's service availability. The secondary node receives logs sent by the primary node and replays them to ensure data consistency between the primary and secondary nodes; in case of primary node failure, the secondary node can quickly switch to the primary node to provide services, ensuring stable business operation.


* **Read\-only node**


The read\-only node handles read\-only requests. Read\-only nodes are an important node of the read/write splitting architecture of a MySQL instance. They receive log files from secondary nodes or the primary node and replay them to ensure data consistency between the read\-only nodes and the primary/secondary nodes; in scenarios with more reads and fewer writes, they handle read\-only requests and share the data read load of the primary node.

<span id=".5Lqn5ZOB54m55oCn"></span>
## Product features

RDS for PostgreSQL offers the following features to help you build an ideal app: Easy to use

**Easy to use**


* The web interface offers simplified daily management functions such as create instance, modify configurations, restart, and delete.


**High\-availability architecture**


* It has a high\-availability primary/secondary architecture to ensure service availability. Once the primary node suffers a fault, the system automatically detects the fault and completes primary/secondary switchover within seconds.


**Backup and recovery**


* RDS for PostgreSQL supports lossless data recovery based on backup files within 7 days to 12 months to ensure data reliability.


**Support for multi\-availability zone deployment**

Supports assigning the primary node, secondary node, and read\-only node to different availability zones within the same region when creating or restoring an instance, enabling cross\-availability zone disaster recovery. For example, when creating an instance with one primary node, one secondary node, and one read\-only node in the North China 2 (Beijing) region, you can choose to deploy the primary node in availability zone A, the secondary node in availability zone B, and the read\-only node in availability zone C.

<span id=".5Lqn5ZOB5LyY5Yq_"></span>
## Product advantages

**Easy management of massive databases**


* RDS for PostgreSQL provides two cloud database management methods, namely command line and web interface, and supports batch management of database accounts and permissions.


**Data backup and recovery**


* RDS for PostgreSQL supports automatic daily backups and data recovery by backup file or backup timepoint.


**Multiple access methods**


* Supports access via public network and virtual private cloud. You can connect the cloud database with IDC, private cloud, or other computing resources through these access methods.
