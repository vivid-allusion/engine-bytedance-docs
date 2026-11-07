---
title: "RetryTransmissionTasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/RetryTransmissionTasks"
---

Call the RetryTransmissionTasks API to batch retry failed transmission tasks.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If there are tasks whose task status is not `Failed` in the batch retry tasks, the corresponding task API call will fail. You can call the [DescribeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks) API to view the transmission task details.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |["d49082d628474f63a71cacfa9e6b\*\*\*\*","742a6d15b4524381a7722cca5d35\*\*\*\*"] |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to view the task ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When performing a batch retry task, separate multiple task IDs with commas (,).</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=RetryTransmissionTasks&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": [
        "d49082d628474f63a71cacfa9e6b****",
        "742a6d15b4524381a7722cca5d35****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202308311451445183C14F150333984C41",
        "Action": "RetryTransmissionTasks",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
