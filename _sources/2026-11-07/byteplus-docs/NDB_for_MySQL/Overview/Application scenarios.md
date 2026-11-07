---
title: "Application scenarios"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Application_scenarios"
---

This article introduces common application scenarios of NDB for MySQL.

<span id="互联网或电商"></span>
## Internet or e\-commerce scenarios


* **Business characteristics**

   In Internet or e\-commerce scenarios, business often grows explosively, business fluctuations change frequently, and traffic peaks are difficult to predict.

* **How to deal with it**

   * Massive data storage: Storage capacity is used on demand and can support up to 500TiB of storage space.

   * Rapid expansion:

      * NDB for MySQL instances support 1 primary node and up to 15 read\-only nodes.

      * Support minutes to add read\-only nodes and configuration changes to meet the requirements of horizontal and vertical performance expansion, automatic load balancing after expansion, no business perception.


<span id="游戏"></span>
## Game


* **Business characteristics**

   In gaming scenarios, server opening and merging operations need to be performed frequently. During business peaks, it may be necessary to support high concurrency pressure from millions of players online at the same time.

* **How to deal with it**

   * Strong and stable performance: NDB for MySQL instances support 1 primary node and up to 15 read\-only nodes, support fast upgrade and downgrade in minutes and millions of QPS, provide excellent data writing capabilities under high concurrency, and easily cope with business peaks.

   * Massive data storage: The storage capacity can be used on demand, and up to 500TiB of storage space can be supported, eliminating the tedious operation of combining areas and services.


<span id="企业应用"></span>
## Enterprise Application


* **Business characteristics**

   There are very strict requirements for the high availability, high reliability, and high security of the database, while ensuring the consistency of the data.

* **How to deal with it**

   * Data consistency guarantee: The design of shared distributed storage completely solves the defect of non\-strong consistency of backup database data caused by master\-slave replication.

   * High availability and high reliability: When any node in the instance fails, data loss can be guaranteed and business can be restored in seconds.

   * Support IP allowlist, VPC, data multiple copies storage and other functions, providing comprehensive security for database data access, storage, management and other aspects.
