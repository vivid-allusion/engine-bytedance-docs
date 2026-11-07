---
title: "Full Probe"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Full_probe"
---

During data use, you can utilize the profiling feature to fully explore a data table and generate a profiling report with one click, displaying the statistical distribution of the explored columns. Profiling serves as the foundation of all data work, helping you understand the complete data, identify potential issues, and grasp data distribution for better data usage.

<span id="_1-前提条件"></span>
## Constraints

After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.

<span id="eb655671"></span>
## Prerequisites

Data table read permissions are required to perform profiling. For instructions on applying for permissions, see [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission).

<span id="_2-创建探查"></span>
## Create Profiling


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Profiling \> Create Probe** to open the create profiling page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecd2f05e9ef24d6fb06a6a28f29ef74e~tplv-goo7wpa0wc-image.image) </span>

3. Set profiling information.

   1. Select profiling target.

      Select the data source you want to profile, including engine, database, table, and partition information.

   2. Set profiling metrics.

   3. Set advanced parameters.

      The parameters for creating a profile are described in the following table. Parameters marked with \* in the name are required, while those without \* are optional.

   
   |Parameter |Description |
   |---|---|
   |**Select profiling object** ||
   |\*Data source type |The profiling object's data source type supports two categories: **Hive** and **other**, each containing the following options selectable from a dropdown.<br><br><br>* Hive: **EMR Serverless Hive**<br><br>* Other: **ByteHouse Enterprise Edition (CE)** , **ByteHouse Cloud Data Warehouse Edition** |
   |* Data sources / Engine |Select the data source/engine to use from the dropdown.<br><br><br>* When the **data source type** is **EMR Serverless Hive**, the instance option defaults to **default**.<br><br>* When the **Data source type** is **ByteHouse Enterprise Edition (CE)** , select a running engine instance from the dropdown.<br><br>* When selecting **data source type** as **ByteHouse Cloud Data Warehouse Edition**, you can choose a running engine instance from the dropdown. |
   |\*DB name |Name of the database to profile; you can select from databases already created in the dropdown. |
   |\*Table name |Name of the data table to profile within the selected database; you can select from tables already created in the dropdown. |
   |Owner |The owner of the data table, automatically displayed after selecting the table name. |
   |\*Partition to profile |Partition fields of the data table. The primary partition is required and can be set as follows:<br><br><br>* Input settings: no quotation marks are needed for partition values.<br><br>   For example, enter date=20201016/hour=10/app=Data quality without quotes like date='20201016'/hour='10'/app='Data quality'.<br><br>* Select the recommended partition expression from the dropdown list and edit it if needed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter appears only after selecting the table name for partition tables.</div><br> |
   |**Probe Settings** ||
   |Duplicate primary key |If probing is required, specify the primary key; multiple keys can be selected. |
   |Field Probe |Contains indicators such as null values, 0 values, numerical distribution, and enumerated values for each field. Changes can be made in **Detailed settings**. Unchecked probe items will not appear in the probe report.<br><br><br>* NULL value: By default, all fields are checked for NULL values.<br><br>* 0 value: By default, all numeric fields are checked for zero values.<br><br>* Enumerated values: By default, all fields are checked for enumerated values. Uncheck if not needed.<br><br>* Numerical distribution: By default, all numeric fields are checked for numerical distribution, including Min/Max/Mean/Sum/percentiles/standard deviation.<br><br>* Empty string: By default, all fields are checked for empty strings "", uncheck if not needed. |
   |\*Calculation group |The computing resource cluster in ByteHouse. Select a calculation group created in the **ByteHouse Cloud Data Warehouse Edition Console** from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only calculation groups with <strong>auto start/stop enabled</strong> or <strong>enabled status</strong> can be selected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Datasource type</strong> is set to <strong>ByteHouse Cloud Data Warehouse Edition</strong>, this parameter must be configured.</div><br> |
   |\*Queue |The rules use an operation queue and support two options: default queue or self\-specified queue.<br><br><br>* Use default queue: use the system's default engine queue without manual selection.<br><br>* Self\-specified queue: select the engine queue to use; the dropdown lists queues bound to the current project. If you have not applied for queues, please go to the corresponding console to apply.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Queues specified manually only show options that support batch task execution.</div><br> |
   |**Advanced parameter settings** ||
   |Description |Supports simple descriptions for profiling reports to help users understand the profiling information. |
   |Operation parameters |Supports setting advanced parameters to help control profiling operation status. |
   |Filter SQL |Supports input of conditional statements with syntax logic consistent with SQL, such as type='\*\*\*', without needing to input 'where'. |
   

