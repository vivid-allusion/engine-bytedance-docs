---
title: "About RDS for MySQL"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_rds_for_mysql"
---

RDS for MySQL is an elastic and reliable online relational database service for BytePlus based on the open\-source MySQL database. RDS for MySQL instances are deployed in a cloud\-native manner and use local SSD storage to provide high\-performance read/write capabilities. They are fully compatible with the MySQL engine and provide a complete set of solutions including instance management, backups, logs, monitoring, and data migration. This helps enterprises simplify complex database management and operation tasks, allowing them to focus more on their core business.

<span id=".5Lqn5ZOB5p625p6E"></span>
## Product architecture

<span id=".6auY5Y-v55So5p625p6E"></span>
### High availability architecture

MySQL provides a one\-primary and one\-secondary high\-availability architecture type. When the primary node fails, it automatically detects and completes a second\-level primary\-secondary switch without business interruption, ensuring stability. MySQL supports backup capabilities, including data backup and log backup, and enables restore by backup set and by point in time to ensure data reliability.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8492ec2ff1701726a8802efaa87fe13a.png) </span>

<span id=".6ZuG576k5p625p6E"></span>
### Cluster architecture

MySQL uses a one\-primary, multiple\-secondary cluster architecture and supports automatic failover and manual switching. Secondary nodes are accessible, improving read capabilities. Can be scaled out to a maximum of 8 secondary nodes to further expand read capabilities.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7435306b4a663a9f3eb4ddc32cb3dd4a.png) </span>

<span id=".6K-75YaZ5YiG56a75p625p6E"></span>
### Read/write splitting

RDS for MySQL provides a read/write separation architecture with one primary node and multiple read\-only nodes. You can add up to 10 read\-only nodes to elastically scale out data read capabilities according to your business needs. It supports read/write separation by automatically forwarding read requests to read\-only nodes, which offloads the read pressure on the primary node, effectively handling scenarios with high read and low write volumes.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_7c31c21aedda8313393f574b87f3ea32.png) </span>

<span id=".5qC45b-D57uE5Lu2"></span>
## Core components


* **Primary node**


The primary node is the basic node of a MySQL instance, which provides services to external users. Other components depend on the primary node to function. In a high\-availability architecture, the primary node receives all read/write service requests. In a read/write split architecture, the primary node receives all the write requests and a portion of the read requests. The primary node stores the data modification log and syncs the log among nodes.


* **Secondary node**


The secondary node is an important node in the high\-availability architecture of a MySQL instance, ensuring the instance's service availability. The secondary node receives logs sent by the primary node and replays them to ensure data consistency between the primary and secondary nodes; in case of primary node failure, the secondary node can quickly switch to the primary node to provide services, ensuring stable business operation.


* **Read\-only node**


The read\-only node is an important node in the read/write separation architecture of an RDS for MySQL instance, responsible for handling read\-only requests. Read\-only nodes are an important node of the read/write splitting architecture of a MySQL instance. They receive log files from secondary nodes or the primary node and replay them to ensure data consistency between the read\-only nodes and the primary/secondary nodes; in scenarios with more reads and fewer writes, they handle read\-only requests and share the data read load of the primary node.

<span id=".5Lqn5ZOB54m55oCn"></span>
## Product features

**Product features Powerful hardware to ensure performance**


* RDS for MySQL uses NVMe SSDs to provide two storage types: local disk and cloud disk. With the local disk storage type, NVMe SSD's strong IO performance ensures the database's read and write access capabilities, providing high reliability and persistence for data. With the cloud disk storage type, a multiple redundancy mechanism is supported to avoid the risk of a single point of data failure, providing 99.9999999% reliability and offering reliable support for the database. Cloud disks support the end\-to\-end 16K atomic write feature, which can ensure the atomicity of each data page write, thereby safely disabling the InnoDB doublewrite mechanism. This not only greatly reduces the I/O write volume, but also simplifies the process of flushing dirty pages, thus greatly improving the write performance of MySQL.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A service period is one calendar month. Data persistence = (Total data volume in the service period \- Data volume lost in the service period) / Total data volume in the service period \* 100%.   </div>
   

**High\-availability architecture**


* It has a high\-availability primary/secondary architecture to ensure service availability. Once the primary node suffers a fault, the system automatically detects the fault and completes primary/secondary switchover within seconds.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Product data is saved in two copies in the data center without a cold backup or backups in other data centers.   </div>
   

   **Read/write splitting**

* MySQL supports the mounting of read\-only nodes, as well as the one\-primary and multi\-read\-only node architecture, to implement automatic read/write splitting to easily cope with high request volumes.


**Backup and recovery**


* Based on data backup and log backup (Binlog), RDS for MySQL supports lossless data recovery within 7 days to 12 months to ensure data reliability.


**Supports multi\-availability zone deployment**


* When creating or restoring a new instance, you can assign the primary, standby, and read\-only nodes to different availability zones within the same region to enable cross\-availability zone disaster recovery.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, restoring a single availability zone instance to a multiple availability zone instance is not supported.</div>


<span id=".5Lqn5ZOB5LyY5Yq_"></span>
## Product advantages

**Product advantages Easy management of massive databases**


* RDS for MySQL provides two cloud database management methods, namely command line and web interface, and supports batch management of database accounts and permissions.


**Backup and recovery**


* RDS for MySQL supports data import through DTS. It automatically backs up data every day. The data can be restored to any time point in the log backup retention period.


**Professional monitoring and alerting**


* Supports multi\-dimensional monitoring and custom resource threshold alarms. It provides online query and download capabilities for various logs.


**Multiple access methods**


* RDS for MySQL supports access through the internet and VPC networks to interconnect cloud databases with data centers, private clouds, and other computing resources.
