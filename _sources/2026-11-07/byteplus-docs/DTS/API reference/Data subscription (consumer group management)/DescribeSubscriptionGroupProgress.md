---
title: "DescribeSubscriptionGroupProgress"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroupprogress"
---

Call the DescribeSubscriptionGroupProgress API to query the progress of the subscription consumer group.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |4ddec6d036384248a25862fb\*\*\*\*\*\*\*\* |Task ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/DTS/describetransmissiontasks">DescribeTransmissionTasks</a> API to query the task ID.</div><br> |
|GroupName |String |Yes |9863318d02ed4a6f88f14c03a28c5b6c:test\*\*\*\* |Consumer group name<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">you can call the <a href="https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroups">DescribeSubscriptionGroups</a> API to view the consumer group name</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|DelayTime |Long |0 |Delay time. |
|Partitions |Array of [SubscriptionPartitionProgress](https://docs.byteplus.com/en/docs/57/15989#subscriptionpartitionprogress) |```json```<br>```[```<br>```   {```<br>```         "Id": 0,```<br>```         "Offset": -1,```<br>```         "LogEndOffset": 0```<br>```  }```<br>```]```<br> |Shard progress information. |


<span id="subscriptionpartitionprogress"></span>
### SubscriptionPartitionProgress


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Id |Integer |0 |Partition ID. |
|LogEndOffset |Long |0 |Highest bit count. |
|Offset |Long |\-1 |Current offset. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeSubscriptionGroupProgress&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "9863318d02ed4a6f88f14c03a2*****",
    "GroupName": "9863318d02ed4a6f88f14c03a28c5b6c:test****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "Action": "DescribeSubscriptionGroupProgress",
        "Region": "cn-beijing",
        "Service": "dts",
        "Version": "2022-10-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "DelayTime": 0,
        "Partitions": [
            {
                "Id": 0,
                "Offset": -1,
                "LogEndOffset": 0
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
