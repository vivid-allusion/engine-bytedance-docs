---
title: "Troubleshooting performance abnormality during migration and synchronization"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_if_migration_or_synchronization_is_slow_"
---

When DTS encounters performance abnormality during migration and synchronization, you can troubleshoot step by step according to your scenario:


<Tabs>
<Tab zoneid="xTmZ2h1zHn" title="DTS experiences slow rate or stuck transmission during migration or synchronization">
<TabTitle>DTS experiences slow rate or stuck transmission during migration or synchronization</TabTitle>

For example, full migration speed is slower than expected, overall synchronization process is slow, or data transmission is stuck Possible cause and solution are as follows:


* **Reason one**: destination write bottleneck, detailed as follows

      * Write performance limit: target database insert performance reaches its limit and cannot handle source end data flow

      * Insufficient concurrency resources: target database max_connections or write concurrency reaches the limit, causing thread blocking

   **Solution**: adjust related parameters according to the following instructions

      * Adjust parameters: consider appropriately increasing concurrency\-related parameters on the target database (e.g., `max_connections` for MySQL or `max_worker_threads` for SQL Server)

      * Enable transaction merging: enable "transaction merging" in DTS task configuration to reduce interactions and improve throughput

      * Execute in off\-peak hours: perform migration or synchronization during business low\-peak periods to avoid resource contention.

* **Cause two**: table structure and index issues, detailed as follows:

      * Missing primary key/unique key: the source end table lacks a primary or unique key, forcing DTS to disable concurrent write and downgrade to serial processing.

      * Complex objects/version compatibility: presence of complex objects not yet supported by DTS (such as comments, custom types) or version incompatibility reduces parsing efficiency.

   **Solution**: adjust related parameters according to the following instructions

      * Complete primary key: check and complete the source end table’s primary or unique key before migration.

      * Temporary handling: for PostgreSQL and others, temporarily remove Comment annotations, then add them after migration; or use pg_dump offline migration for small data volumes.

* **Cause three**: task configuration and specification, detailed as follows:

      * Link specifications too low: the task’s link specifications are set to compact (suitable for small data volumes), limiting throughput capacity.

      * Improper preference configuration: MySQL migration preference set to space first, adopting low memory and low I/O strategies, sacrificing performance.

   **Solution**: adjust related parameters according to the following instructions

      * Upgrade specifications: upgrade the link specifications to Medium or higher. For detailed operations, refer to [Changing the migration task specification](https://docs.byteplus.com/en/docs/DTS/modifying_migration_task_specifications?lang=en) and [Changing the synchronization task specification](https://docs.byteplus.com/en/docs/DTS/modifying_synchronization_task_specifications?lang=en).

      * Adjust preferences: set preferences to performance first and ensure the target database reserves sufficient space (recommended ≥ 1.5 times the source database).


</Tab>
<Tab zoneid="NwJyYxJdWN" title="How to handle the data transmission stuck or failed after DTS completes the schema migration or schema initialization">
<TabTitle>How to handle the data transmission stuck or failed after DTS completes the schema migration or schema initialization</TabTitle>

For example, after schema migration completes, data migration cannot start or returns an error immediately. Possible cause and solution are as follows:

**Reason:**  foreign key constraint interference. The data table to be migrated contains foreign key constraints, resulting in restricted data write order or verification failed, which blocks transmission.

**Solution:**  you can solve the issue according to the following prompts:


* Delete the foreign key: manually delete the foreign key constraint on the destination, then retry the task (recommended, can be rebuilt if needed after migration completes).

* Complete migration: recreate the task, ensuring migrating both parent and child tables involved with foreign keys to the target database, maintaining referential integrity.


</Tab>
</Tabs>