4. Click the **Confirm** button to complete creation and enter the profiling results page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also create new profiling by clicking the <strong>New \> Create Probe</strong> button on the profiling results page.</div>


<span id="_3-创建定期探查"></span>
## Create Scheduled Profiles

For tables that require frequent data checks, configure scheduled profiling to automatically update profiling reports, reducing report waiting time.


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Profiling \> Create scheduled profile** to enter the scheduled profile creation page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1370e5a97a754d329042be1fed4f57de~tplv-goo7wpa0wc-image.image) </span>

3. After setting the probe information, click the **Confirm** button to complete the creation of the regular probe.

   The description of parameters for creating a regular probe is shown in the table below.

   
   |Parameters |Description |
   |---|---|
   |**Select probe object** ||
   |\*Source type |Source type of the probe object, supporting two categories: **Hive** and **other**, each containing the following options available from the dropdown.<br><br><br>* Hive: **EMR Serverless Hive**<br><br>* Other: **ByteHouse Enterprise Edition (CE)** , **ByteHouse Cloud Data Warehouse Edition** |
   |\*Datasource/engine |Select the datasource/engine to use from the dropdown.<br><br><br>* When the **Source type** is set to **EMR Serverless Hive**, the instance option defaults to **default**.<br><br>* When the **Source type** is set to **ByteHouse Enterprise Edition (CE)** , you can select a running engine instance from the dropdown.<br><br>* When the **Source type** is set to **ByteHouse Cloud Data Warehouse Edition**, you can select a running engine instance from the dropdown. |
   |\*DB name |The name of the database to profile; you can select an existing database from the dropdown. |
   |\*Table name |The name of the data table to profile within the selected database; you can select one or more existing tables from the dropdown. |
   |\*Partition |Partition fields of the data table automatically display after selecting the table name.<br><br>The first\-level partition is required and can be set as follows:<br><br><br>* Input settings: no need to use quotes for partition values.<br><br>   For example, you can enter date=20201016/hour=10/app=Data quality without using date='20201016'/hour='10'/app='Data quality'.<br><br>* Select a recommended partition expression from the dropdown list and edit as needed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting multiple table names, tables with the same partition name display in the same row for unified configuration.</div><br> |
   |**Probe Settings** ||
   |Duplicate primary key |If probing is required, specify the primary key(s); multiple can be selected. |
   |Field Probe |Includes metrics such as NULL values, 0 values, numerical distribution, and enumerated values for each field. Changes can be made in **Detailed settings**. Unchecked probe items will not show in the probe report.<br><br><br>* NULL values: by default, probe NULL values for all fields.<br><br>* 0 values: by default, probe 0 values for all numeric fields.<br><br>* Enumerated values: by default, probe enumerated values for all fields; uncheck if not needed.<br><br>* Numerical distribution: by default, probe numerical distribution for all numeric fields, including Min/Max/Mean/Sum/percentiles/standard deviation.<br><br>* Empty strings: by default, probe empty strings "" for all fields; uncheck if not needed.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default is to probe all fields; filtering fields is not supported.</div><br> |
   |\*calculation group |In ByteHouse, the computing resource cluster dropdown allows selection of computing groups already created in the **ByteHouse Cloud Data Warehouse Edition Console**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only calculation groups that <strong>have automatic start\-stop enabled</strong> or <strong>are currently enabled</strong> can be selected.</div><br><br><br>When **source type** is set to **ByteHouse Cloud Data Warehouse Edition**, this parameter must be configured. |
   |\*Queue |The rules use an operation queue and support two options: default queue or self\-specified queue.<br><br><br>* Use default queue: use the system's default engine queue without manual selection.<br><br>* Self\-specified queue: select the engine queue to use; the dropdown lists queues bound to the current project. If you have not applied for queues, please go to the corresponding console to apply.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Queues specified manually only show options that support batch task execution.</div><br> |
   |**Regular execution settings** ||
   |\*Running method |The execution method for regular probes only supports the **regular scheduling** option, which probes periodically according to the set schedule. |
   |\*Execution frequency |The execution frequency for regular probes only supports the **Daily** option. |
   |\*Execution time |The execution time for regular probes only supports setting the time to X o’clock Beijing time every day, with minute precision. |
   |**Advanced parameter** ||
   |Description |Supports simple descriptions for profile reports to help viewers understand the profiling information. |
   |Operation parameters |Supports setting advanced parameters to better control the profiling runtime. |
   |Filter SQL |Supports input of condition statements with syntax logic consistent with SQL, such as type='\*\*\*', without needing to enter 'where'. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only one regular probe can be configured per data table; multiple configurations are allowed, but each new configuration overwrites the previous one.</div>


