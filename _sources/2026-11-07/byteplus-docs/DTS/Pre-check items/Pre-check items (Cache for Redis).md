---
title: "Pre-check items (Cache for Redis)"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_redis"
---

Database Transmission Service (DTS) performs various checks on databases before creating or configuring migration or synchronization tasks for Cache for Redis. This topic introduces the details of check items.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pre\-check items for Cache for Redis apply to all migration and synchronization types.</div>



|**Item** |**Level** |**Check content** |**Remarks** |
|---|---|---|---|
|Environment check |Warning |Environment check. |None |
|Database connection and schema wildcard rule check |Error |Check the database and schema wildcard rules. |None |
|Source database connectivity check |Error |Check whether the data transmission server can connect to the source database. |None |
|Target database connectivity check |Error |Check whether the data transmission server can connect to the target database. |None |
|Source database permission check |Error |Verify whether the source database's account privileges meet the requirements for migration and synchronization. |Privileges refer to the `psync` privilege. |
|Source database existence check |Error |Check whether the specified database exists in the source database. |None |
|Target database role check |Warning |Check whether the role of the target database is master. |None |
|Target database existence check |Error |Check whether the specified database exists in the target database. |None |
|Target database data existence check |Warning |Check if the target database is empty. |When migrating to the Cache for Redis enterprise edition cache database, only the migration of DB 0 is supported. |
|Target database eviction policy check |Warning |Check whether the eviction policy of the target database is Noeviction. |None |
|Source database version check |Error |Check the version of the source database. |None |
|Database version consistency check |Warning |Check whether the database versions of the source database and the target database are consistent. |None |
|Check tables in the same instance and database on the source and target ends |Error |Check whether the source and target ends are the same instance and database & table. |None |
|Cache for Redis module list consistency check |Error |Check if the loaded Cache for Redis module list is consistent. |Applicable to data synchronization tasks. |
