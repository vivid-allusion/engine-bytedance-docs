---
title: "Spatial analysis management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Space_analysis_management"
---

The Database Workshop (DBW) provides spatial analysis functionality, allowing you to visually view the space usage of an instance, such as table space usage.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An NDB for MySQL instance and account have been created, and the instance state is Running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (veDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control), and [Applying for operation permissions (veDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 2,000 table space data entries can be displayed.

* NDB for MySQL data originates from the following data sources

   * Community version: Data statistics are derived from the system database `information_schema.tables`.

   * Proprietary edition: Data statistics are derived from the system database `information_schema.ndb_capacity`.

* If HATP is enabled for the NDB for MySQL instance, only tablespace information for the OLTP tables of that instance is displayed.

* While using the spatial analysis feature, avoid modifying instance configurations, as this may prevent normal display of space usage.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **Space usage**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **veDB MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **Space usage ** tab, you can view the following information:

   
   <Tabs>
   <Tab zoneid="gqQLWFXjM9" title="View spatial profile">
   <TabTitle>View spatial profile</TabTitle>
   
   In the **Spatial profile** area, you can view the **Used space**, **Space usage**, and **Space size prediction after 7 days** for the current instance.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default"><strong>Space usage</strong> includes the occupied space for <strong>Data</strong> and <strong>Log</strong>. Here, <strong>Log</strong> includes <strong>Log</strong>, <strong>Binlog</strong>, <strong>RedoLog space usage</strong>, <strong>UndoLog space usage</strong>, <strong>System space usage</strong>, and <strong>Temporary space usage</strong>.</div>
   
   
   
   </Tab>
   <Tab zoneid="RkHlQossr9" title="Create space analysis task">
   <TabTitle>Create space analysis task</TabTitle>
   
   * Create space analysis task
   
      Click **Analyze now** and select the analysis scope in the dialog box:
   
      * Analyze all databases & tables: Select **All databases and tables** and click **OK**.
   
      * Specify databases & tables: Select **Specify databases & tables**, check the target databases and tables as needed, and click **OK**.
   
         * Specifying databases & tables does not apply to the proprietary edition space analysis for veDB. All database and table data is analyzed by default.
   
         * You can select multiple databases simultaneously for analysis. However, when multiple databases are selected, table filtering is not supported.
   
   * View space analysis results
   
      You can filter analysis tasks by generation time range. By default, tasks from the past day are displayed, with a maximum history of 30 days.
   
      * View task list: Displays an overview of all analysis tasks, including task type, target object, creation time, completion time, state, and error message.
   
      * View task details: In the task list, click **View details** in the **Actions** column of the target task to go to its space analysis page. Here, you can view the **Used space**, **Space usage**, and **Tablespace details** for the specified space. Tablespace details include the community version and proprietary edition, as shown below:
   
         * Community version: On the **Community version** tab, you can view information including the **database name**, **table name**, **storage engine**, **tablespace**, **tablespace ratio**, **data space**, **index space**, **fragmentation ratio**, **number of table rows**, **average number of rows**, and **auto\-increment ID value** for target tables on the business side within the instance, helping you analyze business data space usage and fragmentation. Some parameter descriptions are shown in the table below.
   
            
            |**Parameter** |**Description** |
            |---|---|
            |**Tablespace ratio** |Represents the proportion of a single tablespace to the total tablespaces, taken from `information_schema.tables`.<br><br>The calculation method is: Single table's (INDEX_LENGTH + DATA_LENGTH + DATA_FREE) / total tables' (INDEX_LENGTH + DATA_LENGTH + DATA_FREE). |
            |**Data space** |Taken from the `DATA_LENGTH `field in `information_schema.tables`. |
            |**Index space** |Taken from the `INDEX_LENGTH `field in `information_schema.tables`. |
            |**Fragmentation ratio** |Taken from `information_schema tables`.<br><br>The calculation method is: DATA_FREE / (INDEX_LENGTH + DATA_LENGTH + DATA_FREE). |
            |**Auto\-increment ID value.**  |Taken from the`AUTO_INCREMENT` field in `information_schema.tables`. |
            
   
         * Proprietary edition: On the **Proprietary edition** tab, you can view file information for system\-level tablespaces within the instance to help you analyze the space distribution of the underlying storage engine, specifically including **ID**, **name**, **used space**, **available space**, and **cold/hot**.
   
   
   </Tab>
   </Tabs>
