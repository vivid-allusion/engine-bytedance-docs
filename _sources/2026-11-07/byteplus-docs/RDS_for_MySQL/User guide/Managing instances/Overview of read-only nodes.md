---
title: "Overview of read-only nodes"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_read-only_nodes"
---

To implement elastic expansion of read capabilities and distribute the database workload, you can add one or more read‑only nodes when creating an instance or for an existing instance, which satisfy heavy database read requests and boost application throughput.

<span id=".5Yqf6IO954m554K5"></span>
## Features


* Features Region and availability zone: Read\-only nodes can be in different availability zones in the same region as the primary node.

* Specification: The specification does not need to match the primary instance and can be changed at any time. However, to avoid issues such as high latency and high load on the read\-only node, the read\-only node specification cannot be smaller than the primary node specifications.

* Network type: Only VPC is supported.

* Account and database management: You don't need to maintain account and database information as it is all synchronized from the primary node.

* Data replication: When a read\-only node is created, it replicates data from the secondary instance, and the data is consistent with the primary node.


<span id=".5Yqf6IO96ZmQ5Yi2"></span>
## Limits


* Feature restrictions Number of read\-only nodes: Up to 10 read\-only nodes can be created for each instance.

* Instance backup: Because the primary node already has a backup node, read\-only nodes do not currently support backup settings or manual backups.

* Recovery of read\-only nodes is not currently supported.

* Data migration: Migration of data to a read\-only node is not supported.

* Database management: You cannot create or delete databases.

* Account management: You cannot create or delete accounts, authorize accounts, or modify account passwords.
