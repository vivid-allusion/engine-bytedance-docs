---
title: "DescribeAllowListDetail"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeAllowListDetail-v2"
---

Call DescribeAllowListDetail query the details of the specified allowlist.

<span id="46515c34"></span>
## **Instructions for use**

You can use this interface to view the details of the specified allowlist.

<span id="28708642"></span>
## **Request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-fda2ed6365b94c909e44198fbbf4\*\*\*\* |The allowlist ID to be queried. |


<span id="4d712649"></span>
## **Response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|AllowListId |String |acl\-fda2ed6365b94c909e44198fbbf4\*\*\*\* |Allowlist ID. |
|AllowListName |String |Test |Allowlist name. |
|AllowListDesc |String |Test allowlist |Allowlist description. |
|AllowList |String |127.0.0.1,192.168.0.1/24 |List of allowlist rules. |
|AssociatedInstances |Array of AssociatedInstanceInfo |/ |Allowlist binding instance information. For detailed instructions, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) AssociatedInstanceInfo part in. |


<span id="3ab98096"></span>
## **Example**

<span id="b183120c"></span>
### **Request example**

```JSON
POST /?Action=DescribeAllowListDetail&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "AllowListId": "acl-fda2ed6365b94c909e44198fbbf4****"
}
```


<span id="deb5e919"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D149CF7****9BFA1DC",
        "Action": "DescribeAllowListDetail",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AllowList": "127.0.0.1,192.168.0.1/24",
        "AllowListDesc": "test",
        "AllowListId": "acl-fda2ed6365b94c909e44198fbbf4****",
        "AllowListName": "test",
        "AssociatedInstances": [
            {
                "InstanceId": "kafka-cnitzqgnk0g4****",
                "InstanceName": "doc-test"
            }
        ]
    }
}
```
