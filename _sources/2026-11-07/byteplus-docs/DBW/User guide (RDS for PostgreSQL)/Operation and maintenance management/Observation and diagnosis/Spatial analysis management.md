---
title: "Spatial analysis management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/spatial_analysis_management"
---

The Database Workshop (DBW) provides spatial analysis functionality, allowing you to visually view the space usage of an instance, such as table space usage.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 2,000 table space data entries can be displayed.

* The data is based on the system database `pg_stat_user_tables`.

* While using the spatial analysis feature, avoid modifying instance configurations, as this may prevent normal display of space usage.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for PostgreSQL has been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Applying for operation permissions (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**, and click **Space usage**.

   In the upper right corner of the **Observation and diagnosis** page, switch the instance type to **RDS for PostgreSQL**.

4. In the upper left corner of the **Space usage** tab, switch to the target instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also switch to the target instance by searching for the instance ID.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you access the <strong>Space usage</strong> tab through <strong>Observation and diagnosis</strong> on the left navigation bar, information about the first instance in the Instance list is displayed by default.   </div>
   

5. On the **Space usage ** tab, you can view the following information:

   * Spatial profile: On the **Spatial profile** pane, you can view **Used space**, **Space usage**, and **Remaining available days** of the current instance.

      * **Used space**: Includes the used space and the total space size of the instance.

      * **Space usage**: Displays the size of **Data**, **Log**, and **Remaining space**.

      * **Remaining available days**: This is a prediction based on the current usage, and the specific situation needs to be determined on a case\-by\-case basis.

   * Tablespace: On the **Tablespace** pane, you can view the instance's **Table name**, the table's **Database name**, the table's **Schema name**, **Tablespace**, **Tablespace ratio**, the table's **Row length**, the table's **row length**, the table's **Index visits**, **Full table scan times**, **Last recycle time**, **Last analysis time**, **Expansion rate**, and **Index space size** within a database. Some parameter descriptions are as follows:

      
      |**Parameter** |**Description** |
      |---|---|
      |**Tablespace** |Indicates the size of the database table, including all primary data and index files for the table, but excluding `toast` data and related indexes. Obtained through the function `pg_relation_size`. |
      |**Tablespace ratio** |The percentage of a single tablespace size to the sum of all tablespaces (user data only), calculated by `TableSpace / sum(TableSpace)`. |
      |**Index space** |Indicates the amount of disk space used by all indexes of the specified table in the database, which is calculated using the `pg_indexes_size` function. |
      |**Row length** |Indicates the rows in the table, taken from the `n_live_tup` field in `pg_stat_user_tables`. |
      |**Index visits** |Indicates the times the index in the table is scanned, taken from the `idx_scan` field in `pg_stat_user_tables`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If the index visits are high, it indicates that the index is frequently used. You need to maintain and optimize the index regularly.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the index visits are low, it indicates that the index is not fully used. You can evaluate whether the index is needed, or whether the query needs to be adjusted to better use the index.</div><br> |
      |**Full table scan times** |Indicates the number of sequential scans performed on a specific table, taken from the `seq_scan` field in `pg_stat_user_tables`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A high number of full table scans may indicate that RDS for PostgreSQL is performing many sequential scans for this table. For large tables, sequential scans can be slow. You can create indexes for commonly used query fields or optimize queries as needed to reduce the occurrence of sequential scans and improve query efficiency.</div><br> |
      |**Last recycle time** |Indicates the last time the `VACUUM` operation was performed on a specific table, taken from the `last_vacuum` field in `pg_stat_user_tables`. In RDS for PostgreSQL, the `VACUUM` operation is mainly used for the following purposes:<br><br><br>* Clears outdated row data (that is, dead tuples) generated by delete and update operations in the table and releases this space for future use.<br><br>* Updates the table's statistics so that the PostgreSQL query optimizer can generate query plans more effectively.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If your table is undergoing high updates or deletions, you may need to perform the <code>VACUUM</code> operation regularly. <code>last_vacuum</code> provides you with the exact time the <code>VACUUM</code> last executed, making it easy to track its execution and make corresponding adjustments.</div><br> |
      |**Last analysis time** |Indicates the last time a specific table was subjected to an `ANALYZE` operation, taken from the `last_analyze` field in `pg_stat_user_tables`.<br><br>The `ANALYZE` operation can collect statistics on tables and columns in tables and store this information in the system catalog. RDS for PostgreSQL's query optimizer can use this statistical information to help determine the optimal choice among various query execution plans, such as determining which order to retrieve information when a query needs to retrieve information from multiple tables will be the most efficient.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the timestamp of <code>last_analyze</code> is old, it means that the statistical information may no longer reflect the current state of the table. In this case, you need to run the <code>ANALYZE</code> operation to update the statistics.</div><br> |
      |**Expansion rate** |Indicates the percentage of dead tuples (deleted and updated rows) to total tuples (all rows), taken from the `round(n_dead_tup * 100 / (n_live_tup + n_dead_tup + 1),2)` field in `pg_stat_user_tables`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the expansion rate is high, you can execute <code>VACUUM</code> to clean up dead tuples, reclaim storage space, and improve database performance.</div><br> |
      |**Column index space size** |Indicates the space occupied by the index, obtained through the function `pg_total_relation_size`. |
