---
title: "Can execution results and execution records be exported after executing SQL in the SQL console?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/what-can-do-when-the-system-reports-client-timeout-exceeded-while-awaiting-headers-after-i-call-api"
---

RDS for MySQL and veDB for MySQL support exporting execution results. For detailed operations, see [Create an SQL result set export task for RDS for MySQL instance](https://docs.byteplus.com/en/docs/DBW/creating-a-sql-result-set-export-task-for-mysql) and [Create an SQL result set export task for NDB for MySQL instance](https://docs.byteplus.com/en/docs/DBW/Creating_a_SQL_result_set_export_task). Different Instance types display the following information for execution results and execution records after executing SQL statements in the SQL console:


* RDS for MySQL Or veDB for MySQL

   The following describes the specific information about execution results and execution records after you log in to the Data interaction platform of DBW and Execute SQL statements for an RDS for MySQL or veDB for MySQL instance:

   * Execution record: On the **Execution record** tab, the SQL statements that you executed in the SQL Console are displayed. You can also click **Clear records** to delete the records.

   * Execution result: The execution result varies depending on the objects in the database, as follows:

      * Table: In the **Execution result** area, the executed SQL result is displayed. At the same time, you can perform visualized add, delete, and modify actions on the table.

      * Stored procedures, functions, and views: In the **View result** area, the executed SQL results are displayed.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Execution results and execution records are not displayed during the modification, deletion, and creation of triggers and events.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Query results can only be modified for single\-table queries without column aliases, targeting tables with a primary key or full\-column unique index.         </div>
         

* Document Database for MongoDB

   After logging in to a Document Database for MongoDB instance on the SQL console of DBW and executing an SQL statement, the specific information of the execution result and execution record is as follows:

   * Execution record: On the **Execution record** tab, the SQL statements that you executed in the SQL console are displayed. You can also click **Clear records** to delete the records.

   * Execution result: The SQL results of the execution are displayed on the **Execution result** tab. You can click **Copy** to copy the results.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Exporting execution results is not supported.      </div>
      

* Cache for Redis

   After logging in to the Data interaction platform for Cache for Redis instance in DBW and executing SQL statements, you can view the SQL operation statements that have been executed. You can also click **Clear panel** to delete the SQL operation statements that have been executed.
