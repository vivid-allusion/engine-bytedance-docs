---
title: "DescribeTicketDetail"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeTicketDetail"
---

Call the DescribeTicketDetail API to query the details of a single ticket.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Call the DataDescribeTicketDetail API to query detailed ticket information.</div>


* <div data-tips="true" data-tips-type="default">When <code>TicketStatus</code> is <code>TicketExamine</code>, you can call the DataApproveTicket API to approve the ticket.</div>



<span id="avmeGI5a"></span>
## Request type

Synchronous request.

<span id="YxI9ZL0e"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Description** |**Sample** |
|---|---|---|---|---|
|TicketId |String |Yes |Ticket number |195480667651524\*\*\*\* |


<span id="OAUjn6AP"></span>
## Response parameters


|**Name** |**Type** |**Description** |**Sample value** |
|---|---|---|---|
|InstanceType<br><br> |String |Database type. The currently supported databases are listed below.<br><br><br>* `MySQL`: RDS for MySQL<br><br>* `VeDBMySQL`: NDB MySQL<br><br>* `Postgres`: RDS for PostgreSQL |MySQL<br><br> |
|InstanceId |String |Instance ID. |195480667651524\*\*\*\* |
|SqlText<br><br> |String<br><br> |SQL text to be executed. |CREATE TABLE test (id INT PRIMARY KEY) |
|TicketExecuteType<br><br> |String |Ticket execution type, return values are as follows.<br><br><br>* `Auto`: Automatically executed upon approval completion, default value.<br><br>* `Manual`: Manually executed.<br><br>* `Cron`: Scheduled execution. |Auto<br><br> |
|DatabaseName |String |Database name. |db_production |
|ExecStartTime<br><br> | Long |Execution start time, in seconds timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is returned only when <code>TicketExecuteType</code> is set to <code>Cron</code>.</div><br> |1692508800<br><br> |
|ExecEndTime |Long |The execution end time, in Unix timestamp format.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is returned only when <code>TicketExecuteType</code> is set to <code>Cron</code>.</div><br> |1692512400 |
|Memo<br><br> |String |Ticket remarks. |Create test tables for user data storage |
|Title |String |Ticket title. |Create test table ticket |
|CreateTime |String |Creation time. |2025\-08\-11T07:26:44Z |
|UpdateTime |String |Last updated time. |2025\-08\-11T07:26:44Z |
|CreateUser.CreateUserId |String |Creator ID. |123456 |
|CreateUser.CreateUserName |String |Creator name. |root |
|CurrentUser.CurrentUserIds |String |Current handler ID.<br><br>If there are multiple current handlers, separate each with an English comma (,). |473270,497392,1543634,1251643,1261592,2100067216dbw_bot<br><br> |
|CurrentUser.CurrentUserNames |String |Current handler name.<br><br>If there are multiple current assignees, separate each with an English comma (,). |huahua,csy,testcsy,cyg,dbw_subuser,dbw_bot |
|TicketId |String |Ticket number. |195480667651524\*\*\*\* |
|TicketStatus |String |Ticket status, with the following return values.<br><br><br>* `TicketUndo`: Not started<br><br>* `TicketPreCheck`: Pre\-check in progress<br><br>* `TicketPreCheckError`: Pre\-check failed<br><br>* `TicketExamine`: under review<br><br>* `TicketCancel`: canceled<br><br>* `TicketReject`: rejected<br><br>* `TicketWaitExecute`: pending execution<br><br>* `TicketExecute`: in progress<br><br>* `TicketFinished`: executed successfully<br><br>* `TicketError`: execution failed |TicketExamine<br><br> |
|TicketType |String |Ticket type. |NormalSqlChange |


<span id="K5Z8TIxP"></span>
## Request example

```JSON
POST /?Action=DescribeTicketDetail&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "TicketId": "195480667651524****"
}
```


<span id="D5cKXgde"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202508111531036046BED76806A001048D-ca8a90",
        "Action": "DescribeTicketDetail",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "CreateTime": "2025-08-11T07:26:44Z",
        "CreateUser": {
            "CreateUserId": "2100067216",
            "CreateUserName": "RootAccount"
        },
        "CurrentUser": {
            "CurrentUserId": "473270,497392,1543634,1251643,1261592,2100067216dbw_bot",
            "CurrentUserName": "huahua,csy,testcsy,cyg,dbw_subuser,dbw_bot"
        },
        "CurrentUserRole": "InstanceOwner",
        "DBName": "postgres",
        "Description": "",
        "InstanceId": "postgres-8bd8865c948d",
        "InstanceType": "Postgres",
        "Memo": "创建测试表用于用户数据存储",
        "TicketExecuteType": "Auto",
        "TicketId": "195480667651524****",
        "TicketStatus": "TicketExamine", 
        "TicketType": "NormalSqlChange",
        "Title": "创建测试表工单",
        "UpdateTime": "2025-08-11T07:26:45Z"
    }
}
```


<span id="cvajrGcg"></span>
## Error code

For more details, refer to [Error code](https://docs.byteplus.com/en/docs/DBW/error-codes).
