---
title: "Why does the task progress remain unchanged for a long time during full migration or full initialization?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/why_is_there_no_progress_in_the_full_initialization_task_during_data_synchronization"
---

Issues of TS full migration or full initialization task progress remaining unchanged for a long time usually fall into three typical scenarios for troubleshooting and handling:


* **Scenario one: Why does the progress show 0% for a long time when the task just started?** 

   * **Cause analysis**: When the task just starts, DTS is scanning and initializing full data. At this time, the progress showing 0% is a normal phenomenon. Especially when the source database has many tables without primary keys or large tables, the elapsed time for data scanning and initialization is longer, causing the 0% state to last longer.

   * **Handling suggestions**:

      * If the task just started, it is recommended to wait a moment and observe the task status.

      * If large tables without primary keys exist in the source database, and business conditions allow it, it is recommended to add appropriate primary keys or unique indexes to these tables before executing the task. This not only improves the execution efficiency of the current task but also helps ensure the stability of subsequent synchronization.

* **Scenario two: Why does the full initialization phase have no progress for a long time?** 

   * **Cause analysis**:

      * Null primary key table: The table to be synchronized has no primary key. DTS needs to handle more complex data scanning and comparison logic, resulting in slower processing speed.

      * ETL configuration: The task has enabled ETL (data filtering and transformation) functions. Complex data processing logic increases additional computation elapsed time.

   * **Handling suggestions**:

      * Firstly, check if tables involved in synchronization in the source database lack primary keys. If so, it is recommended that you add a primary key to the table to be synchronized in the source database before performing synchronization.

      * If the task has enabled ETL configuration, check if related rules are overly complex and simplify filtering or transformation logic appropriately according to actual business needs.

* **Scenario 3: No incremental data on the source end, and the task progress is stuck at 99%?** 

   * **Cause analysis**: The DTS task progress panel shows data volume based on estimated values obtained from system tables (such as the TABLE_ROWS field in MySQL's information_schema.TABLES). Because the estimated value differs from the actual data volume to be processed, when the actual data volume exceeds the estimate, the progress may remain stuck at 99%.

   * **Handling suggestions**:

      * Enter the task's task progress tab to check if there are any objects yet to be migrated or initialized. For detailed operations, refer to [view task progress](https://docs.byteplus.com/en/docs/DTS/viewing_migration_progress?lang=zh) or [view synchronization progress](https://docs.byteplus.com/en/docs/DTS/viewing_synchronization_progress?lang=zh).

      * If there are still incomplete objects, wait for the task to continue processing to complete.
