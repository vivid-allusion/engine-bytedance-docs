---
title: "Data Comparison"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Data_comparison"
---

When data changes occur, such as modifying the data schema or changing the data source, compare the data before and after the changes. Quantitatively evaluate the differences between the two datasets and accurately assess the impact of the changes. This provides reference for the data owners to prevent data changes from affecting downstream data usage.

<span id="6f9292e2"></span>
## Constraints

After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.

<span id="b142e0fa"></span>
## **Create Comparison**

Steps to create a new data comparison are as follows:


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Comparison** to enter the data comparison page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9b6ddbb3d0943b288b3692a2ddff07b~tplv-goo7wpa0wc-image.image) </span>

3. Click the **Create Comparison** button to enter the create comparison page.

4. Set comparison information.

   1. Choose the comparison mode and set related parameters.

   2. Select the content to validate.

      1. specify the unique key for comparing the two data sets.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">If the unique key is duplicated, the validation report data may be unreliable. Please check the data quality of primary key uniqueness in advance.         </div>
         

      2. Select fields to validate and set their Diff logic.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">This setting only calculates data where the unique keys match in the two datasets. If the number of matches is 0, no calculation will be performed, and Diff details will not be shown in the report.         </div>
         

   3. Set operation parameters as needed.

5. Click the **Submit** button to complete creating the comparison.


The description of related parameters for creating data comparisons is shown in the table below. Parameters marked with \* before the name are required; those without \* are optional.


|Parameters |Description |
|---|---|
|\*Select the comparison mode |Provides two comparison mode options: table and SQL.<br><br><br>* Table: compares two persistent Hive tables A and B.<br><br>* SQL: compares two SQL\-generated virtual datasets that are not yet persisted in Hive tables.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The following situations are better suited for using SQL comparison mode:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to compare multiple date partitions, you can directly query the data under a specific date range in SQL, whereas Hive table comparison only allows selecting a fixed partition.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The compared data requires filtering, aggregation, Join, or other operations based on the original Hive table.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For data changes that involve altering the table structure (such as adding fields or changing field types), using SQL comparison is more convenient since you can compare data results before making changes.</div><br> |
|\*Engine |Engine instance to use, with only one option: **EMR_SERVERLESS_SPARK**.<br><br>When EMR_SERVERLESS_SPARK is selected, the instance defaults to **default**. |
|**Table mode** ||
|\*DB name |Select the database name to compare under the selected engine. Choose from the dropdown of created databases. |
|\*Table name |Select the table name to compare under the selected database. Choose from the dropdown of created tables. |
|Owner |The owner of the data table, automatically displayed after selecting the table name. |
|\*Partition |The partition field of the data table, automatically displayed after selecting the table name and editable as needed.<br><br>No quotation marks needed for partition values. For example, enter date=20201016/hour=10/app=Data quality without quotation marks around date='20201016'/hour='10'/app='Data quality'.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter only appears after selecting the table name when the table is a partition table.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When multiple partitions exist, at least one partition name must be selected, and the corresponding partition expression cannot be empty.</div><br> |
|Filter SQL |Add filter conditions as needed.<br><br>Supports conditional statements with syntax logic consistent with SQL, such as dau\>1000 and type in (a,b), without entering where. |
|\*Primary key |Used for matching two tables. By default, primary key information for comparison is obtained from the data catalog but can be modified.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure the unique key has no duplicate values; otherwise, the comparison results will be affected.</div><br> |
|\*Attribute |Validation fields corresponding to the two tables, auto\-filled; fields in Table B can be edited. |
|\*Diff logic |Diff logic supports the following two calculation methods; at least one must be selected when setting.<br><br><br>* Equivalent matching: the percentage of rows where the values differ between the old and new fields, relative to the total rows in the old table; the smaller the percentage, the smaller the Diff. Calculation method: count(A!=B)/count(A)<br><br>* Absolute difference: the sum of absolute differences between old and new field values as a percentage of the sum of the old field values; the smaller the percentage, the smaller the Diff. Calculation method: SUM(\|A\-B\|)/SUM(A) |
|Whether to check Diff details |You can choose whether to check Diff details.<br><br>When checked, if Diff appears in this field, the system will provide Diff data details.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This query consumes additional computing resources; select only important fields.</div><br> |
|**SQL mode** ||
|SQL alias |Manually set SQL aliases for the two tables for quicker understanding and comparison of reports. |
|\*SQL statement |Use SQL statements to compare data between two tables, input manually as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Data comparison does not support <strong>Array</strong>, <strong>Map</strong>, or <strong>Struct</strong> type fields. Configuring these fields may cause execution failure.</div><br> |
|\*Comparison field |Automatically filled after parsing the input SQL statement, editable as needed.<br><br>See "table mode" for related parameter descriptions. |
|**Operation settings** ||
|\*Running method |The execution method for data comparison supports **Execute immediately**, **Regular scheduling**, and **Associated** **task**.<br><br><br>* Execute immediately: start immediately after submission; execute only once.<br><br>* Regular scheduling: execute repeatedly based on the set time.<br><br>* Associated task: execute according to the associated task’s schedule. |
|\*Execution frequency |The execution frequency for data comparison supports only per day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>running method</strong> is set to <strong>Regular scheduling</strong>.</div><br> |
|\*Execution date |The execution time for data comparison supports only a specific time point **every day (Beijing time)** , which can be set freely.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>running method</strong> is set to <strong>Regular scheduling</strong>.</div><br> |
|\*Task name |The name of the related task can be searched and selected by the task name keyword or ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>running method</strong> is set to <strong>Associated task</strong>.</div><br> |
|\*Queue |The rules use an operation queue and support two options: default queue or self\-specified queue.<br><br><br>* Use default queue: use the system's default engine queue without manual selection.<br><br>* Self\-specified queue: select the engine queue to use; the dropdown lists queues bound to the current project. If you have not applied for queues, please go to the corresponding console to apply.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Queues specified manually only show options that support batch task execution.</div><br> |
|Operation parameters |Operation parameters before the SQL statement, such as “set parameter name 1=value;”, configure as needed. |
|**Alarm configuration** (optional to enable alarm configuration; if enabled, the following parameters must be set.) ||
|\*Alarm conditions |You can add alarm items via the **Add another attribute** button, each including a field name and alarm condition.<br><br><br>* Field name: select from the dropdown fields in the data table for comparison.<br><br>* Alarm conditions: each field’s alarm condition supports two options: **Equivalent matching rows** and **Equivalent mismatch rows**. Multiple conditions can be set. The default relationship between multiple alarm conditions is **and**, which can be changed to **or**. |
|\*alarm channel |Only the **Email + Site message** alarm method is supported. |
|\*Receivers |Users who receive alarm messages.<br><br><br>* User: after entering the user account keyword, select from the dropdown list. Multiple users can be set. |


