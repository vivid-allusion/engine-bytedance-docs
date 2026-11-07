---
title: "DescribeAllowLists"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeAllowLists-v2"
---

Call DescribeAllowLists to query the allowlist list.

<span id="72b5bccb"></span>
## **Instructions for use**

You can use this interface to view all allowlist lists.

<span id="b3e8763e"></span>
## **Request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|RegionId |String |Yes |CN\-Beijing |Region ID. Represents an allowlist list under the specified instance of the query. |
|InstanceId |String |No |kafka\-cnitzqgnk0g4\*\*\*\* |Kafka instance ID. If this parameter is specified, an allowlist of all instances bound to this instance ID is queried. Otherwise, all allowlists are returned. |


<span id="7e2a5151"></span>
## **Response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|AllowLists |Array of AllowListInfo |/ |Allowlist list information.For detailed instructions, please see [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2). |


<span id="a8a542c7"></span>
## **Example**

<span id="053a003c"></span>
### **Request example**

```JSON
POST /?Action=DescribeAllowLists&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "RegionId": "cn-beijing",
    "InstanceId": "kafka-cnitzqgnk0g4****"
}
```


<span id="ded8ace0"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D1****757A9BFA1DC",
        "Action": "DescribeAllowLists",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowLists": [
            {
                "AllowListDesc": "test",
                "AllowListIPNum": 1,
                "AllowListId": "acl-fc849fa39a114c9684d429b93917***",
                "AllowListName": "test",
                "AssociatedInstanceNum": 2,
            }
        ]
    }
}
```
