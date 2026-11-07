---
title: "CreateDdlSqlChangeTicket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/CreateDdlSqlChangeTicket"
---

Call the CreateDdlSqlChangeTicket interface to create a DDL schema change ticket.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Currently, this interface only supports creating DDL tickets for MySQL, VeDBMySQL, and Postgres databases. For MySQL and VeDBMySQL databases, lock\-free schema change tickets are created by default, and only one DDL SQL statement can be executed. For Postgres databases, DDL SQL statements are executed directly, with a maximum of 10 DDL SQL statements per execution.</div>


* <div data-tips="true" data-tips-type="default">Executing <code>ALTER</code> SQL statements on Postgres databases may cause table locking.</div>


* <div data-tips="true" data-tips-type="default">This is an asynchronous interface. A ticket ID will be returned upon successful creation. Call the DataDescribeTicketDetail interface to query detailed ticket information.</div>


* <div data-tips="true" data-tips-type="default">Pre\-checks are required during ticket creation, and the duration depends on the number of SQL statements to be executed.</div>



<span id="oJLva26M"></span>
## Request type

Asynchronous request.

<span id="0KD0EmZV"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Description** |**Sample** |
|---|---|---|---|---|
|InstanceType |String |Yes |Database type. Currently supported databases are listed below.<br><br><br>* `MySQL`: RDS for MySQL<br><br>* `VeDBMySQL`: NDB MySQL<br><br>* `Postgres`: RDS for PostgreSQL |MySQL |
|InstanceId |String |Yes |Database instance ID |mysql\-2579f0\*\*\*\*\*\* |
|SqlText<br><br> |String<br><br> |Yes |The DDL SQL statement to be executed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For regular SQL changes, multiple DDL statements can be issued, separated by semicolons (;). Note: DDL carries a table\-locking risk. It is recommended to choose a lock\-free schema change with row\-by\-row submission.</div><br> |CREATE TABLE test (id INT PRIMARY KEY)<br><br> |
|TicketExecuteType<br><br> |String<br><br> |Yes<br><br> |Work order execution type, enum values:<br><br><br>* `Auto`: Automatically executed after approval, default value.<br><br>* `Manual`: Manually executed.<br><br>* `Cron`: Scheduled execution. |Cron |
|DatabaseName |String |Yes |Database name for the pending work order. |db_production |
|ExecStartTime<br><br> |Long |No<br><br> |Execution start time in Unix timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TicketExecuteType</code> is set to <code>Cron</code>, the execution start time must be specified.</div><br> |1692508800<br><br> |
|ExecEndTime |Long |No |Execution end time in Unix timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>TicketExecuteType</code> is set to <code>Cron</code>, the execution end time must be specified.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><code>ExecEndTime</code> Must be later than <code>ExecStartTime</code>.</div><br> |1692512400 |
|Memo<br><br> |String |No |Ticket remarks. Detailed remarks facilitate future maintenance. |Create a test table for user data storage |
|Title |String |No |Ticket title. |Create test table work order |


<span id="ogkV96Bk"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|TicketId |String |Ticket ID. |178887541272244\*\*\*\* |


<span id="jhjzVMCq"></span>
## Request example

```JSON
POST /?Action=CreateDdlSqlChangeTicket&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
  "InstanceType": "MySQL",  
  "InstanceId": "mysql-123456",  
  "SqlText": "CREATE TABLE test (id INT PRIMARY KEY)",  
  "TicketExecuteType": "Cron",  
  "DatabaseName": "db_production",  
  "ExecStartTime": 1692508800,  
  "ExecEndTime": 1692512400,  
  "Memo": "Create a test table for user data storage",  
  "Title": "Create test table work order"
}
```


<span id="LI6nPprw"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202405101815074D6C61C22FD7E479870C-e62012",
        "Action": "CreateDdlSqlChangeTicket",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "TicketId": "178887541272244****"
    }
}
```


<span id="sUplHgHN"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
