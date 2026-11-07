---
title: "CreateDmlSqlChangeTicket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/CreateDmlSqlChangeTicket"
---

Call the CreateDmlSqlChangeTicket interface to create a DML data change ticket.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The DML SQL statements to be executed in this interface cannot exceed 1,000 and must not include DDL SQL statements.</div>


* <div data-tips="true" data-tips-type="default">This is an asynchronous interface. A ticket ID will be returned upon successful creation. Call the DataDescribeTicketDetail interface to query detailed ticket information.</div>


* <div data-tips="true" data-tips-type="default">Pre\-checks are required during ticket creation, and the duration depends on the number of SQL statements to be executed.</div>



<span id="c6u55GEQ"></span>
## Request type

Asynchronous request.

<span id="XvdlFiYX"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Description** |**Sample** |
|---|---|---|---|---|
|InstanceType |String<br><br> |Yes |Database types currently supported are listed below.<br><br><br>* `MySQL`: RDS for MySQL<br><br>* `VeDBMySQL`:  NDB MySQL<br><br>* `Postgres`: RDS for PostgreSQL |MySQL |
|InstanceId |String |Yes |Database instance ID. |mysql\-2579f0\*\*\*\*\*\* |
|SqlText<br><br> |String<br><br> |Yes |Pending DML SQL statements.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Regular SQL changes can support multiple DML statements, separated by semicolons (;).</div><br><br><br>* <div data-tips="true" data-tips-type="default">Regular SQL changes are suitable for small\-scale data modifications and support multiple statements.</div><br> |delete from test_table where id = 1;<br><br> |
|TicketExecuteType<br><br> |String<br><br> |Yes<br><br> |Work order execution type, with the following values:<br><br><br>* `Auto`: Automatically executes upon approval completion (default).<br><br>* `Manual`: Manual execution.<br><br>* `Cron`: Scheduled execution. |Cron<br><br> |
|DatabaseName |String |Yes |Database name for the pending ticket. |db_production |
|ExecStartTime<br><br> |Long |No<br><br> |Execution start time, using second timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>TicketExecuteType</code> is set to <code>Cron</code>, the execution start time must be specified.</div><br> |1692508800<br><br> |
|ExecEndTime |Long<br><br> |No |Execution end time, using timestamp format in seconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When <code>TicketExecuteType</code> is set to <code>Cron</code>, the execution end time must be specified.</div><br><br><br>* <div data-tips="true" data-tips-type="default"><code>ExecEndTime</code> Must be later than <code>ExecStartTime</code>.</div><br> |1692512400<br><br> |
|Memo<br><br> |String |No |Ticket remarks. Detailed remarks facilitate future maintenance. |Create a test table for user data storage. |
|Title |String |No |Ticket title. |Create test table ticket |


<span id="hxiaqtGc"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|TicketId |String |Ticket number |196490404892248\*\*\*\* |


<span id="zlBYKC7j"></span>
## Request example

```JSON
POST /?Action=CreateDmlSqlChangeTicket&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
  "InstanceType": "MySQL",  
  "InstanceId": "mysql-2579f0******",  
  "SqlText": "delete from test_table where id = 1",  
  "TicketExecuteType": "Cron",  
  "DatabaseName": "db_production", 
  "ExecStartTime": 1692508800,  
  "ExecEndTime": 1692512400, 
  "Memo": "Create a test table for user data storage.",  
  "Title": "Create test table ticket" 
}
```


<span id="k3eFq5Nd"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202405101815074D6C61C22FD7E479870C-e62012",
        "Action": "CreateDmlSqlChangeTicket",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "TicketId": "196490404892248****"
    }
}
```


<span id="ZKIi6Nr7"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
