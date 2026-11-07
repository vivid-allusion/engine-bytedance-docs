---
title: "DescribeSubscriptionGroups"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroups"
---

Call the DescribeSubscriptionGroups API to query the subscription consumption group list.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Is it required?**  |**Sample** |**Description** |
|---|---|---|---|---|
|TaskId |String |Yes |4ddec6d036384248a25862fb\*\*\*\*\*\*\*\* |Task ID. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|Groups |Array of [SubscriptionGroupInfo](https://docs.byteplus.com/en/docs/57/15990#subscriptiongroupinfo) |```json```<br>```[```<br>```    {```<br>```        "CreateTime":1679280623,```<br>```        "DelaySeconds":0,```<br>```        "Description":"",```<br>```        "GroupName":"9863318d02ed4a6f88f14c03a******:test****",```<br>```        "LogEndOffset":0,```<br>```        "Offset":-1,```<br>```        "PartitionId":0,```<br>```        "UpdateTime":1679280623,```<br>```        "Username":"test****"```<br>```    }```<br>```]```<br> |Consumer group list information. |


<span id="subscriptiongroupinfo"></span>
### SubscriptionGroupInfo


|**Parameter** |**Type** |**Sample** |**Description** |
|---|---|---|---|
|GroupName |String |9863318d02ed4a6f88f14c03a2\*\*\*\*\*\*:test\*\*\*\* |Consumer group name |
|Description |String |Used for subscription to Kafka. |The description of the consumer group helps you identify the purpose of the consumer group. |
|CreateTime |Long |1679280623 |Time to create a consumer group. Unit: Second. |
|UpdateTime |Long |1679280623 |Update time of the consumer group. Unit: Second. |
|PartitionId |Integer |0 |Partition ID. |
|LogEndOffset |Long |0 |The latest position. |
|Offset |Long |\-1 |Current offset. |
|DelaySeconds |Long |0 |Delay time. Unit: Second. |
|Username |String |test\*\*\*\* |The name of the account. |


<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
POST /?Action=DescribeSubscriptionGroups&Version=2022-10-01 HTTP/1.1
Content-Type: application/json
Host: dts.cn-beijing.byteplusapi.com.cn
X-Date: 20221001T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20221001/cn-beijing/dts/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "TaskId": "9863318d02ed4a6f88f14c03a2*****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202303201059212810CCE542B4640C8B51",
        "Action": "DescribeSubscriptionGroups",
        "Version": "2022-10-01",
        "Service": "dts",
        "Region": "cn-beijing"
    },
    "Result": {
        "Groups": [
            {
                "CreateTime": 1679280623,
                "DelaySeconds": 0,
                "Description": "",
                "GroupName": "9863318d02ed4a6f88f14c03a******:test****",
                "LogEndOffset": 0,
                "Offset": -1,
                "PartitionId": 0,
                "UpdateTime": 1679280623,
                "Username": "test****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For more details, see [Error code](https://docs.byteplus.com/en/docs/DTS/error_codes).
