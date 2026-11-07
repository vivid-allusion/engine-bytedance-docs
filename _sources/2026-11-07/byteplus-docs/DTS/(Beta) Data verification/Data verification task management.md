---
title: "Data verification task management"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/viewing_data_validation"
---

This topic describes how to view and manage data verification tasks on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A data verification task has been configured. For more information, refer to [Configuring a data verification task](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation).

<span id=".5p-l55yL5pWw5o2u5qCh6aqM5Lu75Yqh"></span>
## View data verification tasks

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">It is recommended that you view the verification details after the <strong>Task status</strong> of the full data verification, full row verification, and schema verification tasks is <strong>Completed</strong>.</div>


* <div data-tips="true" data-tips-type="tip">For increment validation tasks, it is recommended that you view the verification details after the point in time when the incremental data changes.</div>


* <div data-tips="true" data-tips-type="tip">If the task progress of a full data verification task always displays 0% without any error information, you can hover the cursor over 0% of the task progress to check whether the task is in metadata chunks.</div>


* <div data-tips="true" data-tips-type="tip">If the related migration or synchronization task modifies the target instance, the original data verification task may fail due to the target instance not existing. When this occurs, it is recommended to create a data verification task again based on the current migration or synchronization task's latest configuration.</div>



<span id="4d01BPuU"></span>
### View data verification task details on the data verification list page


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left\-side navigation pane, click **Data verification**.

4. On the **Data validation list** page, view the information of all verification tasks, including **Verification task name/ID**, **Task status**, **Task progress**, **Task type**, **Task result**, **Associate migration/synchronization tasks**, **Source database**, **Target database**, **Start time**, and **End time**.

