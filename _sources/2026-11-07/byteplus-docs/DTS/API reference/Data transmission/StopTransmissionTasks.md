---
title: "StopTransmissionTasks"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/StopTransmissionTasks"
---

Call the StopTransmissionTasks API to batch terminate transmission tasks.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* If there are tasks whose task status is not `Running` or `Suspend` among the batch\-terminated tasks, the corresponding task API calls will fail. You can call the [DescribeTransmissionTasks](https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks) API to view the transmission task details.

* Terminating a task is the same as unsubscribing from the task. Once terminated, here's how you'll be billed based on your chosen billing method:

   * Pay\-as\-you\-go: Terminating a task does not involve Unsubscribe amount, and will be charged according to the actual amount of resources used.

   * Subscription: Terminating a task is equivalent to unsubscribing. After unsubscribing from a subscription DTS task, the refund will be credited to the account balance. For details on refund calculation rules, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/6269/81013#.5LqM44CB6Z2e5LiD5aSp5peg55CG55Sx6YCA6K6i6K-05piO). Subscription is only applicable to data synchronization and data subscription tasks.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskIds |Array of String |Yes |["23208c23945048b482f4b0ece62\*\*\*\*","f4f091ce030a4137b50fd60cdff\*\*\*\*" ] |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> to view the task ID.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When performing a batch terminate task, separate multiple task IDs with commas (,).</div><br> |
|StopAssociatedValidationTasks |Boolean |No |true |Whether to simultaneously terminate the data verification tasks associated with the selected tasks, with the following possible values:<br><br><br>* \- true: Default value. When the task is terminated, all its associated data verification tasks are also terminated simultaneously.<br><br>* \- false: Only terminate the selected task without affecting its associated data verification tasks. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=StopTransmissionTasks&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskIds": [
        "23208c23945048b482f4b0ece62****",
        "f4f091ce030a4137b50fd60cdff****"
    ]
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230320104141406D102417A9E80BEBDC",
        "Action": "StopTransmissionTasks",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/DTS/error_codes).
