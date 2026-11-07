---
title: "Why is the target database disk usage or file size larger than the source end after executing DTS full migration or full initialization tasks?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/After_the_PostgreSQL_type_of_migration_task_is_complete"
---

Common reasons are: The following is a summary and corresponding solutions:


* **Reason 1: Massive accumulation of Binlog logs**

   * **Phenomenon description**: The target database's disk usage is much higher than the original instance.

   * **Cause analysis**: During full migration or initialization, the target database generates a large number of Binlog (binary log) files to record data changes for subsequent synchronization or recovery. These log files occupy significant disk space.

   * **Solution**:

      * It is recommended to modify the Binlog retention policy of the target database (such as shortening the retention period) before the task starts.

      * After the task completes, expired Binlog files can be manually cleaned up to free up space.

* **Reason 2: data fragmentation caused by concurrent writes**

   * **Symptom description**: after migration of databases like PostgreSQL, the <File size\> on the <Destination\> is larger than on the <Source end\>.

   * **Cause analysis**: dts typically uses concurrent <Execute\> of insert operations during the <Full data migration\> phase to improve efficiency. Such a high concurrency <Write mode\> easily causes the tables in the <Target database\> to generate a large amount of storage fragmentation, making the actual physical storage space more scattered and larger than the <Source database\>.

   * **Solution**:

      * After the <Task\> completes, execute commands to defragment the tables on the <Destination\>.

      * For PostgreSQL, you can use vacuum or vacuum full commands to reclaim space and defragment the <table structure\>.

* **Reason 3: redundant data caused by mistakenly using the standby database as the <Source end\>** 

   * **Symptom description**: duplicate and expanded <data\> appears on the <Destination\>, causing an <abnormal\> increase in size.

   * **Cause analysis**: if the standby database is mistakenly used as the <Source end\> in migration or <Synchronization\> <Task\>s:

      * When frequent data changes occur in the primary database, the long connection on the standby database may be disconnected.

      * After Database Transmission Service (DTS) reconnects with the standby database, tables without a primary key may undergo a full table scan again without deduplication, causing the same batch of data to be written repeatedly to the destination, leading to data expansion.

   * **Solution**:

   Strictly prohibit using the standby database as the source end. Always use the primary database or a read\-only instance (ensuring the read\-only instance has very low and stable delay) as the migration source end.
