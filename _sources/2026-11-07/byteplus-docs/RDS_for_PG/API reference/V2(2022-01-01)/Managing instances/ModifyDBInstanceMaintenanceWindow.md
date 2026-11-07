---
title: "ModifyDBInstanceMaintenanceWindow"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/ModifyDBInstanceMaintenanceWindow"
---

Call the ModifyDBInstanceMaintenanceWindow API to modify the maintenance window of an instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|DayKind |String |Yes |Week |The granularity of the maintenance cycle, with values of `Week`. |
|DayOfWeekMaintenanceTime |Array of [DayOfWeekObject](https://docs.byteplus.com/en/docs/61/72581#dayofweekobject) |No |Refer to the request example. |Maintenance window settings for the instance. |


<span id="dayofweekobject"></span>
### DayOfWeekObject


|**Parameter** |**Type** |**Is it required?**  |**Example** |**Description** |
|---|---|---|---|---|
|DayOfWeek |String |Yes |Monday,Tuesday |Specify the maintainable day for the instance each week. Multiple selections allowed.<br><br><br>* `Monday`: Monday.<br><br>* `Tuesday`: Tuesday.<br><br>* `Wednesday`: Wednesday.<br><br>* `Thursday`: Thursday.<br><br>* `Friday`: Friday.<br><br>* `Saturday`: Saturday.<br><br>* `Sunday`: Sunday.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this value is not specified or empty, it defaults to all seven days of the week.</div><br> |
|MaintenanceWindowStartTime |String |Yes |22:00Z |The instance's start time within the maintenance window on the maintainable day. Format: HH:mmZ (UTC time).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only start times between 16:00Z and 20:00Z are supported for the maintenance window.</div><br> |
|Period |Integer |Yes |6 |Duration of the instance's maintenance window on a maintainable day.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The duration is at least 2 hours and at most 6 hours.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=ModifyDBInstanceMaintenanceWindow&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "DayKind": "Week",
    "DayOfWeekMaintenanceTime": [
        {
            "Period": 6,
            "DayOfWeek": "Monday,Tuesday",
            "MaintenanceWindowStartTime": "16:00Z"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20251010125538DD78BB60C53C19A6A9D8-7fca2b",
        "Action": "ModifyDBInstanceMaintenanceWindow",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
