---
title: "DescribeTickets"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/DescribeTickets"
---

Call the DescribeTickets API to query tickets in batch.

<span id="PHTlfmSN"></span>
## Request type

Synchronous request.

<span id="qc5O1Uq4"></span>
## Request parameters


|**Name** |**Type** |**Required?**  |**Description** |**Sample** |
|---|---|---|---|---|
|ListType |String |Yes |The ticket type for batch queries. The values are as follows:<br><br><br>*  `All`: All.<br><br>* `CreatedByMe`: Created by me<br><br>* `ApprovedByMe`: Approved by me |All<br><br> |
|OrderBy |String |No<br><br> |Sort field of the returned result. |UpdateTime |
|SortBy |String |No<br><br> |Sort in descending or ascending order. The values are as follows:<br><br><br>* `ASC`: Ascending order. Default value.<br><br>* `DESC`: Descending order. |DESC |
|PageNumber |Integer |No |Page number. The value range is 1 to 1000, with a default of 1. |1 |
|PageSize |Integer |No |Number of records per page. The value range is 1 to 1000, with a default of 10. |3 |


<span id="qV4kiwNr"></span>
## Response parameters

You only need to understand the return parameters in the table below. You do not need to understand the parameters not in the table.


|**Name** |**Type** |**Description** |**Sample** |
|---|---|---|---|
|CreateTime |Long |Ticket creation time. |2025\-09\-05T09:59:58Z |
|CreateUser |String |Ticket creator<br><br> |See the return example.<br><br> |
|CurrentUser |String |The current handler. |See the return example.<br><br> |
|CurrentUserRole |String |Current handler role. |InstanceOwner |
|DBName |String |Database name. |test |
|InstanceId |String |Instance ID. |mysql\-04af670e\*\*\*\* |
|InstanceType |String |Database types: The following database types are supported:<br><br><br>* `MySQL`: RDS for MySQL.<br><br>* `VeDBMySQL`: NDB for MySQL.<br><br>* `Postgres`: RDS for PostgreSQL. |MySQL |
|Memo |String |Ticket remarks information. |test |
|TicketExecuteType |String |Ticket execution type. The values are as follows:<br><br><br>* `Automatic`: Automatically executed after approval. This is the default value.<br><br>* `Manual`: Manual execution.<br><br>* `Cron`: Scheduled execution. |Auto |
|TicketId |String |Ticket ID. |196390493418532\*\*\*\* |
|TicketStatus |String |Ticket status. Return values are as follows:<br><br><br>* `TicketUndo`: Not started<br><br>* `TicketPreCheck`: Pre\-checking<br><br>* `TicketPreCheckError`: Pre\-check failed<br><br>* `TicketExamine`: Approving<br><br>* `TicketCancel`: Cancelled<br><br>* `TicketReject`: Rejected<br><br>* `TicketWaitExecute`: Wait for execution<br><br>* `TicketExecute`: In progress<br><br>* `TicketFinished`: Executed successfully<br><br>* `TicketError`: Failed |TicketFinished |
|TicketType |String |Ticket type, with the following return values.<br><br><br>* `NormalSqlChange`: Regular SQL change ticket<br><br>* `FreeLockStructChange`: Lock\-free structural change ticket<br><br>* `FreeLockSqlChange`: Lockless schema changes ticket<br><br>* `DataMigrationImport`: Data import ticket<br><br>* `DataMigrationExportDB`: Data export ticket<br><br>* `DataMigrationExportSqlResult`: SQL result set export ticket<br><br>* `DataClean`: Data cleanup and archiving ticket |FreeLockStructChange<br><br> |
|Title |String |Ticket title. |test |
|UpdateTime |Long |Update time. |2025\-09\-05T10:00:13Z |
|total |Integer |Total number of tickets. |3 |


&nbsp;

<span id="5AmigbbB"></span>
## Request example

```JSON
POST /?Action=DescribeTickets&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dbw.cn-beijing.byteplusapi.com.cn
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/dbw/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****

{
    "ListType": "CreatedByMe",
    "OrderBy": "UpdateTime",
    "SortBy": "DESC",
    "PageNumber": 1,
    "PageSize": 3
}
```


<span id="HH7Pxue4"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202509081502470F61B3192B569A2BBE25-b29a5a",
        "Action": "DescribeTickets",
        "Version": "2018-01-01",
        "Service": "dbw",
        "Region": "cn-beijing"
    },
    "Result": {
        "Tickets": [
            {
                "AffectedRows": "",
                "CreateTime": "2025-09-05T09:59:58Z",
                "CreateUser": {
                    "CreateUserId": "2100067216",
                    "CreateUserName": "RootAccount"
                },
                "CurrentUser": {
                    "CurrentUserId": "2100067216",
                    "CurrentUserName": "RootAccount"
                },
                "CurrentUserRole": "",
                "DBName": "test",
                "DataArchiveConfig": {
                    "ArchiveType": "Once",
                    "IsBackUp": false,
                    "TableName": "",
                    "TimeInfos": null
                },
                "Description": "",
                "InstanceId": "mysql-04af670e****",
                "InstanceType": "MySQL",
                "Memo": "",
                "TicketExecuteType": "Auto",
                "TicketId": "196390493418532****",
                "TicketStatus": "TicketFinished",
                "TicketType": "FreeLockStructChange",
                "Title": "",
                "UpdateTime": "2025-09-05T10:00:13Z"
            },
            {
                "AffectedRows": "",
                "CreateTime": "2025-09-05T07:12:52Z",
                "CreateUser": {
                    "CreateUserId": "2100067216",
                    "CreateUserName": "RootAccount"
                },
                "CurrentUser": {
                    "CurrentUserId": "2100067216",
                    "CurrentUserName": "RootAccount"
                },
                "CurrentUserRole": "",
                "DBName": "test",
                "DataArchiveConfig": {
                    "ArchiveType": "Once",
                    "IsBackUp": false,
                    "TableName": "",
                    "TimeInfos": null
                },
                "Description": "",
                "InstanceId": "mysql-04af670e****",
                "InstanceType": "MySQL",
                "Memo": "",
                "TicketExecuteType": "Auto",
                "TicketId": "196386287998365****",
                "TicketStatus": "TicketFinished",
                "TicketType": "FreeLockStructChange",
                "Title": "",
                "UpdateTime": "2025-09-05T07:13:15Z"
            },
            {
                "AffectedRows": "",
                "CreateTime": "2025-09-04T11:33:10Z",
                "CreateUser": {
                    "CreateUserId": "2100067216",
                    "CreateUserName": "RootAccount"
                },
                "CurrentUser": {
                    "CurrentUserId": "497392",
                    "CurrentUserName": "Alice"
                },
                "CurrentUserRole": "InstanceOwner",
                "DBName": "yyz",
                "DataArchiveConfig": {
                    "ArchiveType": "Once",
                    "IsBackUp": false,
                    "TableName": "",
                    "TimeInfos": null
                },
                "Description": "",
                "InstanceId": "mysql-a6d71503****",
                "InstanceType": "MySQL",
                "Memo": "test",
                "TicketExecuteType": "Auto",
                "TicketId": "196356599941221****",
                "TicketStatus": "TicketExamine",
                "TicketType": "<UNSET>",
                "Title": "test",
                "UpdateTime": "2025-09-04T11:33:10Z"
            }
        ],
        "total": 3
    }
}
```


<span id="q7LXwA0f"></span>
## Error code

For more details, see [Error codes](https://docs.byteplus.com/en/docs/DBW/error-codes).
