---
title: "What are the possible causes of the task delay in data migration or synchronization task?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/what_are_the_possible_reasons_for_task_delays_during_data_migration_or_synchronization_tasks"
---

* **Possible reason 1**: The source database is processing large transactions. For example: When the source end is MySQL, if the source database writes a large transaction exceeding the `max_allowed_packet` parameter, DTS may get stuck pulling or parsing Binlog, causing migration or synchronization task delay. The upper limit of `max_allowed_packet` in the MySQL protocol is 1GB. DTS does not impose additional limits on this parameter, but it is recommended to reasonably control the size of a single transaction to avoid oversized transactions affecting task operation.

   **Solution**: You can temporarily remove tables, triggers, etc. that causes task delays from the task. After the task delay is reduced, add the paused tables, triggers, etc. back to the migration or synchronization task.

* **Possible reason 2**: Insufficient bandwidth.

   **Solution 2**: Adjust your bandwidth accordingly.

* **Possible reason 3**: The migration task or synchronization task is manually Paused, resulting in Data accumulation and high Data delay.

   **Solution 3**: Restart the task. For more information, refer to [Starting migration task o](https://docs.byteplus.com/en/docs/DTS/initiating_a_migration_task)r [Starting synchronization task.](https://docs.byteplus.com/en/docs/DTS/initiating_a_synchronization_task)

* **Possible reason 4**: The task's link specifications is set to **Compact**, which does not match your business volume, causing the delay to increase continuously.

   **Solution 4**: It is recommended that you switch the task's link specifications to **Standard**. For detailed operations, refer to [Changing the migration task specification](https://docs.byteplus.com/en/docs/DTS/modifying_migration_task_specifications) or [Changing the synchronization task specification](https://docs.byteplus.com/en/docs/DTS/modifying_synchronization_task_specifications).

* **Possible cause 5**: Incremental delay due to memory overflow in the destination database.

   **Solution 5**: You can first delete the delay table and then re\-add the delayed table.

* **Possible cause 6**: Because more data is added during the full migration or full initialization phase, the system will first catch up with the incremental data in this phase after the full migration or full initialization is complete, which will cause a large data delay.

   **Solution 6**: You can first delete the delay table and then re\-add the delayed table.

* **Possible cause 7**: There are many services on the destination instance, which leads to a high load on the destination instance.

   **Solution 7**: It is recommended that you pause other services first, and then start the normal operation of other services after the delay is reduced.

* **Possible cause 8**: The source table lacks a primary key, and a full\-table `DELETE` operation was executed. Because tables without a primary key generate a large volume of row\-based deletion records in the binary log (binlog) for each `deleted` row, this can significantly bloat the binlog and degrade synchronization performance.

   **Solution 8**: Terminate the `DELETE` operation on the source. DTS will stop receiving new `DELETE` events and gradually process the backlog of logs, allowing replication latency to return to normal over time. It is recommended to add primary keys to the source end tables after pausing the `delete` operation to prevent this issue from recurring.

* **Possible cause nine**: The source database executed DDL operations such as `RENAME TABLE`, which caused the DTS task to be blocked due to metadata lock (MDL) contention, resulting in replication latency or stalled progress.


**Solution** ** nine**:


   * Avoid performing DDL operations such as `RENAME TABLE` or `ALTER TABLE` during peak migration or synchronization periods.

   * If blocking has already occurred, you can temporarily terminate the DDL session and re\-execute it after DTS recovers.

   * It is recommended to perform schema changes in bulk during off\-peak business hours.

* **Possible reason 10**: Complex ETL rules are configured in the synchronization task.

   **solution 10**:

   * **Review existing rules**: check and Remove unnecessary ETL rules and simplify complex transformation logic.

   * **Monitor task indicators**: Use the DTS Console to monitor key indicators such as “synchronization delay,” “rows processed per second (TPS),” and “CPU utility” to confirm whether the delay is caused by ETL.

   * **Upgrade instance specification**: If the business must retain complex ETL rules, upgrading the DTS task instance specification is recommended to provide stronger computing power. For detailed operations, refer to [Changing the synchronization task specification](https://docs.byteplus.com/en/docs/DTS/modifying_synchronization_task_specifications).
