---
title: "RestartDBInstance"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/RestartDBInstance"
---

Call the RestartDBInstance to restart the instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

You can restart only instances that are in the **Running** state. When you call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances) API, the returned InstanceStatus must be Running.

<div data-tips="true" data-tips-type="default">Description</div>



* <div data-tips="true" data-tips-type="default">During the restart process, access to some services will be affected for a short period of time. Please operate with caution.</div>


* <div data-tips="true" data-tips-type="default">We recommend you restart instances during off\-peak hours and ensure that applications have an automatic reconnection mechanism.</div>



<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RestartDBInstance&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-r3xq0zdl\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the Instance ID.</div><br> |
|NodeId |String |No |vedbm\-r3xq0zdl\*\*\*\*\-1 |The ID of the node to be restarted.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If this parameter is specified, the specified node is restarted. If this parameter is not specified, the entire instance (all nodes) is restarted.</div><br> |
|ScheduleType |String |No |Immediate |Execution method. Possible values:<br><br><br>* `Immediate`: Execute now (default).<br><br>* `MaintainTime`: Execute during the maintenance window. |


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
POST /?Action=RestartDBInstance&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
     "InstanceId" : "vedbm-r3xq0zdl****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe",
        "Action": "RestartDBInstance",
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
