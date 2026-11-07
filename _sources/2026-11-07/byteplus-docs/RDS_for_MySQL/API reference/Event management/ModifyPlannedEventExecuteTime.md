---
title: "ModifyPlannedEventExecuteTime"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifyplannedeventexecutetime"
---

Call the ModifyPlannedEventExecuteTime API to postpone the execution time of a maintenance event.

## Request type

Synchronous request.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-d4942fd7\*\*\*\* |Instance ID. |
|EventId |String |Yes |7ccb2271846b439892797fe81219\*\*\*\* |Event ID. |
|TaskEventOperation |String |Yes |ChangeToSpecifiedTime |Modify the modification type of the task. Values:<br><br><br>* `ChangeToSpecifiedTime`: Modify to execute in the specified time period.<br><br>* `ChangeToMaintainTime`: Modify to execute in the maintainable time period.<br><br>* `Cancel`: Cancel the task.<br><br>* `ImmediateExecute`: Execute immediately.<br><br>* `ImmediateSwitch`: Switch immediately.<br><br><br>tip<br><br>When the value is `ChangeToSpecifiedTime`, you need to specify ModifyBeginTime and ModifyEndTime. |
|ModifyBeginTime |String |No |2023\-08\-03T06:00:00Z |The start time of the specified execution time window. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>This field is required when the task execution method is set to execute at a specified time, i.e., when `TaskEventOperation` is set to `ChangeToSpecifiedTime`. |
|ModifyEndTime |String |No |2023\-08\-03T07:59:00Z |The end time of the specified execution time window. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>This field is required when the task execution method is set to execute at a specified time, i.e., when `TaskEventOperation` is set to `ChangeToSpecifiedTime`. |
|ProjectName |String |No |default |The project to which it belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this parameter must be specified. |

## Response parameters

null

## Sample request

```json
POST /?Action=ModifyPlannedEventExecuteTime&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "EventId": "7ccb2271846b439892797fe81219****",
    "InstanceId": "mysql-405262bb392f",
    "TaskEventOperation": "ChangeToSpecifiedTime",
    "ModifyBeginTime": "2024-12-21T10:00:00Z",
    "ModifyEndTime": "2024-12-21T11:59:00Z"
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202401292217051EEC3AE57291E28EA9A5",
        "Action": "ModifyPlannedEventExecuteTime",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