* <div data-tips="true" data-tips-type="tip">You can also create new regular probes via the <strong>Create \> Create regular probes</strong> button on the profiling results page.</div>



<span id="_4-管理探查结果"></span>
## Manage Probe Results

After the data profiling is created successfully, you can view the profiling report, search profiling results, and check the run log. Follow these steps:


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Profiling \> Probe results** to enter the probe results page.

3. Select the desired engine and its instance from the source type and corresponding engine dropdown lists.

4. Click the collapse icon before the probe results list or the **Expand all** button to enlarge the list information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d94c66fbab04515980c7aaa5b99c517~tplv-goo7wpa0wc-image.image) </span>

5. You can perform the following actions:

   * Set search criteria to quickly find probe result entries that meet the conditions.

   * Manage regular probes

      * Click the **Edit Regular Probe** button in the **Action** column of a list entry to edit the regular probe information for that data.

      * After selecting one or more entries, click the **Close regular probes** button and confirm to close regular probes in bulk.

      * After selecting one or more entries, click the **Open regular probes** button and confirm to open regular probes in bulk.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can only perform the above management operations after creating regular probes for the related data.      </div>
      

   * Click the **Report** button in the **Action** column of a probe entry to open the probe report page and view profiling results.

      The content includes the row count, number of fields, table size, storage format, the probe description provided, and a summary of the field profiling information. Field details are as follows:

      * NULL value: Count and percentage of NULL occurrences in this field.

      * 0 value: Count and percentage of zero occurrences in this field. Only **numeric** fields are supported.

      * Enumerated values: count the enumerated values in this field, sorted by percentage from high to low. Click the **More** button to view all enumerated values, displaying up to the first 100.

      * Numerical statistics: calculate quantiles, mean, standard deviation, and SUM for this field, filtering out null values before calculation. Among them, quantiles can be selected to **view 10% \- 90% quantile** or **view 25%/50%/75% quantile**. Only **numerical** fields are supported.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59e4966e579845e689eb704c1f65e5b2~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can view the profile report only after the created data profiling runs successfully.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When the <strong>row count</strong> in the probe report is 0, no relevant data is available in the <strong>field details</strong>. It is recommended to reprobe or check the table data status.      </div>
      

   * Click the **Share** button in the **Action** column of an exploration item to copy and share the report link with others.

   * Click the **Copy** button in the **Action** column of an exploration item to copy and modify its exploration information, quickly creating a new exploration.

   * Click the  **...**   **\> Log** button in the **Action** column of an exploration item to view the run log of this exploration.

   * Click the  **...**   **\> Terminate** button in the **Action** column of a running exploration item to stop the profiling.

   * Click the  **...**   **\> Rerun** button in the **Action** column of a profiling record in the list to rerun the profiling task.
