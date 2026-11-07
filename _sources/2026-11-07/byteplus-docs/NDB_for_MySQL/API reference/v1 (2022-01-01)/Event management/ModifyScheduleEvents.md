---
title: "ModifyScheduleEvents"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/ModifyScheduleEvents"
---

Call the ModifyScheduleEvents to modify the execution time of the event to be executed.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

You can only modify planned events with an event type of configuration change (ModifyDBInstanceSpec) or modify parameters (ModifyDBInstanceParameters) and a state of waiting for execution (pending).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyScheduleEvents&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|EventId |Array of String |Yes |["uo7bx101rr29\*\*\*\*"] |The event ID. Use commas (,) to separate multiple event IDs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can select up to 100 operation and maintenance events to modify their execution time in batches.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Only events whose status is changed to pending execution are supported. Call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeScheduleEvents">DescribeScheduleEvents</a> API to query pending planned events for the current account.</div><br> |
|InstanceIds |Array of String |Yes |["vedbm\-ca12cbqv\*\*\*\*"] |The IDs of the instances for the event to be modified. Separate multiple Instance IDs with a comma (,).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br> |
|ScheduleType |String |Yes |Immediate |Execution method. Possible values:<br><br><br>* `Immediate`: Advance the operation and maintenance event to execute immediately.<br><br>* `MaintainTime`: Execute during the maintenance window. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=ModifyScheduleEvents&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "EventId": [
        "w51xskdez85y****"
    ],
    "ScheduleType": "Immediate",
    "InstanceIds": [
        "vedbm-cb4h7vlg****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240417154518D67D0DE06CE874E3D377-4f39a4",
        "Action": "ModifyScheduleEvents",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
