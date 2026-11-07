---
title: "SuspendTransmissionTasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/SuspendTransmissionTasks"
---

Call the SuspendTransmissionTasks API to batch pause transmission tasks.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If there are tasks whose task status is not `Running` among the batch suspend tasks, the corresponding task API calls will fail. You can call the [DescribeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks) API to view the transmission task details.

* Pausing a subscription task that is in progress is not supported.

* When a task is suspended for more than 7 days, the task can not be resumed due to expired logs required by the source database. To avoid potential irrecoverable task issues, it is recommended that the pause duration does not exceed 24 hours.

* After a normally executing transmission task is paused, the current session (that is, the database session from the DTS server to the destination) will not be interrupted immediately. At the same time, if the transaction executed by the current session is not submitted, the row locks and table locks occupied by the relevant transaction will not be released, which may lead to other sessions being blocked from applying for relevant resources, affecting the existing performance of the database. If a task remains paused for an extended period (exceeding the inactive session timeout parameter), the session will be terminated and transactions will be rolled back. When pausing a task, it is recommended to confirm that DTS is not transmitting large transactions, as this may otherwise lead to degraded database performance.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |["2e0f73647d294856aa41ec3034d8\*\*\*\*","bfc3e433e06f48d196ddeafe7979\*\*\*\*"] |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> to view the task ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When performing a batch pause task, separate multiple task IDs with commas (,).</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=SuspendTransmissionTasks&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": [
        "2e0f73647d294856aa41ec3034d8****",
        "bfc3e433e06f48d196ddeafe7979****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230831144152DBE7FE5BB6E915ADD037",
        "Action": "SuspendTransmissionTasks",
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
