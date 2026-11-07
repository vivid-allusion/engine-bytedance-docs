---
title: "DescribeTasks"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/DescribeTasks"
---

Call the DescribeTasks API to query tasks.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|PageNumber |Integer |Yes |1 |Current page number. The minimum value is 1. |
|PageSize |Integer |Yes |100 |Number of records per page. The minimum value is 1, and the maximum value cannot exceed 1,000. |
|InstanceId |String |No |postgres\-2904ed64\*\*\*\* |Instance ID. |
|TaskId |String |No |202509102225598DA116E6B90D38F149EA\-9f0b91 |Task ID. |
|TaskAction |String |No |ModifyDBInstanceSSL |Action corresponding to the task, generally the action of the corresponding Open API for the task. |
|CreationStartTime |String |No |2025\-09\-04T21:30:00Z |Task start time. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You must specify either the task time parameters (CreationStartTime and CreationEndTime) or the TaskId.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The maximum interval between CreationStartTime and CreationEndTime cannot exceed 7 days.</div><br> |
|CreationEndTime |String |No |2025\-09\-10T23:40:00Z |Task end time. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You must specify either the task time parameters (CreationStartTime and CreationEndTime) or the TaskId.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The maximum interval between CreationStartTime and CreationEndTime cannot exceed 7 days.</div><br> |
|TaskStatus |Array of String |No |Success |Task status. The valid values are:<br><br><br>* `Canceled`: cancelled.<br><br>* `WaitStart`: waiting for execution.<br><br>* `WaitSwitch`: to be switched.<br><br>* `Running`: running.<br><br>* `Running_BeforeSwitch`: running \- before switching.<br><br>* `Running_Switching`: running \- switching.<br><br>* `Running_AfterSwitch`: running \- after switching.<br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `Timeout`: timeout.<br><br>* `Rollbacking`: rolling back.<br><br>* `RollbackFailed`: failed to rollback.<br><br>* `Paused`: paused. |
|ProjectName |String |No |default |Project name. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TaskInfos |Array of [TaskInfoObject](https://docs.byteplus.com/en/docs/61/69194#taskinfoobject) |Refer to the sample response. |Task details. |
|Total |Integer |123 |Quantity of tasks matching query conditions. |


<span id="taskinfoobject"></span>
### TaskInfoObject


|**Parameter** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CostTimeMS |Long |11990 |Task time consumption. The unit is milliseconds. |
|CreateTime |String |2025\-09\-10T13:53:27Z |The time when the task was created. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time). |
|FinishTime |String |2025\-09\-10T13:53:39Z |Task completion time. The time format is yyyy\-MM\-ddTHH:mm:ssZ (UTC time). |
|InstanceId |String |postgres\-2904ed64\*\*\*\* |Task\-related instance ID. |
|ProjectName |String |default |Project name. |
|Region |String |cn\-beijing |Region of the task |
|ScheduledSwitchEndTime |String |2025\-09\-20T17:59:00Z |The deadline for the planned switch. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for tasks in the "wait to start", "waiting for execution", or "waiting for switch" state.</div><br> |
|ScheduledSwitchStartTime |String |2025\-09\-20T16:00:00Z |Start time of the scheduled switchover. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This field is returned only for tasks in the "wait to start", "waiting for execution", or "waiting for switch" state.</div><br> |
|TaskAction |String |AssociateAllowList |Open API name corresponding to the task. |
|TaskId |String |20250910215326D9573E9EDB8708234022\-3202e3 |Task ID. |
|TaskParams |String |{"InstanceId":"postgres\-2904ed64\*\*\*\*","EndpointId":"postgres\-2904ed64\*\*\*\*\-custom\-bf14"} |Task parameters. |
|TaskStatus |String |Success |Task status. The valid values are:<br><br><br>* `Canceled`: cancelled.<br><br>* `WaitStart`: waiting for execution.<br><br>* `WaitSwitch`: to be switched.<br><br>* `Running`: running.<br><br>* `Running_BeforeSwitch`: running \- before switching.<br><br>* `Running_Switching`: running \- switching.<br><br>* `Running_AfterSwitch`: running \- after switching.<br><br>* `Succeeded`: succeeded.<br><br>* `Failed`: failed.<br><br>* `Timeout`: timeout.<br><br>* `Rollbacking`: rolling back.<br><br>* `RollbackFailed`: failed to rollback.<br><br>* `Paused`: paused. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeTasks&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "PageNumber": 1,
    "PageSize": 5,
    "CreationEndTime": "2025-09-11T23:40:00Z",
    "CreationStartTime": "2025-09-10T21:30:00Z"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250911131641D9E1CECC49958E281C7B-15c708",
        "Action": "DescribeTasks",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {
        "TaskInfos": [
            {
                "CostTimeMS": 3235,
                "CreateTime": "2025-09-11T05:16:15Z",
                "FinishTime": "2025-09-11T05:16:18Z",
                "InstanceId": "postgres-635ef13f0f47",
                "ProjectName": "default",
                "Region": "cn-beijing",
                "TaskAction": "ModifyDBInstanceConfig",
                "TaskId": "20250911131615549F0FE8E578FD2772B1-64727b",
                "TaskParams": "{\"InstanceId\":\"postgres-635ef13f****\",\"GlobalReadOnly\":true}",
                "TaskStatus": "Success"
            },
            {
                "CostTimeMS": 119,
                "CreateTime": "2025-09-11T05:15:38Z",
                "FinishTime": "2025-09-11T05:15:38Z",
                "InstanceId": "postgres-635ef13f****",
                "ProjectName": "default",
                "Region": "cn-beijing",
                "TaskAction": "CreateDatabase",
                "TaskId": "2025091113153732DF01B85B0733C564B7-98c665",
                "TaskParams": "{\"InstanceId\":\"postgres-635ef13f****\",\"DBName\":\"fnyql9p8\",\"CharacterSetName\":\"utf8\",\"Collate\":\"en_US.utf8\",\"CType\":\"en_US.utf8\"}",
                "TaskStatus": "Success"
            },
            {
                "CostTimeMS": 133,
                "CreateTime": "2025-09-11T05:15:24Z",
                "FinishTime": "2025-09-11T05:15:24Z",
                "InstanceId": "postgres-635ef13f****",
                "ProjectName": "default",
                "Region": "cn-beijing",
                "TaskAction": "ModifyDBInstanceName",
                "TaskId": "202509111315246CB6233D740D0BD25DC7-bf4064",
                "TaskParams": "{\"InstanceId\":\"postgres-635ef13f****\",\"InstanceNewName\":\"测试实例-kmjt5p\"}",
                "TaskStatus": "Success"
            },
            {
                "CostTimeMS": 77,
                "CreateTime": "2025-09-11T05:15:24Z",
                "FinishTime": "2025-09-11T05:15:24Z",
                "InstanceId": "postgres-deacd3e6****",
                "ProjectName": "default",
                "Region": "cn-beijing",
                "TaskAction": "ModifyDBInstanceName",
                "TaskId": "20250911131524889D767ED5A0B19477A9-953dbc",
                "TaskParams": "{\"InstanceId\":\"postgres-deacd3e6****\",\"InstanceNewName\":\"测试实例-nvmp96\"}",
                "TaskStatus": "Success"
            },
            {
                "CostTimeMS": 86,
                "CreateTime": "2025-09-11T05:15:24Z",
                "FinishTime": "2025-09-11T05:15:24Z",
                "InstanceId": "postgres-a3c2cffc****",
                "ProjectName": "default",
                "Region": "cn-beijing",
                "TaskAction": "ModifyDBInstanceName",
                "TaskId": "202509111315238BE74A8188414622A7FD-dcfc00",
                "TaskParams": "{\"InstanceId\":\"postgres-a3c2cffc****\",\"InstanceNewName\":\"测试实例-ns9wri\"}",
                "TaskStatus": "Success"
            }
        ],
        "Total": 198
    }
}
```
