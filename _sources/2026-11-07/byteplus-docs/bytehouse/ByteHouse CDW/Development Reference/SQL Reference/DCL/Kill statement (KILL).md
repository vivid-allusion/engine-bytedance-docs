---
title: "Kill statement (KILL)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/kill-statement"
---

ByteHouse currently supports terminating queries (kill query).

<span id="dee3cdfc"></span>
### KILL QUERY

The kill query statement forcibly terminates the currently running query.

<span id="35708705"></span>
#### Advisory

If you only have read\-only access (SELECT, SHOW, GET), you can only terminate queries you created. You can view your data management permissions through **ByteHouse Console** \> **Permission Management** \> **User** \> **Data management permission**. To obtain higher data management permissions, contact the system administrator for configuration. For details, see [Data privilege management](https://docs.byteplus.com/docs/bytehouse/docs-permission).

<span id="0f5b8d82"></span>
#### Syntax

```SQL
KILL QUERY
  WHERE <where expression to SELECT FROM system.processes query>  
  [SYNC|ASYNC|TEST]  
  [FORMAT format]
```


Detailed parameter description is as follows:


|Param |Required |Description |
|---|---|---|
|`WHERE <where expression to SELECT FROM system.processes query>` |Yes |Use the where expression to define the conditions for the query to terminate. This example terminates queries that meet conditions selected from the `system.processes` table. You can replace `system.processes` with your table name. |
|[SYNC |ASYNC |TEST]<br><br><br>* ASYNC: Asynchronous forced termination is used by default. The asynchronous termination executes forcibly without confirming whether the current query has stopped (stop).<br><br>* SYNC: Synchronous queries wait for all queries to stop before terminating and display process information. SYNC returns information shown in the `kill_status` column, including the following types:<br><br>   * `finished` – The query has successfully terminated.<br><br>   * `waiting` – A termination signal has been sent, waiting for the query to end.<br><br>   * Other values explain the reason why the query cannot be terminated.<br><br>* TEST: TEST only verifies the user's permission and lists the operations to be terminated. |
|[FORMAT format] |No |Optional values define the output format of the command execution result. The default output format is TabSeperated. Common supported formats include TabSeperated, CSV, Pretty, JSON, JSONEachRow, XML, and others. |


<span id="a52b52d5"></span>
#### Example

<span id="43d5bcd8"></span>
##### Example 1: forcibly terminate a specific query


1. Get the list of unfinished queries.

   ```SQL
   SHOW PROCESSLIST WHERE query like 'SELECT%'
   ```
   

2. Terminate the query.

   ```SQL
   KILL QUERY WHERE initial_query_id='2-857d-4a57-9ee0-327da5d60a90' 
   ```
   


<span id="b92d79ed"></span>
##### Example 2: synchronously terminate all queries run by a user


1. Get the list of unfinished queries.

   ```SQL
   SHOW PROCESSLIST
   ```
   

2. Terminate query.

   ```SQL
   KILL QUERY WHERE user='username' SYNC 
   ```
   


&nbsp;
