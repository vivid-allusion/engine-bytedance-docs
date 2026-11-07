---
title: "RetryValidationTask"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/RetryValidationTask"
---

Call the RetryValidationTask API to retry a transmission task.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The task status must be failed. That is, the value of `TaskStatus` is `Failed`. You can call the [DescribeValidationTaskInfo](https://docs.byteplus.com/en/docs/DTS/describevalidationtaskinfo) API to view the state of the verification task.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |aaeff059c0c846f3a8061202c\*\*\*\*\*\*\* |Verification task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DTS/describevalidationtasks">DescribeValidationTasks</a> API to query data verification tasks.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=RetryValidationTask&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "aaeff059c0c846f3a8061202c*******"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "RetryValidationTask",
        "Region": "cn-beijing",
        "Service": "dts",
        "Version": "2022-10-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
