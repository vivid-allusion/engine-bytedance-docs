---
title: "Data correction management"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Data_correction_management"
---

When Diff data is verified in the data verification task, DTS supports generating SQL statements for correcting Diff data based on the source database or the target database. After you execute the corrected SQL statement in the corresponding database, you can correct the Diff data.

<span id="cEssPk7s"></span>
## Prerequisites

The data verification task has been configured, and Diff data has been verified. For how to configure the data verification task, refer to [Configure data validation](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation).

<span id="lYrXF7FW"></span>
## Precautions


* Currently, only full Diff and increment Diff verified in the MySQL data migration or data synchronization task can be corrected, and corrected SQL statements can be generated. Data correction is not supported for the verification task created before the Diff management function is released.

* For MySQL\-to\-MySQL single\-table data verification, DTS supports identifying up to 100,000 rows of differing data. If the number of differing rows exceeds 100,000, DTS will not perform data validation. The console page does not display Diff data; to view, you can download the data locally. For detailed operations, refer to [Download data verification results](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation?lang=en#.5LiL6L295pWw5o2u5qCh6aqM57uT5p6c). This feature is available on an allowlist basis. To use it, [Submit tickets](https://console.byteplus.com/workorder/create).

* In single full data verification tasks for other database types, each table can verify up to 100 lines of Diff data. When Diff data exceeds 100 lines, the Diff rows display 100+.

* In a single increment data verification task, a maximum of 10,000 Diff data can be verified for all tables.

* When the number of Diff lines is 100+, it indicates that the actual number of Diff lines in this table exceeds 100. Therefore, after the data correction is complete, it is recommended that you create a data verification job again and initiate verification, or if you estimate that there is a large amount of Diff data, you can resynchronize the data.

* The DELETE type Diff indicates that one end (source end or target end) has data while the other end (target end or source end) does not. For this type of Diff data, DTS generates a DELETE type SQL statement in data correction. Exercise caution when correcting DELETE type Diff.

* Currently, the correction policy of the corrected SQL is conflict overwrite, that is, according to the baseline for correction, the corrected SQL statement is generated, and after the corrected SQL statement is executed in the corresponding database, the Diff data can be executed.


<span id="SmCE4ene"></span>
## Data correction


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration** or **Data synchronization**.

4. On the **Migration task list** or **Data synchronization list** page, click the target task name.

5. On the target task name page, click **Data verification**.

6. On the **Data verification** tab, click **Diff**.

   Only the data of full Diff and increment Diff can be corrected.

   
   <Tabs>
   <Tab zoneid="F1ichNkIU4" title="Correct full Diff">
   <TabTitle>Correct full Diff</TabTitle>
   
   Supports individual or batch correction of full Diff data.
   
   
   1. On the **Diff management** tab, click **Full Diff**.
   
      * Batch correct Diff data.
   
         1. In the full Diff list, select one or more Diff records to be corrected.
   
         2. Below the list, click **Batch generation of corrected SQL**.
   
      * Correct individual Diff data.
   
         i. In the full Diff list, click **Generate corrected SQL** in the action column of the target Diff record.
   
   2. In the **Generate corrected SQL** dialog box, configure the following parameters.
   
      
      |**Name** |**Description** |
      |---|---|
      |**Select revised scope** |Confirm that the Diff records in the revised scope are the data to be corrected. In the **Select revised scope** area, single or batch remove Diff data that does not need to be corrected. |
      |**Correct DELETE type Diff?**  |The `DELETE` type Diff indicates that one end (source end or target end) has data while the other end (target end or source end) does not. For this type of Diff data, DTS generates a `DELETE` type SQL statement in data correction. Select whether to correct `DELETE` type Diff as needed.<br><br><br>* **Yes**: According to the baseline for correction, DTS generates SQL statements containing `DELETE` types for Diff data that exists on one end but not on the other.<br><br>* **No**: According to the baseline for correction, DTS automatically ignores Diff data that exists on one end but not on the other, and does not generate SQL statements containing the `DELETE` type. |
      |**Baseline for correction** |Select a baseline for correction as needed.<br><br><br>* **Source database**: With the source database as the baseline, correct the Diff data to keep the destination data consistent with the source database.<br><br>* **Target database**: With the target database as the baseline, correct the Diff data to keep the source database consistent with the target database. |
      
   
   3. Click **OK**.
   
   
   </Tab>
   <Tab zoneid="lrLMUZbcgk" title="Correct increment Diff">
   <TabTitle>Correct increment Diff</TabTitle>
   
   Supports single or batch correction of increment Diff data.
   
   
   1. On the **Diff management** tab, click **Increment Diff**.
   
      * Batch correct Diff data.
   
         1. In the increment Diff list, select one or more diff records to be corrected.
   
         2. Below the list, click **Batch generation of corrected SQL**.
   
      * Correct individual Diff data.
   
         i. In the increment Diff list, click **Generate corrected SQL** in the action column of the target Diff record.
   
   2. In the **Generate corrected SQL** dialog box, configure the following parameters.
   
      
      |**Name** |**Description** |
      |---|---|
      |**Select revised scope** |Confirm that the Diff records in the revised scope are the data to be corrected. In the **Select revised scope** area, single or batch remove Diff data that does not need to be corrected. |
      |**Correct DELETE type Diff?**  |The `DELETE` type Diff indicates that one end (source end or target end) has data while the other end (target end or source end) does not. For this type of Diff data, DTS generates a `DELETE` type SQL statement in data correction. Select whether to correct `DELETE` type Diff as needed.<br><br><br>* **Yes**: According to the baseline for correction, DTS generates SQL statements containing `DELETE` types for Diff data that exists on one end but not on the other.<br><br>* **No**: According to the baseline for correction, DTS automatically ignores Diff data that exists on one end but not on the other, and does not generate SQL statements containing the `DELETE` type. |
      |**Baseline for correction** |Select a baseline for correction as needed.<br><br><br>* **Source database**: With the source database as the baseline, correct the Diff data to keep the destination data consistent with the source database.<br><br>* **Target database**: With the target database as the baseline, correct the Diff data to keep the source database consistent with the target database. |
      
   
   3. Click **OK**.
   
   
   </Tab>
   </Tabs>
   

7. Subsequent operations.

8. After the data correction operation is complete, you can perform the following operations.

   
   |**Actions** |**Description** |
   |---|---|
   |**Download the corrected SQL** |After the data correction is complete, you can view the data correction event in the data correction tab, and download the corrected SQL file, and then execute the corrected SQL statement in the corresponding database. Refer to [View data correction event](https://docs.byteplus.com/en/docs/DTS/Data_correction_management#VnHR82zV) for more information. |
   |**Re\-create data verification task** |When the number of Diff lines is 100+, it indicates that the actual number of Diff lines in this table exceeds 100. Therefore, it is recommended that you re\-create the data verification task and initiate the verification after the data correction is complete. If there is a large amount of estimated Diff data and manual correction is time\-consuming, you can also choose to re\-synchronize the data. |
   


<span id="VnHR82zV"></span>
## View data correction event

The data correction list records all data correction events, including corrected SQL ID/Name, task status, corrected databases & tables, baseline for correction, initiation time, and generation time. You can view each correction event information, including the correction policy, and download the corrected SQL.


1. Log in to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration** or **Data synchronization**.

4. On the **Migration task list** or **Data synchronization list** page, click the target task name.

5. On the target task name page, click **Data verification**.

6. On the **Data verification** tab, click **Data correction**.

   In the data correction list, you can view the data correction event logs and the correction policy of each data correction event, and download the corrected SQL.

   
   |**Actions** |**Description** |
   |---|---|
   |View data correction list |In the data correction list, you can view the corrected SQL ID/Name, task status, corrected databases & tables, baseline for correction, initiation time, and generation time of each data correction event. You can search for target events by database/table name. |
   |View correction policy |In the action column of the target event, click **View correction policy** to view the data correction policy of the current event. |
   |Download the corrected SQL |In the action column of the target event, click **Download the corrected SQL** to save the corrected SQL file generated by the corrected data to the local device.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After you download the corrected SQL, if you confirm that the corrected SQL information is correct, you can execute the corrected SQL in the corresponding Database to correct the Diff data.</div><br> |
   


<span id="KPUN7Z3D"></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CreateValidationTask](https://docs.byteplus.com/en/docs/DTS/createvalidationtask) |Call the CreateValidationTask interface to create a data correction task. |
|[GetCorrectionResultDownloadLink](https://docs.byteplus.com/en/docs/DTS/GetCorrectionResultDownloadLink) |Call the GetCorrectionResultDownloadLink API to download data correction SQL. |


&nbsp;

<span id="ZQ9jk8YH"></span>
##
