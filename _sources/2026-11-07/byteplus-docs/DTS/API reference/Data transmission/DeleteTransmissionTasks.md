---
title: "DeleteTransmissionTasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/DeleteTransmissionTasks"
---

Call the DeleteTransmissionTasks API to batch delete transmission tasks

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Deleting a task is the same as unsubscribing from the task. Once deleted, here's how you'll be billed based on your chosen billing method:


* Pay\-as\-you\-go: Deleting a task does not involve an unsubscribe amount and will be charged based on the actual amount of resources used.

* Subscription: Deleting a task is equivalent to unsubscribing. After unsubscribing from a subscription DTS task, the refund will be credited to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/6269/81013#.5LqM44CB6Z2e5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO). Subscription is only applicable to data synchronization and data subscription tasks.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |["96ef0e25e6f14c99a4ba9b160c\*\*\*\*\*","742a6d15b4524381a7722cca5d35\*\*\*\*"] |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the Task ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When performing a batch delete task, separate multiple task IDs with commas (,).</div><br><br><br>* <div data-tips="true" data-tips-type="default">\- When batch deleting a migration or synchronization task, the associated data verification task is deleted at the same time if the selected task is associated with the data verification task.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DeleteTransmissionTasks&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": [
        "96ef0e25e6f14c99a4ba9b160c*****",
        "742a6d15b4524381a7722cca5d35****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230831145441454B1F9E42DAE3AB6606",
        "Action": "DeleteTransmissionTasks",
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
