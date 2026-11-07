---
title: "Read-only node overview"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/overview_of_read-only_nodes"
---

To implement elastic expansion of read capabilities and distribute the database workload, RDS for PostgreSQL supports creating read\-only nodes. To implement elastic expansion of read capabilities and distribute the database workload, you can create one or more read\-only nodes while creating an instance.

<span id=".5Yqf6IO954m554K5"></span>
## **Features**


* Specification: it can differ from the primary node and can be changed at any time. However, to avoid high latency and high load on read\-only nodes, the number of cores and memory of read\-only nodes cannot be less than half of the primary node specifications. For example, if the primary node specification is 8C16G, the number of cores for the read\-only node cannot be less than 4, and the memory cannot be less than 8.

* Network type: Only private network is supported.

* Account and database management:No account or database maintenance is required for read\-only nodes. Both the account and database are synced from the primary node.

* Allowlist: The allowlist information of the primary node is automatically replicated at read\-only node creation.

* Data replication: data is replicated from the secondary node at read\-only node creation, and the secondary node data is consistent with that on the primary node. Any data updates on the primary node will be automatically synced to all the read\-only nodes immediately when the operation is completed on the primary node.


<span id=".5Yqf6IO96ZmQ5Yi2"></span>
## **Limits**


* Number of read\-only nodes: You can create 10 read\-only nodes at the maximum for each primary node.

* Instance backup: Because the primary node already has a backup node, read\-only nodes do not currently support backup settings or manual backups.

* Instance recovery: Currently, read\-only nodes do not support data recovery.

* Data migration: Currently, data cannot be migrated to read\-only nodes.

* Database management: Currently, you cannot create or delete databases.

* Account management: Currently, you cannot create or delete accounts, authorize accounts, or modify account passwords.
