---
title: "ModifyTask"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifytask"
---

Call the ModifyTask API to edit a task.

## Request type

Synchronous request.

## Precautions

When initiating the following tasks and selecting execution during a specified time period or maintenance window, the task will enter the **Pending Execution** state. The task cancellation will take effect immediately.

* RestartDBInstance

* ModifyDBProxySpec

When initiating the following tasks and selecting execution during a specified time period or maintenance window, the task will enter the **Running (Pre\-Switchover)**  state, performing resource preparation and background scheduling. If the task is canceled during this period, the cancellation will be executed after the current phase (resource preparation and background scheduling) is completed.

* MigrateToOtherZone

* UpgradeDBInstanceEngineMinorVersion

* CreateDBNodes

* DeleteDBNodes

* ModifyDBNodeSpec

* ModifyDBNodeTemporarySpec

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mysql\-603e30e6\*\*\*\* |Instance ID. |
|TaskId |String |Yes |20231025212656894676D90A825E31\*\*\*\* |The ID of the task to be modified. |
|TaskEventOperation |String |Yes |ChangeToSpecifiedTime |Modify the modification type of the task. Values:<br><br><br>* `ChangeToSpecifiedTime`: Modify to execute in the specified time period.<br><br>* `ChangeToMaintainTime`: Modify to execute in the maintainable time period.<br><br>* `Cancel`: Cancel the task.<br><br>* `ImmediateExecute`: Execute immediately.<br><br>* `ImmediateSwitch`: Switch immediately.<br><br><br>tip<br><br>When the value is `ChangeToSpecifiedTime`, you need to specify ModifyBeginTime and ModifyEndTime. |
|ModifyBeginTime |String |No |2024\-12\-22T05:00:00Z |The start time of the specified time period for execution. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>Required when the task execution method is set to execute at a specified time, i.e., when `TaskEventOperation` is set to `ChangeToSpecifiedTime`. |
|ModifyEndTime |String |No |2024\-12\-22T06:59:00Z |The end time of the specified time period for execution. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br>tip<br><br>Required when the task execution method is set to execute at a specified time, i.e., when `TaskEventOperation` is set to `ChangeToSpecifiedTime`. |
|ProjectName |String |No |default |The project to which the task belongs.<br><br>tip<br><br>If the AK/SK used to call the API belongs to a sub\-account that only has permissions for a specific project, this parameter must be provided. |

## Response parameters

null

## Sample request 1

取消任务

```json
POST /?Action=ModifyTask&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "mysql-f2f3bd1f****",
    "TaskId": "20240122071944PSCANNER0324C2****-7f2ca6",
    "TaskEventOperation": "Cancel"
}
```

## Sample response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "2023081115435093486CC3E10539843CDA",
        "Action": "ModifyTask",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```

## Sample request 2

修改任务执行时间

```json
POST /?Action=ModifyTask&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: open.ap-southeast-1.byteplusapi.com
X-Date: 20211202T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/ap-southeast-1/rds_mysql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceID": "mysql-f2f3bd1f****",
    "TaskId": "2024122415200733A28F43CA1D6B6CF4AF-1454a2",
    "TaskEventOperation": "ChangeToSpecifiedTime",
    "ModifyBeginTime": "2024-12-27T09:00:00Z",
    "ModifyEndTime": "2024-12-28T09:00:00Z"
}
```

## Sample response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "202412241523281F4B96DE5383EB6F8F43-13bdf4",
        "Action": "ModifyTask",
        "Version": "2022-01-01",
        "Service": "rds_mysql",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```

## Error codes

For more details, refer to [Error codes](https://docs.byteplus.com/en/docs/RDS_for_MySQL/error_code).
