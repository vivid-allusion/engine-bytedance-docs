---
title: "Viewing migration progress"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/viewing_migration_progress"
---

During the execution of a data migration task, you can view the detailed progress of schema migration, full migration, and incremental migration at any time. This topic describes how to view the data migration progress on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A migration task has been created and started. For instructions on how to create and start a migration task, refer to [Creating and starting a migration task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. On the **Migration task list** page, find the target migration task.

   You can view the overall progress of the migration task or the progress of each migration type based on your business needs.

   * **View overall migration progress**

      You can view the overall progress of the target migration task on the task list page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The full migration progress percentage in the figure below is calculated as: Rows migrated ÷ Total rows to be migrated × 100%.      </div>
      

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9aed4fd8a67617aa415ce3e4bfb5b322.png) </span>

   * **View migration progress by type**

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you can not see the tab for a specific migration type, it may be because the type was not selected during migration task configuration, or the database being migrated does not support that type.      </div>
      

      1. Click the task ID.

      2. On the data migration page, click the **Task progress** tab.

      3. Under the **Task progress** tab, click the tabs of different migration types to view the corresponding migration progress and execution status.

      
      |**Migration type** |**Supported operations** |**Precautions** |
      |---|---|---|
      |**User migration** |* View the user migration objects and whether the migration is complete.<br><br>* User migration includes migrating the account and its privileges.<br><br>* After migration is complete, click **DDL syntax** in the **Action** column on the right to view the object's creation syntax. |**User migration** type is supported only when the target database integrated mode is **Public network MySQL** or **BytePlus edition MySQL**. |
      |**Schema migration** |* View information such as objects, state, source database, and target database of the schema migration.<br><br>* Enter the name of the migration object in the search bar at the top\-right corner to search for its migration details.<br><br>* After the migration is complete, click **View creation syntax** in the **Actions** column on the right to view the creation syntax of the object.<br><br>* If a large amount of data needs to be migrated, you can quickly filter migration objects in the list by **Type** or **State** to check whether different types of migration objects have completed migration. |* Schema migration tasks end automatically. Do not manually end the task during schema migration.<br><br>* To ensure the performance of data migration and the stability of the migration task, some database migration objects will be created after the incremental migration is completed, which marks the entry into the **Post\-schema migration** phase. For more information, refer to [Post-schema migration](https://docs.byteplus.com/en/docs/DTS/glossary). |
      |**Full migration** |* View the information such as object, state, rows migrated, average row size, estimated migration data volume, elapsed time, and average migration rate of full migration.<br><br>* Enter the name of the migration object in the search bar at the top\-right corner of the page to search for its migration details.<br><br>* If a large amount of data needs to be migrated, you can quickly filter the list by **State** to identify objects currently being migrated and sort them by the **Estimated total number of rows**. |* When the **Instance type** of the source database is **RDS for MySQL**, **Document Database for MongoDB**, or **RDS for PostgreSQL**, average row size and estimated migration data volume are supported for viewing.<br><br>* When the **Instance type** is **Cache for Redis**, the volume of scanned data and the number of scanned instructions are supported for viewing.<br><br>* Full migration tasks end automatically. Do not manually end the task during full migration. |
      |**Incremental migration** |* Enter the name of the migration object in the search bar at the top\-right corner of the page to search for its migration details.<br><br>* View the information such as object, source, target, migration status, rows migrated, data volume of rows migrated, delay, and average 5s RPS of incremental migration.<br><br>* If a large amount of data needs to be migrated, you can sort the list by **Delay** to view details of migration objects with high delay.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Delay is the time difference between DTS reading the most recent data from the source and writing the most recent data to the target.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Migration tasks of the full\-incremental architecture do not support displaying delay information at the table level.</div><br> |* Only after the schema migration and full migration are completed can you find the data such as rows migrated, data volume of rows migrated, and delay.<br><br>* Incremental data migration tasks do not stop automatically. After verifying all data has been migrated to the target database, you can manually terminate the migration task. For termination methods, refer to [Terminating a migration task](https://docs.byteplus.com/en/docs/DTS/terminating_a_migration_task).<br><br>* When the data migration delay exceeds 5 seconds, click Enable isolation migration to split lagging tables into independent lanes for data migration. For details, refer to [Configuring delayed migration](https://docs.byteplus.com/en/docs/DTS/configuring_migration_delay_isolation). |
      


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DescribeTransmissionTaskProgress](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress) |Call the DescribeTransmissionTaskProgress API to query transmission task progress. |