5. Click the target task name to view the following information:

   * Task information: On the **Task information** tab, you can view the **Basic configuration**, **Source database information**, **Target database information**, and **Billing information** of the verification task.

   * Task progress: On the **Task progress** tab, you can view the **State**, **Number of Notice**, **Number of errors**, **Number of source rows**, **Number of target rows**, **Number of inconsistent objects**, **Estimated total rows**, **Start time**, **End time**, and other information of the verification task. If there is inconsistent data, you can also download the inconsistent data on this tab.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The information in the task progress list varies depending on the task type. The actual page information shall prevail.      </div>
      

   * Monitor: Only increment validation tasks that are in progress support the display of monitoring information. On the **Monitor** tab, you can view the indicators within the specified time, including **Increment validation inconsistent number** and **Increment validation delay**. The details are as follows:

      * **Increment validation inconsistent number**: Indicates inconsistent rows between the two ends in the data with incremental changes from the start of the task to the present.

      * **Increment validation delay**: Indicates the time difference between the checked bit and the latest bit in the increment validation. The unit is minutes (min).

   * Task log: On the **Task log** tab, you can view the event name, start time, and event state of each event in the current verification task. If an event execution fails, **Task failed** is prompted. You can hover over the icon to view the task failed error message.

   * Health status: On the **Health status** tab, you can view the diagnostic report of the data verification task, including the basic information of the pre\-check and the pre\-check results. For more information about pre\-check, refer to [Pre-check (Data verification)](https://docs.byteplus.com/en/docs/DTS/beta-pre-check-items-data-verification). When the data verification task is blocked, you can perform a one\-click diagnosis on the health status of the current task, and then repair or adjust the relevant configurations based on the diagnosis results. For more information about one\-click diagnosis, refer to [One-click diagnosis](https://docs.byteplus.com/en/docs/DTS/One-click_diagnosis).


<span id="E9Kod23o"></span>
### Viewing data verification tasks in a DTS migration or synchronization instance


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration** or **Data synchronization**.

4. On the **Migration task list** or **Data synchronization list** page, click the target task name.

5. On the target task name page, click **Data verification**.

   * On the **Data validation list** sub\-tab, you can view all verification tasks associated with the current migration or synchronization task.

      
      |**Actions** |**Description** |
      |---|---|
      |**Viewing the data verification task list** |On the **Data validation list** sub\-tab, you can view the data verification task information, including **Task name/ID**, **Task status**, **Task progress**, **Task result**, **Task type**, **Billing method**, **Start time**, **End time**, **Actions**, and others. |
      |**View data verification task details** |On the **Data validation list** sub\-tab, click the target task name to view the details of the target task. |
      |**Download inconsistent data** |When the **Inconsistent** is displayed in the task result column, you can click **Download** in the Actions column to download the inconsistent data to your local device. |
      

   * On the **Diff management** sub\-tab, you can view Diff data, including **Structural Diff**, **Full Diff**, and **Increment Diff**.

      
      |**Actions** |**Description** |
      |---|---|
      |**View structural diff**<br><br> |On the **Structural Diff** sub\-tab, you can view **Structural Diff** information, including the **Source database**, **Target database**, **Object type**, **Source database object count ** , **Target database object count ** , **Number of inconsistent objects**, **Verification time ** , and **Actions**. |
      |**View full Diff** |On the **Full Diff** sub\-tab, you can view **Full Diff** information, including **Source database**/**table**, **Target database**/**table**, **Diff rows**, **Estimated total rows**, **Diff rate**, **Verification time**, and **Actions**. |
      |**View increment Diff** |On the **Increment Diff** sub\-tab, you can view **Increment Diff** information, including the **Source database**/**table**, **Target database**/**table**, **Diff rows**, and **Actions**. |
      |**View Diff data details** |On the **Full Diff** sub\-tab, click **View Diff** in the Actions column to view detailed Diff data in the **View Diff ** pop\-up window. |
      |**Download Diff data** |* Download Diff data in a single database/table. On the **Structural Diff**/**Full Diff**/**Increment Diff** sub\-tab, click **Download Diff** in the Actions column to download the Diff data in a database and table to the local device.<br><br>* Batch download Diff data in multiple databases/tables. On the **Structural Diff**/**Full Diff**/**Increment Diff** sub\-tab, select multiple Diff data, and then click **Batch download Diff** to download the Diff data in multiple databases and tables to the local device. |
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Increment validation tasks can display up to 10,000 rows of diff data. Other types of verification tasks support displaying a maximum of 100 rows of diff data.      </div>
      

<span id=".5LiL6L295pWw5o2u5qCh6aqM57uT5p6c"></span>
## Download data verification results

This topic describes how to download the data verification result, i.e., inconsistent data, in the Database Transmission Service (DTS) console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Incremental verification tasks support downloading only when they are in progress and inconsistent data exists. Other verification tasks support downloading only after the verification task has ended and inconsistent data exists.</div>


* <div data-tips="true" data-tips-type="tip">Before downloading the inconsistent data of increment validation, you must generate diff data and then download it. Otherwise, you will not be able to download inconsistent data.</div>


* <div data-tips="true" data-tips-type="tip">For verification tasks that are completed with consistent results, it indicates that there is no differing data between the source and target ends, thus no download is necessary.</div>



<span id="Ixzw8ggQ"></span>
### Download the verification result on the data verification task list page


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left\-side navigation pane, click **Data verification**.

4. On the **Data validation list** page, filter **Task result** as **Inconsistent**.

5. Download inconsistent data as needed.

   * Increment validation task

      1. Click **Download** in the **Actions** column.

      2. In the download Diff file pop\-up window, click the **Click to download ** link.

   * For other types of verification tasks, click **Download** in the **Actions** column of the target task.


<span id="5YiEn7oD"></span>
### Download data verification results in DTS migration or synchronization instances.


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration** or **Data synchronization**.

4. On the **Migration task list** or **Data synchronization list** page, click the target task name.

5. On the target task name page, click **Data verification**.

   
   |**Download method** |**Procedure** |
   |---|---|
   |**Download Diff data in the data validation list** |1. On the **Data validation list sub**\-tab, filter **Task result** as **inconsistent**.<br><br>2. Download inconsistent data as needed.<br><br>   * Increment validation task<br><br>      1. Click **Download** in the **Actions** column.<br><br>      2. In the download Diff file pop\-up window, click the **Click to download ** link.<br><br>   * For other types of verification tasks, click **Download** in the **Actions** column of the target task. |
   |**Download Diff data in the Diff management list** |On the **Diff management** sub\-tab, **download** the Diff **data** as required.<br><br><br>* Download Diff data in a single database/table. On the **Structural Diff**/**Full Diff**/**Increment Diff** sub\-tab, click **Download Diff** in the Actions column. In the **Download Diff** pop\-up window, click **One\-click download **  to download Diff data in a database and table to the local device.<br><br>* Batch download Diff data in multiple databases/tables. On the **Structural Diff**/**Full Diff**/**Increment Diff** sub\-tab, select multiple Diff data, and then click **Batch download Diff** to download the Diff data in multiple databases and tables to the local device. |
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Batch operations are supported when the status of the target task remains consistent and meets the terminate, pause, start, delete, and retry conditions.


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration** or **Data synchronization**.

4. On the **Migration task list** or **Data synchronization list** page, click the target task name.

5. On the target task name page, click **Data verification**.

6. On the **Data verification** tab, manage the verification tasks.

   
   |**Actions** |Limits |Procedure |
   |---|---|---|
   |**Modify verification task name** |The length of the task name must be within 256 characters. |1. Select the target **Verification task name/ID** column, then click the pen icon next to the task name.<br><br>2. Enter the task name in the pop\-up input box. The length must be within 256 characters. |
   |**Terminate a verification task** |* The verification task that is running, paused, and failed can be terminated.<br><br>* Task termination is irreversible. Proceed with caution. After termination, the state of the verification task changes to completed. |* Terminate the specified verification task<br><br>   1. Select **Actions** \> **More operations** \> **Terminate** in the target verification task column.<br><br>   2. In the **Terminate selected verification task?**  dialog box, click **Terminate**.<br><br>* Batch terminate verification tasks<br><br>   1. Select the verification tasks to be terminated, and click **Batch terminate** in the bottom menu bar.<br><br>   2. In the **Terminate task** dialog box, click **OK**. |
   |**Pause a data verification task** |* Only running verification tasks can be paused.<br><br>* Incremental tasks might not be recoverable after being paused. Other types of verification tasks that are paused for more than 7 days cannot be recovered. Proceed with caution. |* Pause the specified verification task<br><br>   1. Select the target verification task **Actions** column, click **More operations** \> **Pause**.<br><br>   2. In the **Pause selected verification task?**  dialog box, click **Pause**.<br><br>* Batch pause verification tasks<br><br>   1. Select the verification tasks to be paused, and click **Batch pause** in the bottom menu bar.<br><br>   2. In the **Suspend task** dialog box, click **OK**. |
   |**Start a data verification task** |Supports starting verification tasks whose status is **Paused** or ** To be started**. |1. Select the target verification task **Actions** column, click **More operations** \> **Start**.<br><br>2. In the **Start selected verification task? ** dialog box, click **Start**. |
   |**Delete a data verification task** |It can not be restored after deletion. Proceed with caution. |* Delete the specified verification task<br><br>   1. Select **Actions** \> **More operations** \> **Delete** for the target verification task.<br><br>   2. In the **Delete selected verification task?**  dialog box, click **Delete**.<br><br>* Batch delete verification tasks<br><br>   1. Select the verification tasks to delete, then choose **More operations** \> **Batch delete** in the bottom menu bar.<br><br>   2. In the **Delete task** dialog box, click **OK**. |
   |**Retry a data verification task** |Only **Failed** verification tasks can be retried. |* Retry the specified verification task<br><br>   1. Select the target verification task **Actions** column, click **More operations** \> **retry**.<br><br>   2. In the **Retry selected verification task?**  dialog box, click **Retry**.<br><br>* Batch retry verification tasks<br><br>   1. Select the verification tasks to be retried, and click **Batch retry ** in the bottom menu bar.<br><br>   2. In the **Retry task** dialog box, click **OK**. |
   


<span id=".5Y-C6ICD5YaF5a65"></span>
## Reference content

The following table describes the parameters in the schema verification result of MySQL:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Field differences at the <code>Error</code> level have a relatively significant impact. If present, they indicate discrepancies in the table structure.</div>


* <div data-tips="true" data-tips-type="tip">Field differences at the <code>Notice</code> level have minimal impact and, even if present, they will not cause discrepancies in the table structure. However, these diff data can still be viewed in the data verification report.</div>




|**Diff position** |**Verification item** |**Description** |**Verification level** |
|---|---|---|---|
|**Table** |Existence check |It checks whether the table structure exists at both the source and target ends. If it exists at only one end, an Error\-level prompt will be output. |Error |
||Engine |The storage engine name used by the table. |Error |
||Collation |Name of the default sort rule for the table. |Error |
||RowFormat |Storage format of the data. |Notice |
||Comment |Comments on the table. |Notice |
|**Constraint** |ReferencedSchema |Database name referenced by the foreign key. |Error |
||ReferencedTable |Table name referenced by the foreign key. |Error |
||ReferencedName |Column name referenced by the foreign key. |Error |
||UpdateRule |The `ON UPDATE` attribute value of the foreign key. |Error |
||DeleteRule |The `ON DELETE` attribute value of the foreign key. |Error |
||SeqInIndex |The position of the column in the index. |Error |
||Collation |The sorting method of the column in the index. The values are generally ascending, descending, or null. |Error |
||SubPart |Prefix length of a column participating in an index. |Error |
||Expression |The expression for a function index. For non\-function indexes, it is NULL. |Error |
||Name |Name of the foreign key or index. |Notice |
||ConstraintType |The constraint type. The values are as follows:<br><br><br>* `1`: Unique key.<br><br>* `2`: Non\-unique key.<br><br>* `3`: Foreign key. |Notice |
|**Column** |IsNull |Whether the column can be null. |Error |
||GenerateExpress |Expression of the generated column. |Error |
||Precision |The precision of the numeric column. |Error |
||Scale |Scale of the numeric column. |Error |
||DatetimePrecision |Precision of the time column. |Error |
||CharacterMaxLen |The maximum length of a string type column. |Error |
||Tp.Name |Name of the column type. |Error |
||Tp.IsUnsigned |Whether it is an unsigned integer. |Error |
||Position |The position of the column in the table. |Notice |
||DefaultValue |Default value for a column. |Notice |
||Comment |Comments on the column. |Notice |
||Extra |Additional information of the column. Typical values include `auto_increment`, `on update CURRENT_TIMESTAMP`, `STORED GENERATED`, `VIRTUAL GENERATED`, or `DEFAULT_GENERATED`. |Notice |
||CollationName |Sorting rules for a column. |Notice |
||CharSet |Character set of the column. |Notice |
