---
title: "What causes a task to fail during execution?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/what_are_the_reasons_for_task_execution_failures_during_the_task_execution_process"
---

The following are possible reasons for task failure:


* **Source and target environment compatibility issues**

   * **Possible cause 1: Version incompatibility**

   In synchronization or migration tasks, the source and target database versions are inconsistent, or the target version is lower than the source version. For example, in a migration task, the source end MySQL version is 8.0, and the destination end MySQL version is 5.7. Because MySQL version 5.7 does not support the execution of the `ALGORITHM=INSTANT` statement, the migration task fails.

   **Solution**: It is recommended to keep the source and target database versions consistent, or ensure that the target version is higher than the source version.

   * **Possible cause 2: Index length exceeds the allowed limit**

   During MySQL data migration or synchronization, the task may fail if the index length exceeds MySQL's maximum allowed limit.

   **Solution**: You can resolve the issue of index length exceeding the limit by adjusting the row format (e.g., `ROW_FORMAT=DYNAMIC`), using prefix (partial) indexes, changing the character set, applying index compression, or redesigning the table schema. At the same time, when creating a task, ignore the pre\-check item of the warning type.

   * **Possible cause 3: Inconsistent configuration of the parameter ** **`max_allowed_packet`**

    For example, if the source is set to 2G and the target to 1G for max_allowed_packet, large transactions during synchronization may produce packets that exceed the target’s limit. The target will reject these oversized packets, leading to task failure.

   **Solution**: It is recommended to configure the `max_allowed_packet` parameter identically on both the source and target instances, using a sufficiently large value to accommodate large transactions.

   * **Possible cause 4: MongoDB index exceeds length limit**

      DTS migration or Synchronization task failed due to index length exceeding the limit

      * **Solution**:

         * Set the `failIndexKeyTooLong` parameter to `false` at the destination end.

         * Delete the oversized index at the source end, or change the oversized index to a hash index or text index.

* **Permission and security configuration issue**

   * **Possible cause 4: Insufficient database account privileges**

   The database account on the target side lacks the necessary privileges for the required operations.

   **Solution:**  The database accounts on both the source and target sides must be granted the necessary permission policies. For related permission policy information, refer to the specific documents in [](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions)[](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions) and [Overview of synchronization solutions](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

   * **Possible cause 5: Missing ** **`PSYNC`** ** permission in Redis**

   During Redis data migration or synchronization, the source database account lacks the `PSYNC` permission.

   **Solution**: You need to [submit tickets](https://console.byteplus.com/workorder/create/) to contact the technical staff and add `PSYNC` permission to the source database account before performing data migration or synchronization.

   * **Possible reason 6: Allowlist disassociated**

   During data transmission, the whitelist associated with the source or target instance was unbound or removed. When creating a data transmission task, the target instance automatically associate a allowlist, and the CIDR blocks used by the DTS service are added to this allowlist. If the allowlist associate to the source or target instance is disassociate or deleted, it will result in connection failures to the source or target database and cause the task to be interrupted.

* **Network and instance availability issues**

   * **Possible reason 7: IP address changes**

   When the source or target is a self\-managed database exposed over the public network or deployed in a VPC, any change to the IP address of the source or target during task execution will cause the task to fail.

   **Solution**: Do not modify the IP address of the source or target during task execution.

   * **Possible reason 8: Source or target instance downtime**

   Possible cause 6: The source or target instance downtime, causing the task to fail.

   **Solution**: You can delete the data already migrated or synchronized to the target database and then re\-create the task.

* **Binlog and log availability causes**

   * **Possible cause 9: Source end Binlog unavailable**

      Including: Manually deleted Binlog files, Task paused beyond retention period (e.g., more than 7 days), binlog automatically deleted, Binlog retention time (`expire_logs_days`) set too short.

   **Solution**: You can resolve it by following methods:

      * Retain binlogs for a sufficiently long period (recommended ≥ 7 days).

      * Avoid pausing the task for extended periods (recommended ≤ 24 hours).

      * If binlogs have already been lost, you can restore them from a backup or re\-create the migration/synchronization task.

* **Target database status abnormal issues**

   * **Possible cause 10: Manual modifications made to the target database while the task is running**

   Making arbitrary modifications to the target database resources during task execution.

   For example, during a synchronization task, if a DDL operation such as `DROP TABLE` is executed on the target database, the synchronized table may no longer exist when subsequent data changes are applied. This causes the task to fail due to missing objects.

   **Solution**: Do not perform any unauthorized operations on the target database during task execution. You can view the action records in database audit of Database Workshop (DBW) to locate and analyze problems. For more information, see [Database audit management](https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-mysql).

   * **Possible cause 11: The target database already contains an object with the same name, and the conflict resolution policy is set to error.** 

   When creating a data synchronization task, the task may fail because the target database already has a database or table with the same name to be migrated, and the task's **conflict resolution strategy** is set to **abort on conflict**.

   **Solution**: You can change the task's **conflict resolution strategy** to **ignore on conflict**.

* **Task configuration error**

   * **Possible cause 12**: Structure migration not selected

   When creating a data migration or data synchronization task, if the **Migration type** or **Synchronization type** does not select **Schema migration** or **Schema initialization**, it causes inconsistent table structures between the source end and the target database.

   **Solution**: Create a table with the same structure in the target database or re\-create a transmission task selecting migration type or synchronization type as schema migration or schema initialization.

   * **Possible cause 13**: Insufficient storage/Binlog space

   Due to insufficient storage space at the target end, a large number of Binlog files are generated in the target database during full migration or full initialization, causing the task to fail.

   **Solution**: It is recommended to modify the retention policy of the target database Binlog before full migration or full initialization.
