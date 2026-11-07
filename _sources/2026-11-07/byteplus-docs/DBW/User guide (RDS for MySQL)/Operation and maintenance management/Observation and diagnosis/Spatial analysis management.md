---
title: "Spatial analysis management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/spatial-analysis-management-for-mysql"
---

The Database Workshop (DBW) provides spatial analysis functionality, allowing you to visually view the space usage of an instance, such as table space usage.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The tablespace data is calculated based on the system database `information_schema.tables` and may be slightly inaccurate. Please refer to the actual values for confirmation.

* Instance\-level analysis limit: Space usage is analyzed for up to the first 20,000 tables per database instance.

* Database\-level analysis limit: For a single database (DB), tablespace usage is analyzed for up to 2,000 tables within it.

* While using the spatial analysis feature, avoid modifying instance configurations, as this may prevent normal display of space usage.


<span id=".5pON5L2c5q2l6aqk"></span>
## Advantages

Space analysis can transform complex storage issues into intuitive data views, helping to shift from reactive emergency handling to proactive management.


* Global visualization: Charts display key metrics such as used space, space distribution (e.g., data, binlog, undo log), and estimated days of remaining available storage, enabling a comprehensive, at\-a\-glance view of storage status.

* Strong alerting capability: Automatically estimates the number of days until storage is exhausted, proactively identifying potential risks—such as an impending disk full condition—to prevent service disruption.

* Deep table\-level space insights: Enables viewing key metrics for each table—including tablespace size, fragmentation ratio, and row count—to accurately identify large tables or those with high fragmentation.

* Historical trend tracking: Provides space usage trend charts to help analyze growth patterns and forecast future capacity requirements.

* Multi\-dimensional breakdown: Categorizes and analyzes storage usage across user data, system space, log files (e.g., binlog, undo log), and temporary files to help identify the sources of resource consumption.


<span id="RdxUBI88"></span>
## Applicable scenarios


* Storage scaling assessment: Review current space usage and estimated days of remaining capacity to determine whether immediate scaling is required; combine this with trend charts to forecast future growth.

* Performance optimization diagnostics: Analyze tables with high fragmentation and execute `ALTER TABLE ...` `ENGINE=InnoDB` or perform a table rebuild to reduce fragmentation and enhance query performance.

* Log management optimization: Review the storage占比 of Binlog and Redo Log; if their proportion is excessively high, consider adjusting retention policies—for example, by setting `expire_logs_days`.

* Large table identification and archiving: Sort tables by tablespace size to identify those consuming the most storage, and evaluate whether sharding, partitioning, or archiving historical data is necessary.

* Capacity planning and budget control: Leverage space usage trends and consumption statistics to provide data\-driven support for resource procurement and budget allocation.

* Troubleshooting assistance: When encountering disk read\-only or write failures, quickly determine whether the issue is caused by data bloat or log accumulation.


<span id="lY0W4Pes"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the **Observation and diagnosis** page, click **Space usage**.

5. In the upper left corner of the **Space usage** tab, switch the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you access the <strong>Space usage</strong> tab through <strong>Observation and diagnosis</strong> on the left navigation bar, information about the first instance in the Instance list is displayed by default.   </div>
   

