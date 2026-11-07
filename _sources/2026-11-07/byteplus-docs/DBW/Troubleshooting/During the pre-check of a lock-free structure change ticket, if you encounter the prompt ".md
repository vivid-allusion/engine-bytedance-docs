---
title: "During the pre-check of a lock-free structure change ticket, if you encounter the prompt \"Your lock-free change task has been detected, and there are potential risks during execution, such as data loss due to duplicate data,\" how should you handle it?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/during-the-pre-check-of-a-lock-free-structure-change-ticket-if-you-encounter-the-prompt-your-lock-"
---

Follow these steps:


1. On the Create data change ticket dashboard, click **Immediate processing** in the **Results details** column for **Online DDL add unique key**.

2. In the **Add index check** dialog box, select the **Task execution mode** with the following options:

   * **Lock\-free execution**: Uses an external tool to create a shadow table to simulate the change, offering high compatibility but consuming more resources. Ensure that the disk space is greater than or equal to the size of the current table. Suitable for scenarios with large tables exceeding 1 GB or 1 million rows.

   * **Native execution**: Directly executes the ALTER TABLE statement on the target table, offering higher efficiency but depending on the version. Suitable for MySQL 5.6 and later versions with smaller tables.


Execute the operation during off\-peak business hours to minimize potential impact on online services. For details about task execution modes, see [Introduction to execution plans](https://docs.byteplus.com/en/docs/DBW/during-the-pre-check-of-a-lock-free-structure-change-ticket-if-you-encounter-the-prompt-your-lock-?lang=zh#q1Zc0hEJ).

<span id="q1Zc0hEJ"></span>
## Introduction to execution plans

The system provides two execution plans when adding a unique index to a database table. Select the most suitable solution based on your table's data volume, peak business hours, and stability requirements. This section introduces the two execution methods and their differences to help you choose the appropriate solution.

<span id="I4F3P7XH"></span>
### Precautions

Regardless of the method chosen, ensure the following checks are completed before adding a unique index; otherwise, the task will fail:


1. Check for duplicate data: Unique indexes require field values to be unique. If duplicate data exists in the table, both methods will report errors or abort. Confirm no duplicate data exists by executing the following SQL statement in the target database instance in advance:


```SQL
SELECT target Column, COUNT(*) AS cnt 
FROM Your table name 
GROUP BY target Column 
HAVING cnt > 1;
```



2. Assess resources: When selecting the lock\-free execution (gh\-ost online change) method, ensure the remaining disk space is not less than the current table size.

3. Choose a time window: It is recommended to perform the operation during relatively low business hours to minimize potential impact on online services.


<span id="zO9BIGg8"></span>
### Solution overview


|**Dimension** |**Lock\-free execution (gh\-ost online change)**  |**Native execution (Online DDL)**  |
|---|---|---|
|**Applicable scenarios** |Large table changes (\> 1 million rows or \> 1 GB), during peak business hours, read/write operations cannot be blocked, and the change task needs to be paused or aborted at any time. |Small table changes (< 1 million rows and < 1GB), low business activity periods, fast completion required, limited disk space. |
|**Core principles** |gh\-ost is a triggerless online table structure change tool. This tool uses a shadow table mechanism to complete structural changes without affecting normal read/write operations on the original table. The specific steps are:<br><br><br>1. Create a shadow table: Create an empty table with the same structure in the same database and apply the target DDL, such as adding a unique index.<br><br>2. Full data migration: Copy the original table data to the shadow table in batches.<br><br>3. Incremental data synchronization: Simulate a MySQL replica to parse Binlog and synchronize changes from the original table to the shadow table in real time, ensuring eventual data consistency.<br><br>4. Atomic switch (Cut\-over): After the data is synchronized, swap the original table with the shadow table using a millisecond\-level RENAME TABLE operation.<br><br>5. Cleanup: Automatically delete or retain old tables. |Execute the ALTER TABLE statement directly on the original table.<br><br>The Online DDL mechanism (typically using the INPLACE algorithm) introduced in MySQL 5.6 and later builds indexes in\-place within the InnoDB engine. It records incremental changes via the Online log during execution and applies the changes with a brief table lock during the commit phase.<br><br> |
|**Advantages** |* Minimal business impact: The original table maintains normal read and write capabilities throughout the process, with no blocking of online DML operations.<br><br>* Pause and cancel: Supports pausing or canceling the task at any time during migration, with no negative impact on the original table.<br><br>* No trigger dependency: Unlike pt\-osc's trigger\-based mechanism, this solution avoids the performance overhead and lock contention risks associated with triggers.<br><br>* Comprehensive data validation: After migration completes, supports data consistency validation before the final cut\-over, ensuring accuracy before execution.<br><br>* Supports rate limiting control: Allows configuring migration speed to prevent excessive I/O and CPU pressure on the primary database. |* Minimal operation, zero additional dependencies: Complete the change by executing a single standard SQL statement without introducing any third\-party tools or setting up complex operational workflows.<br><br>* In\-place execution with high efficiency: Uses the INPLACE algorithm to build indexes in place, eliminating the need for full table data copying. Execution speed is typically much faster than online change tools like gh\-ost in common scenarios.<br><br>* Minimal disk overhead: No shadow tables are created. The incremental disk space usage is limited to the size of the new index itself, resulting in the highest resource utilization.<br><br>* Native atomic guarantee: Relies on MySQL's internal mechanisms to strictly ensure the atomicity of DDL operations. The operation either completes successfully or rolls back entirely, preventing any intermediate states.<br><br><br> |
|**Potential disadvantages** |* Performance bottleneck: Full table copy results in extremely long migration times for large tables.<br><br>* Space overhead: The shadow table mechanism doubles disk usage during the migration period.<br><br>* Data risk: If the original table contains duplicate data, migration may fail midway due to unique key conflicts.<br><br>* Dependency limitation: Strongly depends on the MySQL binlog_format=ROW configuration.<br><br>* Operational cost: Involves multi\-stage operations (create table/migration/parsing/switch table), making the process cumbersome. |* Non\-interruptible: Cannot be safely canceled midway; forced interruption may lead to prolonged rollback.<br><br>* Lock risk: MDL lock waits can easily block full table reads and writes, causing a surge in the number of connections.<br><br>* High risk for large tables: During an extended execution cycle, any anomaly may lead to failure and prolonged rollback.<br><br>* Low fault tolerance: Fails immediately upon encountering duplicate data, wasting all initial time investment.<br><br>* No rate limiting: Uncontrollable I/O overhead severely impacts online query performance. |


&nbsp;

<span id="tZFL39gr"></span>
### Comparison and selection recommendations for solutions


|**Dimension** |**Lock\-free execution (gh\-ost)**  |**Native execution (Online DDL)**  |
|---|---|---|
|**Execution method** |1. Create shadow table.<br><br>2. Migrate data.<br><br>3. Atomic switch. |Execute ALTER TABLE directly on the original table. |
|**Business impact** |Extremely small. Does not block read/write operations throughout the process. |Risk of MDL lock wait, may cause brief blocking. |
|**Execution speed** |Slow. Requires copying all data. |Faster. Build index in place. |
|**Disk overhead** |High. Requires approximately double the table space. |Low. Only requires space equal to the index size. |
|**Controllability** |Supports suspend, abort, and rate limiting. |Cannot be paused or rate limited. |
|**Recommended scenarios** |Large tables, peak business hours, high stability requirements. |Small tables, low business traffic periods, and pursuit of efficiency. |
