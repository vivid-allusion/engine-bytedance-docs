---
title: "Migration and synchronization data consistency troubleshooting guide"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/why_are_data_on_source_and_target_instances_inconsistent_during_migration_or_sync_tasks"
---

<span id="pufwtbLi"></span>
#### In data migration or synchronization tasks, if the data content between the source end and the destination is inconsistent, or the number of tables at the destination is less than the source end, it is usually caused by the following reasons. Troubleshoot according to the specific database type and symptoms:


<Tabs>
<Tab zoneid="qxk1jbFBRm" title="Type 1: Data content inconsistent">
<TabTitle>Type 1: Data content inconsistent</TabTitle>

* **Possible cause 1: MySQL ddl changes causing TIMESTAMP/DATETIME differences**


During MySQL migration or synchronization processes (except synchronization to Elasticsearch), if an alter table add column operation is executed on the source end, and the column uses automatic initialization and update mechanisms, it may lead to inconsistent data in that column between the two ends. For example:


   * The DDL add column statement simultaneously uses automatic initialization and updates TIMESTAMP.

      ```SQL
      ALTER TABLE test
      ADD COLUMN update_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;
      ```
      

   * The DDL add column statement simultaneously uses automatic initialization and updates DATETIME.

      ```SQL
      ALTER TABLE test 
      ADD COLUMN update_time DATETIME DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP;
      ```
      

      DTS may not fully replicate the internal automatic timestamp generation logic of the source database when handling such specific ddl changes, causing slight differences or different logic in the time values written to the destination.

* **Possible cause 2: MySQL JSON type large floating\-point precision loss**

   * **Cause analysis**: In MySQL type tasks, values in JSON fields do not match the source end. MySQL JSON type may lose data precision when storing large floating\-point numbers due to its precision handling, resulting in data differences after migration.

   * **Solution**: Before migration, convert large floating\-point numbers in source\-end JSON type to strings, then perform data migration or synchronization.

* **Possible cause three: data mistakenly deleted by MongoDB TTL index**

   * **Cause analysis**: In MongoDB full + incremental migration or synchronization, the destination data is less than the source or some data "disappears." Because MongoDB supports creating a TTL index, MongoDB will periodically and automatically delete expired documents through setting the `expireAfterSeconds` parameter. If this parameter is set too low (for example, less than the task's elapsed time), the data might be automatically cleared soon after writing to the destination.

   * **Solution**: Set the `expireAfterSeconds` parameter to more than 604800 seconds (7 days) to prevent accidental clearing during migration synchronization. For more information about TTL, refer to [Setting automatically deletion of time-sequence collections (TTL)](https://www.mongodb.com/zh-cn/docs/manual/core/timeseries/timeseries-automatic-removal/).

* **Possible cause four: temporary differences caused by incremental delay**

   * **Cause analysis**: data inconsistency found during verification. If the task is in incremental synchronization and has delay, new data from the source end has not been synchronized to the destination, causing differences during verification.

   * **Solution**: pause business write operations, wait for incremental synchronization to catch up (delay at 0), then create data verification task to confirm.


</Tab>
<Tab zoneid="K6pkiW2g8K" title="Type 2: Missing Object/Table count (schema difference)">
<TabTitle>Type 2: Missing Object/Table count (schema difference)</TabTitle>

* **Possible cause one: skipping due to existing object with the same name at the destination**

   * **Cause analysis**: after schema migration or initialization, some tables or views do not appear in the destination. During schema migration, if the target database already contains tables or views with the same name, DTS skips creating those objects to avoid overwriting data or errors.

   * **Solution**: ensure the target database is clean before schema migration, or manually remove old objects with the same name as the migration objects.

* **Possible cause two: inconsistency in instance parameter configuration causes table creation to fail**

   * **Cause analysis**: after migration, the number of tables at the destination is significantly less than at the source end. Inconsistent parameter configurations between source and destination database instances (for example, charset, SQL mode, storage engine restrictions) cause some tables to fail creating at the destination.

   * **Solution**:

      1. Check and modify Destination parameters to keep them consistent with the Source end. Refer to [Modify parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters) for how to set parameters for a RDS for MySQL instance.

      2. After modifying configuration, recreate the data transmission task.


</Tab>
</Tabs>
