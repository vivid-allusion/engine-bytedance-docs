---
title: "Dynamic Probe"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Dynamic_Probe"
---

Dynamic Probe offers a global data perspective and refined sampling strategies to limit data within a specific scope, improving response speed.

Dynamic Probe explores sampled partial data, showing field details along with 0 values, null values, enumerated values, and other probe information. It supports filtering and group by operations to analyze data quality issues and displays statistical distribution results in real time.

<span id="_1-使用场景"></span>
## Usage Scenarios

The current main usage scenarios supported by Dynamic Probe are as follows:


* E\-commerce data contains a Json\-type field storing unique product attributes. During analysis, you can use Hive basic functions, such as get_json_object, to extract corresponding column data.

* If data development tracking shows user accounts that are non\-email accounts causing inaccurate final statistics, you can use the probe to identify data distribution and anomalies, then locate specific abnormal rows using the anomalies.


<span id="1273b783"></span>
## Constraints

After all activated services expire, all quality rules will be retained, but they will be disabled and cannot be used. After repurchasing the service, you must re\-enable the rule before it can be used.

<span id="_2-前提条件"></span>
## Prerequisites

Read permission on the data table is required to perform profiling. Refer to [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission) for instructions on applying for permissions.

<span id="_3-操作步骤"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Quality \> Profiling \> Dynamic Probe** to enter the dynamic profiling page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43ff1e4ba0dd4a8a9a8f9118596bc3d6~tplv-goo7wpa0wc-image.image) </span>

3. Set probe information.

   1. Select the probe object.

   2. Set probe metrics.

      The related parameters for dynamic probing are explained in the table below. Parameters marked with \* are required, while those without \* are optional.

   
   |Parameters |Description |
   |---|---|
   |**Select probe object** ||
   |\*Data source type |The datasource type of the probe object supports two categories: **Hive** and **other**, each with the following options selectable from the dropdown.<br><br><br>* Hive: **EMR Serverless Hive**<br><br>* Other: **ByteHouse Enterprise Edition (CE)** , **ByteHouse Cloud Data Warehouse Edition** |
   |\*Datasource/Engine |Select the data source/engine to use from the dropdown.<br><br><br>* When **data source type** is set to **EMR Serverless Hive**, the instance option defaults to **default**.<br><br>* When **data source type** is set to **ByteHouse Enterprise Edition (CE)** , select a running engine instance from the dropdown.<br><br>* When **data source type** is set to **ByteHouse Cloud Data Warehouse Edition**, select a running engine instance from the dropdown. |
   |\*DB name |The database name to probe; the dropdown lists created databases. |
   |\*Table name |The data table name to probe under the selected database; the dropdown lists created tables. |
   |Owner |The data table owner, displayed automatically after selecting the table name. |
   |\*Partition |The partition field of the data table, displayed automatically after selecting the table name.<br><br>The first\-level partition is required; do not use quotes around partition values. For example, you can enter date=20201016/hour=10/app=Data quality without using date='20201016'/hour='10'/app='Data quality'.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter only appears after selecting the table name when the table is a partition table.</div><br> |
   |**Probe Settings** ||
   |\*Sampling method |Provides three options: continuous sampling, filter sampling, and random sampling.<br><br><br>* continuous sampling: sample the first x data entries in the default order consecutively.<br><br>* filter sampling: filter using a where clause.<br><br>* random sampling: randomly select part of the data from the whole dataset. |
   |\*Sampling conditions |Filtering conditions for sampling. Filter using a where clause.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when <strong>sampling method</strong> selects <strong>filter sampling</strong>.</div><br> |
   |\*Number of samples |The number of samples must be a positive integer, with a maximum of 5000.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Probing will consume a certain amount of computing resources. If the number is large, the probe running time will be longer.</div><br> |
   |Probe field selection |Table fields to probe, selected by default. Edit via the **Detailed settings** button. |
   |\*Calculation group |Computing resource cluster in ByteHouse. Select the calculation group created in the **ByteHouse Cloud Data Warehouse Edition console** from the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Set this parameter when the <strong>Source type</strong> is <strong>ByteHouse Cloud Data Warehouse Edition</strong>.</div><br> |
   

