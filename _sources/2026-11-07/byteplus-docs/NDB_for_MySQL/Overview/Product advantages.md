---
title: "Product advantages"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_advantages"
---

This article introduces the product advantages of NDB for MySQL.

<span id=".5byA5pS-55Sf5oCB"></span>
## Open ecology

NDB for MySQL 100% compatible with MySQL open source relational database engine, code/application without modification or only a small amount of modification.

<span id=".5by65Yqy5oCn6IO9"></span>
## Powerful performance


* Based on MySQL kernel deep optimization, while using physical replication, distributed shared storage, greatly improve the overall performance.

* The instance contains a primary node and up to 15 read\-only nodes, which meets the performance requirements of high\-concurrency scenarios, especially for scenarios with more reads and less writes.

* Based on shared storage, it is possible to scale read\-only nodes in minutes. Once the expansion is completed, the load balancing is automatic, and the pressure is distributed to all nodes.


<span id=".5rW36YeP5a2Y5YKo"></span>
## Mass Storage

Adopting a distributed storage system, a single instance can reach up to 500 TiB.

<span id=".5pmu5oOg5pyN5Yqh"></span>
## Inclusive service


* Storage and computing separation: multiple computing nodes share storage, and only pay for computing nodes when adding read\-only nodes, which greatly reduces the cost of expansion.

* Flexible charging methods: Computing nodes and storage space can be charged in a variety of combinations, and the most suitable charging method can be selected according to business needs, which can better control costs and be adjusted according to actual usage.


<span id=".56iz5a6a5Y-v6Z2g"></span>
## Stable and reliable

NDB for MySQL has no single point of failure, and guarantees high reliability and high availability of services through underlying architecture design such as distributed storage.


* The design of shared distributed storage completely solves the defect of non\-strong consistency of standby data caused by master\-slave replication, so that the entire database instance can guarantee zero data loss when dealing with any single node failure.

* Support IP allowlist, VPC, data multiple copies storage and other functions, providing comprehensive security for database data access, storage, management and other aspects.


<span id=".5p6B6YCf5omp5a65"></span>
## Extremely fast expansion

Through a variety of technologies to ensure the service efficiency of flexible expansion scenarios such as lift distribution, to cope with uncertain business growth.


* Configure lift, take effect in 5 minutes. Adopting container virtualization technology enables the database server's CPU and memory to be rapidly expanded.

* Node additions and deletions will take effect in 5 minutes. Through distributed storage pool technology, there is no need to synchronize data to increase or decrease nodes; by using cluster addresses, automatic load balancing is possible, and there is no awareness of the application layer.


<span id=".5b-r6YCf5Zue5qGj"></span>
## Quick recovery

Data recovery is performed on running or released instances by restoring from a backup set and restoring to a point in time in the past.


* Full Recovery: Restore the backup data of a running or deleted instance to a new instance, including all database accounts and other data. Suitable for instance\-level data recovery scenarios.

* Databases and tables recovery: Restore some databases or tables in a running instance to the original instance without affecting existing data. It is suitable for scenarios where part of the data needs to be restored in the business.