<span id="_2-管理对比结果"></span>
## **Manage Comparison Results**

After successfully creating a data comparison, you can view the comparison report, search the comparison results, and check the run log. Follow these steps:


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Data comparison \> Comparison results** to enter the comparison results page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9b6ddbb3d0943b288b3692a2ddff07b~tplv-goo7wpa0wc-image.image) </span>

3. In the **Engine** dropdown menu, select the engine and corresponding instance you want to view.

4. You can perform the following actions:

   * Set search criteria to quickly find comparison results that meet the conditions.

   * Click the **Comparison Report** button in the **Action** column of any item in the comparison results list to enter the comparison report page, where you can view the overall comparison overview and Diff details list.

      * The calculation logic for each metric in the comparison overview is as follows:

         * Row count of table A/B: select count(\*) from table_A/B

         * Row difference percentage: |Row count of data B \- Row count of data A| / Row count of data A

         * Total rows matched by primary key: select count(\*) from table_A inner join table_B on unique_key_A = unique_key_B

         * Proportion of matched rows in table A/B: (Total rows matched by primary key) / (Row count of table A/B)

      * Diff details list: the meanings of each field are as follows:

         * Field name (A/B): used to verify whether the selected fields are correct.

         * Field type (A/B): used to compare field type differences.

         * Diff logic: if the Diff value is 0, it means the two tables are completely identical; if a Diff exists, evaluation can be done based on the values of **Diff logic: Diff value** and **Ratio of the difference (%)** .

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can view the comparison report only after the data comparison runs successfully.      </div>
      

   * Click the **Log** button in the **Action** column of an item in the list to view the run log for that comparison.

   * Click the **Terminate** button in the **Action** column of a running item in the list to terminate that comparison.

   * Click the  **...**   **\> Copy** button in the **Action** column of an item in the list to copy the comparison information to create a new comparison.

   * Click the  **...**   **\> Rerun** button in the **Action** column of an item in the list to allow re\-executing the verification task after confirmation.

   * Click the  **...**   **\> Share** button in the **Action** column of an item in the list to copy the report link for sharing.

   * Click the  **...**   **\> View SQL** button in the **Action** column of an item in the list to display the SQL statement for the data comparison information.


<span id="_3-管理定时对比任务"></span>
## Manage Timing Comparison Tasks

If the new comparison uses scheduled execution, a timing comparison task will be created. You can manage it through this feature by following these steps:


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Comparison \> Timing comparison** to enter the timing comparison page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/664def2b8b284224b142300c568bea91~tplv-goo7wpa0wc-image.image) </span>

3. In the **engine** dropdown list, select the engine and instance you want to view.

4. You can perform the following operations:

   * Set search criteria to quickly find timing comparison task lists that meet the conditions.

   * Click the **Edit** button in the **Action** column of a list item to modify that comparison information.

   * Click the **On/off** toggle in the **Action** column of a list item to enable or disable the timing comparison. The comparison only runs on schedule after being enabled.

   * Click the **Delete** button in the **Action** column of an item in the list. After the second confirmation, you can delete the scheduled comparison task.

   * Select one or more items, then click the batch operation button below the list to perform the corresponding batch operation.
