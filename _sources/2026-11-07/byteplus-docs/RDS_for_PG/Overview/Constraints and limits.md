---
title: "Constraints and limits"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/constraints_limits"
---

Instance parameters are modified via the console or API. However, only certain parameters can be modified to ensure security and stability.


|Constraint |Description |
|---|---|
|Instance parameters |Instance parameters are modified via the console or API. However, only certain parameters can be modified to ensure security and stability. |
|Account privileges |SuperUser permission is not provided. |
|Database backup |Physical backup is supported via the console or API only. |
|Database recovery |Physical recovery is supported via the console or API only. |
|Database replication |PostgreSQL adopts a primary\-secondary replication structure, where the secondary node is not directly accessible by users. |
|Instance parameters are modified via the console or API. However, only certain parameters can be modified to ensure security and stability. |Instances are restarted via the console or API only. |
|Large objects |RDS for PostgreSQL instances support the use of large objects, but not their import or export. |