6. On the **Space usage ** tab, you can view the following information:

   
   <Tabs>
   <Tab zoneid="qpskEnYQNZ" title="View spatial profile">
   <TabTitle>View spatial profile</TabTitle>
   
   In the **Spatial profile** section, you can view the **Used space**, **Space usage**, and **Remaining available days** for the current instance.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default"><strong>Space usage</strong> includes the occupied space and <strong>Remaining</strong> space of <strong>User data</strong>, <strong>System</strong>, <strong>Bin Log</strong>, <strong>Redo Log</strong>, <strong>Undo Log</strong>, <strong>Relay logs</strong>, <strong>Audit log</strong>, <strong>Slow log</strong>, <strong>Error log</strong>, <strong>Temporary file</strong>, and <strong>Other documents</strong>.</div>
   
   
   
   </Tab>
   <Tab zoneid="hwpcP0zoH9" title="View trends in space">
   <TabTitle>View trends in space</TabTitle>
   
   In the **Trends in space** section, you can set a time frame and view the **Space utilization** and **Size of space** for the current instance during this period. Default is the trends in space in the past day.
   
   
   </Tab>
   <Tab zoneid="vhzUzxBStQ" title="Create space analysis task">
   <TabTitle>Create space analysis task</TabTitle>
   
   * Create space analysis task
   
   
   Click **Analyze now** and select the analysis scope in the dialog box:
   
   
      * Analyze all space: Select **All space** and click **OK**.
   
      * Analyze specified space: Select **Specified space**, check the target databases and tables as needed, and click **OK**.
   
   
   You can select multiple databases simultaneously for analysis. However, when multiple databases are selected, table filtering is not supported.
   
   
   * View space analysis results
   
   
   You can filter analysis tasks by generation time range. By default, tasks from the past day are displayed, with a maximum history of 30 days.
   
   
      * View task list: Displays an overview of all analysis tasks, including task type, target object, creation time, completion time, state, and error message.
   
      * View task details: In the task list, click **View details** in the **Actions** column of the target task to go to its space analysis page. Here, you can view the **Used space**, **Space usage**, and **Tablespace** information for the specified space.
   
   
   In the **Tablespace** section, you can analyze the detailed storage space usage of tables within all or specified databases and tables in a database instance. This analysis is generated based on statistics from the system database information_schema.tables. This section enables rapid identification of large tables, tables with severe fragmentation, or potential optimization targets, facilitating storage optimization, performance tuning, and resource planning.
   
   
         * The data is sourced from system tables and may contain slight inaccuracies.
   
         * To ensure performance, the system imposes limits on the analysis scope:
   
            * Instance\-level analysis limit: Space capacity is analyzed for up to the first 20,000 tables per database instance.
   
            * Database\-level analysis limit: For a single database (DB), tablespace usage is analyzed for up to 2,000 tables within it.
   
            In the left panel of the tablespace section, click a database name to switch and view detailed tablespace information for that database. You can also filter databases by entering the database name in the search box. The specific details displayed include:
   
                  
                  |**Parameter** |**Description** |
                  |---|---|
                  |Table name |Table name in the database. |
                  |Storage engine |The storage engine used by the table. |
                  |Tablespace |The total space occupied by the table (including both data and indexes), displayed in MB or KiB. |
                  |Tablespace ratio |Indicates the proportion of space that this table occupies within the current database, sourced from `information_schema.tables`, making it easier to identify large tables.<br><br> The calculation method is: Single table's `(INDEX_LENGTH + DATA_LENGTH + DATA_FREE)` / total tables' `(INDEX_LENGTH + DATA_LENGTH + DATA_FREE)`. |
                  |Data space |The size of space storing actual data, taken from the `DATA_LENGTH` field in `information_schema.tables`. |
                  |Index space |The physical storage size of the index structures, sourced from the `INDEX_LENGTH` field in `information_schema.tables`. |
                  |Fragmentation ratio |The proportion of tablespace that is not effectively utilized—higher values indicate a greater need for optimization (e.g., `optimize table`). This metric is sourced from `information_schema.tables`.<br><br>The calculation method is: `DATA_FREE / (INDEX_LENGTH + DATA_LENGTH + DATA_FREE)`. |
                  |Number of table rows |The total number of rows (records) in the current table. |
                  |Average row length |The average number of bytes per row, reflecting data density. |
                  |Auto\-increment ID value. |The current maximum value of the auto\-increment column, useful for assessing growth trends, sourced from the `AUTO_INCREMENT` field in `information_schema.tables`. |
                  
   
   
   
   
   </Tab>
   </Tabs>
