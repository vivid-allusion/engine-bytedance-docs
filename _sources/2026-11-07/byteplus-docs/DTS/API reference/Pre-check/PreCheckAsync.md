---
title: "PreCheckAsync"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/precheckasync"
---

Call the PreCheckAsync API to create and start a pre\-check task for the Database Transmission Service(DTS).

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

When you call the PreCheckAsync API, `Version` must be set to `2018-01-01`.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskID |String |Yes |05a7eb098f3443929835e2fab5\*\*\*\*\*\* |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the task ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|ID |String |174673297540540\*\*\*\* |Pre\-check ID. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=PreCheckAsync&Version=2018-01-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "05a7eb098f3443929835e2fab5******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240115140957BA42BED676A30104B613",
        "Action": "PreCheckAsync",
        "Version": "2018-01-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "ID": "174673313234787****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
