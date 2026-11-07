---
title: "SetBiSyncDDLSource"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/SetBiSyncDDLSource"
---

Call the SetBiSyncDDLSource API to switch the DDL synchronization direction of the bidirectional synchronization task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronize request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Both the forward and reverse synchronization tasks of the bidirectional synchronization task are in the incremental synchronization stage. You can call the [DescribeTransmissionTaskProgress](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress) API to view the task state.

* The forward synchronization task in the bidirectional synchronization task must contain DDL.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |cba921a501b042e8ba3c51f\*\*\*\*\*\* |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the task ID.</div><br> |
|Type |String |No |Backward |Set the task direction that contains the DDL action. The values are as follows:<br><br><br>* `Forward`: Indicates forward.<br><br>* `Backward`: Indicates reverse. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=SetBiSyncDDLSource&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "",
    "Type": "Backward"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024053110204995ED9D1532C1ED8ADC70-44e45b",
        "Action": "SetBiSyncDDLSource",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
