---
title: "ModifyTask"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyTask"
---

Call the ModifyTask API to edit the task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-2904ed64\*\*\*\* |Instance ID. |
|TaskId |String |Yes |202509102225598DA116E6B90D38F149EA\-9f0b91 |Task ID. |
|TaskEventOperation |String |Yes |ChangeToSpecifiedTime |The modification type of the task. Values:<br><br><br>* `ChangeToSpecifiedTime`: modify to execute during a specific time period. When the value is `ChangeToSpecifiedTime`, ModifyBeginTime and ModifyEndTime are required.<br><br>* `ChangeToMaintainTime`: modify to execute during the maintenance window.<br><br>* `ImmediateExecute`: execute now.<br><br>* `Cancel`: cancel the task.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Only tasks in <strong>To be switched</strong> state support modification.</div><br> |
|ModifyBeginTime |String |No |2025\-08\-03T06:00:00Z |The start time for execution within a specific time period. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When modifying the task to execute within a specific time period, that is, when TaskEventOperation equals <code>ChangeToSpecifiedTime</code>, this field is required.</div><br> |
|ModifyEndTime |String |No |2025\-08\-03T07:59:00Z |The end time for execution within the specific time period. The time format is `yyyy-MM-ddTHH:mm:ssZ` (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When modifying the task to execute within a specific time period, that is, when TaskEventOperation equals <code>ChangeToSpecifiedTime</code>, this field is required.</div><br> |
|ProjectName |String |No |default |Project name. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyTask&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-c80c288b****",
    "TaskEventOperation": "Cancel",
    "TaskId": "2025091110404644E00EC62320C40F8011-5345d9"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250911133256F240B7AC2B8EC854351B-748dd1",
        "Action": "ModifyTask",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
