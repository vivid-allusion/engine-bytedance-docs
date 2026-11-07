---
title: "Configuring reverse synchronization"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/configuring_reverse_synchronization"
---

Database Transmission Service (DTS) provides various types of database synchronization services. This topic describes how to configure a reverse data synchronization task through Database Transmission Service (DTS).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A bidirectional data synchronization task has been created. For the method to create a synchronization task, refer to [Creating a synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task).

* The forward synchronization task has entered the **Incremental synchronization** stage, and the reverse synchronization task is **To be configured**. For more information about the synchronization topology, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The full initialization of reverse synchronization does not synchronize the databases and tables included in forward synchronization.

* When the forward synchronization task has not yet entered the incremental synchronization phase, configuring a reverse synchronization task will not support setting synchronization objects for the reverse task.

* If a data verification task is enabled in the synchronization task, the data verification task can be disabled by configuring the synchronization task before it starts. Once the built\-in data verification task is disabled, it will be removed from the data verification task list. After the synchronization task is started, the built\-in data verification task can not be disabled.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.


3. In the left navigation bar, click **Data synchronization**.


4. On the synchronization task list page, find the target reverse task, and click **Configure** on the right of the task progress.

5. On the **Configure synchronization objects** page, configure the following parameters.

   * When **Instance type** is **MySQL**, configure the following parameters:

   
   |Parameter |Description |
   |---|---|
   |**Initialization steps** |You can select **Schema initialization** or **Full initialization**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><strong>Incremental synchronization</strong> is selected by default and does not require selection. After the pre\-check is completed, DTS initializes the full data of the objects to be synchronized from the source instance into the target instance, serving as the foundation for subsequent incremental data synchronization.</div><br> |
   |**Primary key conflict handling** |Select the method for handling duplicate primary keys or unique values when they exist in the target database, with the following options:<br><br><br>* **Overwrite on conflict**: During task execution, if the target database contains the same primary key or unique value, DTS will not retain the conflicting data at the destination. Instead, the source data will overwrite the target data.<br><br>* **Abort on conflict**: During task execution, if the target database contains the same primary key or unique value, the task will report an error and stop running, with the error message indicating the conflicting data.<br><br>* **Ignore on conflict**: During task execution, if the target database contains the same primary key or unique value, DTS will retain the conflicting data at the destination, and the source data will not overwrite the target data.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When selecting <strong>Primary conflict resolution</strong> as <strong>Abort on conflict</strong>, the data handling method varies depending on the synchronization phase, as detailed below:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Full initialization stage: DTS does not retain conflicting data at the destination. That is, data from the source overwrites the target data.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">Incremental synchronization stage: DTS will handle data conflicts by aborting the process. The task will stop running, and error messages will indicate the conflicting data.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When a conflict overwrite occurs, if there is a table with the same name in the target database, it may cause data inconsistency issues or task failures as detailed below. It is recommended to use table name mapping or delete or rename the table with the same name in the target database to avoid data inconsistency and reduce business risks.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">When the table structure is consistent, data from full synchronization overwrites records in the target table with the same primary key or unique key values as in the source database.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">When the table structure is inconsistent, initialization of data may fail, and only partial column data can be synchronized or synchronization may fail.</div><br> |
   |**Synchronization starting point** |Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify GTID**: Enter the specified GTID in the input box, formatted as `source_id:transaction_id`.<br><br>* **Set GTID_EXECUTED**: ** ** Enter the specified GTID_EXECUTED in the input box, formatted as `source_id:transaction_id`. If multiple exist, separate them with commas (,).<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This step is not supported when <strong>Initialization step</strong> selects <strong>Full initialization</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">GTID and GTID_EXECUTED must be legal values from the source end. Otherwise, pre\-check reports an error.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When selecting <strong>Specify timestamp</strong>, the time you set must be later than the earliest Binlog time on the source end. If there is no corresponding time Binlog, the closest Binlog starting point will be selected.</div><br> |
   |**Synchronization object** |Select objects to be synchronized, such as tables, views, functions, or stored procedures.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">By default, a reverse synchronization task only synchronizes Delete, Insert, and Update operations and does not synchronize DDL operations.</div><br> |
   |**Error retry time** |If the source database or target database disconnects, the synchronization task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   

   * When **Instance type** is **Redis**, configure the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Initialization steps** |Indicates whether to select **Full initialization**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Incremental synchronization</strong> is selected by default and does not require selection.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the <strong>Synchronization topology</strong> is set to <strong>Bidirectional synchronization</strong> and <strong>Full initialization</strong> is selected for forward synchronization, reverse synchronization must wait until full initialization of forward synchronization is complete before starting.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After the pre\-check is completed, DTS initializes the full data of the objects to be synchronized from the source instance into the target instance, serving as the foundation for subsequent incremental data synchronization.</div><br> |
   |**Synchronization object** |Select the object to be synchronized. |
   |**Error retry time** |If the source database or target database disconnects, the synchronization task automatically recovers if reconnection occurs within that time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   

6. Click **Pre\-check**. You can perform the following operations based on the pre\-check result:

   * Click ** Details** in the **Actions ** column of the pre\-check results to view a detailed alarm or failure message. After modifying the databases and tables according to the alarm or failure message, click ** Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the synchronization task.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you choose to <strong>Ignore</strong> the alert and start the synchronization Task, it may cause data inconsistencies and business risks.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql">Pre\-check items</a>.   </div>
   

7. In the lower\-right corner of the page, click **Start task**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the task starts, you can return to the console and view the progress details of the synchronization task on the synchronization task list page. For more details, refer to <a href="https://docs.byteplus.com/en/docs/DTS/viewing_synchronization_progress">Viewing synchronization progress</a>.   </div>
