---
title: "Viewing synchronization progress"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/viewing_synchronization_progress"
---

You can check the progress of schema synchronization, full synchronization, and incremental synchronization at any time during the execution of a data synchronization task. This topic describes how to view the data synchronization progress on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A synchronization task has been created and configured. In which,


* If you select **Unidirectional synchronization** when creating the task, you can only view the progress details of the forward synchronization task. For how to configure a synchronization task, refer to [Configuring forward synchronization](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).

* If you select **Bidirectional synchronization** when creating the task, you can view the progress details of the forward and reverse synchronization tasks separately. For how to configure a reverse task, refer to [Configuring reverse synchronization](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_migration_task).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data synchronization**.


4. On the synchronization task list page, find the target synchronization task. You can view the overall progress of the synchronization task or the progress of each synchronization type based on your business needs.

   * **Viewing overall synchronization progress**

      You can view the overall progress of the target synchronization task on the task list page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the figure below, the progress percentage of the full synchronization task is calculated as: Rows synchronized ÷ Total rows to be synchronized × 100%.      </div>
      

   * **View migration progress by type**

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you can not see the tab for a specific synchronization type, it may be because the type was not selected during synchronization task configuration, or the database being synchronized does not support that type.      </div>
      

      1. On the synchronization task list page, find the target unidirectional synchronization task, and select **More operations \> Task details** on the right of Task progress.

      2. On the data synchronization page, click the **Task progress** tab.

      3. Under the **Task progress** tab, click the tabs of different synchronization types to view the corresponding synchronization progress and execution status.

         
         |**Synchronization type** |**Supported operations** |**Precautions** |
         |---|---|---|
         |**Schema initialization** |* View information such as objects, state, source database, and target database of the schema initialization.<br><br>* Enter the name of the initialization object in the search bar at the top\-right corner to search for its initialization details.<br><br>* If a large amount of data needs to be initialized, you can quickly filter initialization objects in the list by ** Type** or **State** to check whether different types of initialization objects have completed initialization. |Schema initialization tasks end automatically. Do not manually end the task during schema initialization. |
         |**Full initialization** |* View the information such as object, state, rows initialized, average row size, estimated initialization data volume, elapsed time, and average initialization rate of full initialization.<br><br>* Enter the name of the initialization object in the search bar at the top\-right corner to search for its initialization details.<br><br>* If a large amount of data needs to be initialized, you can quickly filter the list by **State** to identify objects currently **Being initialized** and sort them by the **Estimated total rows**. |* When the **Instance type** of the source database is **RDS for MySQL**, **Document Database for MongoDB**, or **RDS for PostgreSQL**, average row size and estimated migration data volume are supported for viewing.<br><br>* When the **Instance type** is **Cache for Redis**, the volume of scanned data and the number of scanned instructions are supported for viewing.<br><br>* Full initialization tasks end automatically. Do not manually end the task during full initialization. |
         |**Incremental synchronization** |* Enter the name of the synchronization object in the search bar at the top\-right corner to search for its synchronization details.<br><br>* View the information such as object, source, target, synchronization status, rows synchronized, data volume of rows synchronized, delay, and average 5s RPS of incremental synchronization.<br><br>* If a large amount of data needs to be synchronized, you can sort the list by **Delay** to view details of synchronization objects with high delay.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Delay is the time difference between DTS reading the most recent data from the source and writing the most recent data to the target.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Synchronization tasks of the full\-incremental architecture do not support displaying delay information at the table level.</div><br> |* Incremental synchronization tasks do not stop automatically. After verifying all data has been synchronized to the target database, you can manually terminate the synchronization task. For the method to terminate the synchronization task, refer to [Terminating a synchronization task](https://docs.byteplus.com/en/docs/DTS/terminating_a_synchronization_task).<br><br>* When the data synchronization delay exceeds 5 seconds, click Enable isolation synchronization to split lagging tables into independent lanes for data synchronization. For details, refer to Configuring delayed synchronization. |
         


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DescribeTransmissionTaskProgress](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress) |Call the DescribeTransmissionTaskProgress API to query transmission task progress. |
