---
title: "ModifyPlannedEventExecuteTime"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyPlannedEventExecuteTime"
---

Call the ModifyPlannedEventExecuteTime API to modify the execution time of operation and maintenance events.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-a2f9831f\*\*\*\* |Instance ID. |
|EventId |String |Yes |7ccb2271846b439892797fe81219\*\*\*\* |Event ID. |
|TaskEventOperation |String |Yes |ChangeToSpecifiedTime |The modification type of the task. Values:<br><br><br>* `ChangeToSpecifiedTime`: change to execute within a specific time period.<br><br>* `ChangeToMaintainTime`: modify to execute during the maintenance window.<br><br>* `ImmediateExecute`: execute now.<br><br>* `ImmediateSwitch`: switch now.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When the value is <code>ChangeToSpecifiedTime</code>, ModifyBeginTime and ModifyEndTime are required.</div><br> |
|ModifyBeginTime |String |No |2025\-08\-03T06:00:00Z |The start time for execution within a specific time period. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when modifying the task to execute within the specific time period, that is, when TaskEventOperation is set to <code>ChangeToSpecifiedTime</code>.</div><br> |
|ModifyEndTime |String |No |2025\-08\-03T07:59:00Z |The end time for execution within the specific time period. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Required when modifying the task to execute within the specific time period, that is, when TaskEventOperation is set to <code>ChangeToSpecifiedTime</code>.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=DescribeWALLogBackups&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-08f97473****",
    "EventId": "f760e6d119e14fcda9ee12f8075f****",
    "TaskEventOperation": "ChangeToSpecifiedTime",
    "ModifyBeginTime": "2025-12-06T06:00:00Z",
    "ModifyEndTime": "2025-12-06T07:59:00Z"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20251204164500F1614C86F6D536E36C76-c86048",
        "Action": "ModifyPlannedEventExecuteTime",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```
