---
title: "Common error log list"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/list_of_common_error_logs"
---


|Scenario |General format of the log content |Log level |
|---|---|---|
|Instance restart |the database system is shutting down |FATAL |
|Connection interrupt |terminating connection due to administrator command |FATAL |
||terminating connection due to unexpected postmaster exit |FATAL |
||terminating connection due to immediate shutdown command |FATAL |
||connection to client lost |FATAL |
|SQL syntax parsing error, check if the SQL statement is valid. |syntax error at or near xxx |ERROR |
||division by zero |ERROR |
||function xxx does not exist |ERROR |
||function with OID xxx does not exist |ERROR |
||column xxx does not exist |ERROR |
||column xxx of relation xxx does not exist |ERROR |
|Permission\-related error |password authentication failed for user xxx |FATAL |
||permission denied for table xxx |ERROR |
||permission denied for function xxx |ERROR |
||role xxx does not exist |FATAL |
||role with OID xxx does not exist |FATAL |
|Insufficient resources |out of memory |ERROR |
||could not write to file xxx |ERROR |
||could not open file xxx |ERROR |
||could not create shared memory segment: xxx |FATAL |
|Data integrity issue |item order invariant violated for index: xxx |ERROR |
||can't find left sibling high key in index |ERROR |
||duplicate key value violates unique constraint |ERROR |
||null value in column xxx violates not\-null constraint |ERROR |
||foreign key constraint cannot have xxx columns |ERROR |
||foreign key constraint xxx cannot be implemented |ERROR |
||foreign key constraints are not supported on foreign tables |ERROR |
|Transaction\-related issues |could not serialize access due to concurrent update |ERROR |
||could not serialize access due to concurrent delete |ERROR |
||invalid transaction termination |ERROR |
||deadlock detected |ERROR |
||current transaction is aborted xxx |ERROR |
