---
title: "What should I do if I get the error Could not obtain exclusive lock on database 'model' when creating database?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/what-should-I-do-if-I-get-the-error-Could-not-obtain-exclusive-lock-on-database-model-when-creat-dat"
---

This article introduces the solution when `Could not obtain exclusive lock on database'model'` error is encountered when establishing a database.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Your account needs to be granted <code>VIEW SERVER STATE</code> permission or higher.</div>



1. Execute the following command to check if there are any other session occupancy locks.

   ```sql
   IF 
   EXISTS(SELECT request_session_id FROM 
   sys.dm_tran_locks 
   WHERE resource_database_id = 
   DB_ID('Model')) 
   PRINT 
   'Model Database being used by some other session' 
   ELSE 
   PRINT 
   'Model Database not used by other session'
   ```
   

   If the output is as follows, it indicates that the lock was occupied by another session.

   ```sql
   Model Database being used by some other session 
   Completion time: 2024-04-07 T7:24:54.6358865 + 08:00
   ```
   

2. Execute the following command to see which sessions are currently occupied by the modle.

   ```sql
   SELECT request_session_id FROM 
   sys.dm_tran_locks WHERE resource_database_id =DB_ID('Model');
   ```
   

3. Execute the following command to query information about the current session and the SQL statements executed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can only view information about the current session, which may be idle.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <code>session_id</code> corresponding process is no longer active, you may not be able to find the specific SQL statement in this way.   </div>
   

   ```sql
   SELECT 
       r.session_id, 
       r.start_time, 
       r.status, 
       r.command, 
       r.wait_type, 
       r.wait_time, 
       r.blocking_session_id, 
       r.cpu_time, 
       r.total_elapsed_time, 
       ST.text AS sql_text 
   FROM 
       sys.dm_exec_requests AS r 
   CROSS APPLY 
       sys.dm_exec_sql_text(r.sql_handle) AS ST 
   WHERE 
   session_id = < your_session_id >;//< your_session_id > replaced with request_session_id value found from the sys.dm_tran_locks view
   ```
   

4. The service determines whether the corresponding session can be terminated, or waits for the session to complete before operating.