4. Click the **Confirm** button to enter the sampling probe results page and view quick probe results for the sample count.

   The content includes the preview object, number of rows and columns, number of operation steps, and displays probe information and data lists.

   * Probe information: A summary of the statistics field probe information.

      * NULL value: The number and proportion of NULL occurrences in the field.

      * 0 value: The number and proportion of zero values in the field. Only **numerical** fields are supported.

      * Enumerated values: count the enumerated values in this field, sorted from smallest to largest. Click the **More** button to view all enumerated values, showing up to the first 100.

      * Numerical statistics: calculate quantiles, mean, standard deviation, and SUM for this field; NULL values are filtered out before calculation. Quantiles can be viewed as **10% \- 90% quantiles** or **25%/50%/75% quantiles**. Only **numerical** fields are supported.

   * Data list: display all explored data sets to quickly view detailed raw data.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/806ccb67c4f04093be0b95193d4ca72d~tplv-goo7wpa0wc-image.image) </span>

5. The following operations can also be performed on the probe results:

   * Data sampling

      Click the **Data sampling** button to edit probe information and perform new sampling on the object on the data sampling page.

   * Filter

      Click the **Filter** button, select fields and set filter rules on the filter page, then click the **Save** button to view the filtered profiling results in real time.

   * Group By

      Click the **Group By** button, select one or more grouping fields and their display methods on the Group By page, then click the **Save** button to display the count(\*) values for the selected fields in real time.

   * Column deletion

      Click the **Column deletion** button, select one or more columns to remove on the column deletion page, then click the **Delete** button to remove those columns’ display information in real time.

   * Column sorting

      Click the **Column sorting** button, select fields and set ascending or descending sorting rules on the column sorting page, then click the **Save** button to view the profiling results sorted by your rules in real time.

   * Operation steps

      Click the **Operation steps** button or visit the filtering, Group By, and other operation pages to view all actions performed on the current profiling results. You can also edit or delete corresponding operation steps. After editing or deleting, the calculation will be reprocessed according to the new logic.

   * Locate field

      In the dropdown list of the field name search box, select the field you want to view to quickly locate it.

   * View monitoring recommendations for the located field

      Click the displayed **monitoring recommendations** button to view the suggestions, then click the **configure monitoring** button to jump to the **Rules** page to set up monitoring information.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">This feature is supported only for Hive tables.      </div>
      

   * Collapse/expand profiling

      Click the **collapse/expand profiling** compound button to collapse or expand the profiling information in the upper part of the page.

   * Display profiling results in full screen

      Click the full\-screen icon button at the top right of the page to display the profiling results page in full screen.

      The parameters for the related operations are described in the following table.

   
   |Parameters |Description |
   |---|---|
   |**Filter** ||
   |Filter method |Currently, only **Filter template** option is supported.<br><br>You can set filter rules for all fields involved in operations so far. Multiple rules can be set, combined with **and**.<br><br>The following options are supported for filtering fields:<br><br><br>* ==<br><br>* !=<br><br>* \><br><br>* \>=<br><br>* <<br><br>* <=<br><br>* empty string<br><br>* non\-empty string<br><br>* IS NOT NULL<br><br>* IS NULL<br><br>* LIKE<br><br>* contain<br><br>* Not include |
   |**Group By** ||
   |Group By |Column fields to group by, selectable from the dropdown, supports multiple selections.<br><br>The options include all fields available from previous operations. |
   |Display method |Offers two options: newly generated table and as a new column.<br><br><br>* Newly generated table: Group By generates a new table and replaces the current table.<br><br>* As a new column: adds a column to the original table showing the count(\*) value for each group by field. |
   |**Column deletion** ||
   |Attribute |Column fields to delete, selectable from the dropdown, supports multiple selections.<br><br>The option range includes all fields available so far in the operation. |
   |**Column sorting** ||
   |Sorting rules |Select fields and set their ascending or descending sorting rules.<br><br>The option range includes all fields available so far in the operation. |
