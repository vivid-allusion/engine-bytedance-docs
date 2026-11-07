---
title: "About NDB for MySQL"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/About_NDB_for_MySQL"
---

NDB for MySQL is a new generation of cloud\-native relational databases developed by BytePlus. NDB for MySQL 100% compatible with MySQL, suitable for enterprise diverse database application scenarios.

<span id="产品介绍"></span>
## Product introduction

NDB for MySQL adopts a computing and storage separation architecture, supporting up to 500TiB of ultra\-large\-capacity structured data storage, and a single database cluster can be expanded to up to 16 computing nodes. Based on the cloud\-native database design concept, NDB for MySQL combines the high performance, high reliability, and high availability of commercial databases with the advantages of simplicity, openness, rapid iteration, and efficient expansion of open source databases. After being tempered in key business scenarios and accumulating experience in the industry's top fields, NDB for MySQL can provide enterprises with secure, reliable, high\-performance, and feature\-rich database services.

<span id="PITypM8U"></span>
## Product architecture<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_84c815110cc27862a05801ddc870a622.png) </span>The overall architecture of NDB for MySQL is divided into three layers from top to bottom.


* **Proxy intelligent proxy layer**: 100% compatible with community version. No changes are required to migrate the application to the NDB for MySQL database, and the instance address supports automatic read and write separation by default.

* **SQL computing analysis layer**: based on self\-developed distributed technology implementation computing storage separation, in which write requests are processed only by the primary node, read requests will be automatically allocated to all nodes for processing. Support the addition of up to 15 read\-only nodes, and the minute\-level node expansion can effectively cope with sudden business pressures and improve overall performance.

* **Distributed storage layer**: self\-developed distributed shared storage, single instance capacity is currently up to 500TiB. According to the storage object, it can be divided into the following two parts.

   * **Distributed log storage layer (LogStore)** : Distributed redo log storage system, responsible for persistent storage of database transaction logs.

   * **Distributed data storage layer (PageStore)** : Distributed database storage system, responsible for the persistent storage of database table data.
