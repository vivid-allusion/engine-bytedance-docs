---
title: "Kyuubi overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Kyuubi_overview"
---

Apache Kyuubi is a distributed, multi\-tenant, high\-performance gateway that provides SQL query services for a wide range of compute engines in data lakes.

<span id="功能特性"></span>
## Features

Here are some of the features of Kyuubi:


|Features |Note |
|---|---|
|Unified interface |Kyuubi implements the standard Hive Service RPC module. With Kyuubi, you can access data in the same way as with Hive Server2 and STS. |
|Multi\-tenancy |Kyuubi provides security for enterprise applications through a unified authentication and authorization system, enabling end\-to\-end multi\-tenant support for data access. This multi\-tenant support also enables more robust resource management. At the appropriate sharing level, by isolating different tenants in separate engines, it is possible to control each tenant's resource usage with finer granularity and simultaneously isolate the impact of erroneous jobs from different tenants. |
|High availability & load balancing |With ZooKeeper's service discovery capabilities, Kyuubi provides unlimited horizontal scalability for servers, supports theoretically unlimited client requests, and delivers enterprise\-grade SLA guarantees. |


<span id="文档指引"></span>
## Documentation guide


* To quickly get started with Kyuubi features, refer to the documentation[Kyuubi quickstart](https://docs.byteplus.com/docs/E-MapReduce/109327).

* To learn more about Kyuubi and its advanced features, refer to the documentation[Kyuubi advanced features](https://docs.byteplus.com/docs/E-MapReduce/109324).
