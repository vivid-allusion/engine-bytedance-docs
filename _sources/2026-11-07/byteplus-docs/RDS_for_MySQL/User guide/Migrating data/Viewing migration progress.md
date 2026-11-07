---
title: "Viewing migration progress"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_migration_progress"
---

With RDS for MySQL, you can view schema migration, full migration, and incremental migration progress at any time during the execution process of a data migration task. This topic describes how to view the progress of data migration through the DTS console.

<span id="prerequisites"></span>
## Prerequisites

A migration task has been created and initiated. For the methods of creating and initiating the migration task, refer to [Creating and initiating a migration task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).

<span id="procedure"></span>
## Procedure


1. Log in to the [DTS console](https://console.byteplus.com/dts).

2. In the upper\-left corner of the top menu bar, select the target region.

3. On the **Migration task list** page, find the target migration task, and click **Task id**.

4. Click the **Task progress** tab.

5. Under the **Task progress** tab, click the tabs of different migration types to view the corresponding migration progress and execution status.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you cannot find the tab of a migration type, it may be because this type was not selected during the configuration of the migration task, or this type is not supported by the migrated database.   </div>
   

   * **Schema migration**

      You can do the following under the **Structural migration** tab:

      * View the information such as the object, status, source database, and destination database of schema migration.

      * In the search bar in the upper right corner of the page, enter the name of the migration object to search for the migration details of the target object.

      * In the **Action** column on the right side of the target object, click **View creation syntax**, to view the specific creation syntax of the object.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If there is a lot of data for migration, you can quickly filter out different types of migration objects to check whether the migration is completed according to "Type" or "Status" in the list.      </div>
      

   * **Full migration**

      You can do the following under the **Full migration** tab:

      * View the information such as object, status, number of rows migrated, time consumption, and average migration rate of full migration.

      * In the search bar in the upper right corner of the page, enter the name of the migration object to search for the migration details of the target object.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If there is a lot of data for migration, you can quickly filter out the objects in the process of migration from the list by "Status" and sort them according to "Migration percentage".      </div>
      

   * **Incremental migration**

      You can do the following under the **Incremental migration** tab:

      * In the search bar in the upper right corner of the page, enter the name of the migration object to search for the migration details of the target object.

      * View the information such as object, status, number of rows migrated, data volume of rows migrated, and delay of incremental migration.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">Note         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Only after the schema migration and full migration are completed can you find the data such as the number of rows migrated, data volume of rows migrated, and delay.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can sort by "Delay" in the list, to view the details of the migration objects with high delay.         </div>
