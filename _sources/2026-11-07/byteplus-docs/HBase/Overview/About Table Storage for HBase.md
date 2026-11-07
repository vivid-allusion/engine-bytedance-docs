---
title: "About Table Storage for HBase"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/About_Table_Storage_for_HBase"
---

Table Storage for HBase is a fully managed NoSQL service based on Apache HBase. It is compatible with standard HBase access protocols and offers benefits such as low\-cost storage and high\-throughput scalability.

<span id="6xmcDFMS"></span>
## Product architecture

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4da7bfae68beeb4cd7328017092d2336.png) </span>As shown in the figure above, Table Storage for HBase primarily consists of four components: Master, RegionServer, ZooKeeper, and HDFS.


* Master: Manages and coordinates RegionServers and handles create, read, update, and delete (CRUD) operations for tables. Each HBase instance can have two Master nodes (one primary and one standby) by default.

* RegionServer: Stores and manages HRegions and provides read/write services for table data. Each HBase instance can have 2 to 100 RegionServer nodes.

* ZooKeeper: Ensures high availability for the Master, monitors the online/offline status of RegionServers in real time, and promptly notifies the Master.

* HDFS: A distributed file system with three replicas by default, providing highly available and scalable file storage.


<span id=".5Lqn5ZOB5LyY5Yq_"></span>
## Product advantages

Table Storage for HBase offers the following advantages to help you build your ideal applications.


* Supports the wide table model.

* Features a high\-availability architecture where the Master uses a two\-node primary/standby mode and supports real\-time HA detection.

* Separating storage and compute ensures high data reliability. Storage uses a multi\-replica mechanism to provide at least 99.9% availability.

* It separates hot and cold data by archiving historical data to cold storage based on a defined separation point, which effectively reduces storage costs.

* Supports instance configuration changes, including horizontal scale\-out and vertical scaling. It also provides features such as monitoring and alerts, making instance management simple and convenient.


<span id=".5a6e5L6L"></span>
## Instance

The basic unit of HBase is an instance. An instance is an independent, virtualized database runtime environment composed of multiple data and proxy nodes. The Apache HBase engine runs on the data nodes. When creating an instance, you need to specify the engine version and specifications for all nodes. After creating an HBase instance, you can access it through ECS. Table Storage for HBase supports Apache HBase engine version 2.x. For more information about HBase versions, see [Apache HBase](https://hbase.apache.org/book.html).

<span id=".5a6e5L6L55uR5o6n"></span>
## Instance monitoring

You can use the Cloud Monitor service to monitor the performance and health of HBase instances and view relevant Cloud Monitor performance charts on the HBase console. For more information, see [Monitoring metrics](https://docs.byteplus.com/en/docs/HBase/Monitoring_metrics).
