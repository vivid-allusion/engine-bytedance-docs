---
title: "Can the task automatically handle newly added tables or schema changes at the source end during runtime?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Can_newly_added_tables_"
---

* Synchronization task: when the synchronization type includes incremental synchronization, and the synchronization objects are full\-database synchronization, newly added tables or tables with schema changes in the source database can be synchronized to the target.

* Migration task:

   * When the migration type includes incremental migration and the migration object is full\-database migration, newly added tables in the source database can be migrated to the target.

   * It is recommended to add new tables in the source database before starting the migration task or during the incremental migration phase.
