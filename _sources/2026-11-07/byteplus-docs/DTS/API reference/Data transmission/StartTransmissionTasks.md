---
title: "StartTransmissionTasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/StartTransmissionTasks"
---

Call the StartTransmissionTasks to batch start transmission tasks.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If there are tasks whose task status is not `Init` in the batch start tasks, the corresponding task API call will fail. You can call the [DescribeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks) interface to view detailed information about the transmission tasks.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |["2e0f73647d294856aa41ec3034d8\*\*\*\*","d20670ba8cec464885d504eee7c0\*\*\*\*"] |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> to view the task ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When performing a batch start task, separate multiple task IDs with commas (,).</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=StartTransmissionTasks&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskIds": [
        "2e0f73647d294856aa41ec3034d8****",
        "d20670ba8cec464885d504eee7c0****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230320102619F78568E65FC7880F296B",
        "Action": "StartTransmissionTasks",
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
