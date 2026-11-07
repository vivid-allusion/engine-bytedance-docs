---
title: "Modifying synchronization objects"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/managing_synchronization_objects"
---

DTS supports changing the synchronization objects in data synchronization tasks. This topic describes how to modify synchronization objects and view modified records in the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Synchronization tasks with a state of **In progress** or **Failed** and that have entered the incremental synchronization stage support modifying synchronization objects. For the method to create a synchronization task, refer to [Creating a synchronization task](https://docs.byteplus.com/en/docs/DTS/creating_and_initiating_a_synchronization_task).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only Redis, MySQL, PostgreSQL, and MongoDB synchronization tasks that are in progress and have entered the incremental synchronization stage support modifying synchronization objects.

* Newly added synchronization objects do not support modification of the synchronization type. For example, if the current task's **Synchronization type** does not have **Schema initialization** selected, you must ensure that the target schema objects already exist. Otherwise, it may affect the full/incremental synchronization of the newly added objects and cause the synchronization task to fail.

* If you select full synchronization when creating a data synchronization task, the newly added objects will first synchronize the full data to the destination before proceeding with subsequent incremental synchronization operations.

* When modifying synchronization objects, modifying the name of the synchronized databases and tables on the destination is not supported.

* Changing synchronization objects is not supported when you configure synchronization delay isolation. For more information about synchronization delay, refer to [Configuring synchronization delay isolation](https://docs.byteplus.com/en/docs/DTS/configuring_synchronization_delay_isolation).

* During object change, DDL operations are not allowed on the changed object. Otherwise, data change may fail.

* When adding synchronization objects in a bidirectional synchronization task, to avoid data inconsistency caused by repeated full data synchronization, and considering that most business scenarios involve adding databases or tables at the source end, the default strategy of DTS is as follows: the forward task defaults to full initialization plus incremental synchronization, while the reverse task defaults to incremental synchronization only. If your business scenario involves adding databases or tables at the destination, you need to first modify the reverse task by selecting full initialization plus incremental synchronization for the newly added databases or tables in the reverse task. Then, modify the forward task by selecting only incremental synchronization for the newly added databases or tables in the forward task.


<span id=".5Y-Y5pu05ZCM5q2l5a-56LGh"></span>
## Modify synchronization objects


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the synchronization task list page, find the target task, and click **Configure** on the right of the task progress.

5. On the **Configure synchronization objects** page, configure the following parameters.

   
   |<div style="text-align: center"><br>Parameter</div><br> ||Description |
   |---|---|---|
   |<div style="text-align: center"><br><strong>Conflict resolution strategy</strong></div><br> ||Select how to handle rows with the same primary key value already existing in the target database. The values are as follows:<br><br><br>* **Overwrite on conflict**: Use the source database data to overwrite the target database data. The synchronization task can be started normally.<br><br>* **Ignore on conflict**: During the pre\-check, rows with the same primary key value in the target database will be skipped, and the synchronization task can be started normally.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The abort on conflict strategy means if the task encounters existing rows with the same primary key or unique value in the target database during operation, the task reports an error and stops; the error message will include the conflicting data. This strategy currently belongs to an allowlist feature; to use it, please <a href="https://console.byteplus.com/workorder/create/">submit tickets</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you select the <strong>Conflict ignore</strong> handling method, data inconsistenties may occur, which may bring risks to the business. Choose with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If there are new synchronization objects, the conflict resolution strategy for primary key conflicts of the new objects is conflict overwrite before the incremental synchronization is started.</div><br> |
   |<div style="text-align: center"><br><strong>Synchronization object</strong></div><br> ||Select objects to be synchronized, such as tables, views, functions, or stored procedures. |
   |<div style="text-align: center"><br><strong>Advanced configuration</strong></div><br> |**Enable key filtering** |In a data synchronization task, if you only need to synchronize data that meets the conditions to the target database, you can achieve this by using the key filtering function.<br><br>Select whether to enable the key filtering function.<br><br><br>* **Yes**: Indicates that the key filtering function is enabled. After Key filtering is enabled, you must configure **Filter rules**.<br><br>   * **Allowlist**: If you select **Allowlist** for filtering **rule**, you must enter a regular expression. Indicates that the Keys matched by the regular expression will be synchronized to the Target.<br><br>   * **Blocklist**: If you select **Blocklist** for the filtering rule, you must enter a regular expression. Indicates that the Keys matched by the regular expression will be filtered out, that is, they will not be synchronized to the target. After Key filtering is enabled, to ensure the accuracy of the synchronized data, click **Online test**. On the **VolcDTSRedisKeyFilter** page, test whether the regular expression you entered completely meets your filtering requirements online. Based on the test results, you can confirm whether the regular expression has the correct syntax and whether it can meet the filtering requirements, so as to reduce the risk of data loss or synchronization errors during data synchronization.<br><br>* **No**: Indicates that the key filtering function is not enabled. |
   ||**Synchronization preferences** |Select a synchronization preference policy as needed. The following options are supported:<br><br><br>* **Performance first**: It can increase the speed of existing data synchronization but may also lead to higher disk fragmentation and increased system load. It is recommended to reserve an additional 50% of storage space on the target end. Performance first applies to scenarios with high requirements for existing data synchronization speed, such as financial transactions, fast data collection, and real\-time monitoring.<br><br>* **Space first**: The test space amplification rate is generally around 5%, which is suitable for scenarios with limited storage resources and relatively low requirements for data synchronization timeliness, such as data archiving, historical data backup, and log file synchronization. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When modifying PostgreSQL synchronization objects, there is no need to configure a conflict resolution strategy.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When modifying Redis synchronization objects, it is supported to configure whether to enable the Key filtering function.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When modifying MySQL synchronization objects, it is supported to configure <strong>Synchronize preference</strong>.   </div>
   

6. Click **Save task** at the bottom\-right corner of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the synchronization objects are modified, you can view the change log details on the console. For more information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/managing_synchronization_objects#.5p-l55yL5Y-Y5pu06K6w5b2V">Viewing change log</a>.   </div>
   

<span id=".5p-l55yL5Y-Y5pu06K6w5b2V"></span>
## View change log


1. Log in to the [DTS console](https://console.byteplus.com/dts).

2. In the upper\-left corner of the top menu bar, select the target region.

3. In the left navigation bar, click **Data synchronization**.

4. On the synchronization task list page, find the target unidirectional task, and click **More operations \> Task details** on the right of the task progress.

5. Click the **Synchronization object change records** tab.

6. In the change record table, you can view information such as the names, change actions, change time, and the state of the source and target database tables for the changed objects.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there are many change logs, you can filter the list by <strong>Modify actions</strong> and <strong>State</strong> to <strong>view</strong> them.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a synchronization object change is initiated, its status in the change log will be <strong>Waiting</strong>. You need to wait for the synchronization operation to complete before proceeding to the next step. Once the object change is successfully completed, the status will update to <strong>Succeeded</strong>.   </div>
