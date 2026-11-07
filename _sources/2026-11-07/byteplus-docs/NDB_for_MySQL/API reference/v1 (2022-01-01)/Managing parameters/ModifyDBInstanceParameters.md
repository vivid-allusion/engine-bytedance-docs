---
title: "ModifyDBInstanceParameters"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyDBInstanceParameters"
---

Call the ModifyDBInstanceParameters to modify instance parameters.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The instance currently has no **pending** parameter modification events. You can search and view them by instance ID in the **Planned event list**. For steps, see [Viewing event list](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_event_list).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceParameters&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-gzwdsf9b\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|Parameters |Array of [OverrideParameterObject](https://docs.byteplus.com/en/docs/265/57395#overrideparameterobject) |Yes |See the request example. |The parameter and parameter value to be modified. |
|ScheduleType |String |No |Immediate |Execution method. Possible values:<br><br><br>* `Immediate`: Execute now (default).<br><br>* `MaintainTime`: Execute during the maintenance window. |


<span id="overrideparameterobject"></span>
### OverrideParameterObject


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|ParameterName |String |Yes |auto_increment_increment |Parameter name. |
|ParameterValue |String |Yes |1 |Parameter running value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ScheduleEventId |String |wpck1hqmndmb\*\*\*\* |Event ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyDBInstanceParameters&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-gzwdsf9b****",
    "Parameters": [
        {
            "ParameterName": "auto_increment_increment",
            "ParameterValue": "2"
        }
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202502251546052135B1F0689AE7184178-7a8a42",
        "Action": "ModifyDBInstanceParameters",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
