---
title: "AssociateAllowList"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/AssociateAllowList-v2"
---

Call AssociateAllowList to bind the instance to the allowlist.

<span id="ab5de46e"></span>
## **Instructions for use**

You can use this interface to bind instances to the corresponding allowlist.

<span id="a9f6f763"></span>
## **Request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|AllowListIds |Array of String |Yes |["acl\-fda2ed6365b94c909e44198fbbf48\*\*\*\*"] |The allowlist ID to be bound. |
|InstanceIds |Array of String |Yes |["kafka\-cnitzqgnk0g4\*\*\*\*"] |The ID of the Kafka instance to bind. |


<span id="0f8964bf"></span>
## **Response parameter**

None

<span id="d30735a5"></span>
## **Example**

<span id="6dcb0459"></span>
### **Request example**

```JSON
POST /?Action=AssociateAllowList&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "AllowListIds": ["acl-fda2ed6365b94c909e44198fbbf4****"],
    "InstanceIds": ["kafka-cnitzqgnk0g4****"]
}
```


<span id="d39e1b64"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D149CF757A9****",
        "Action": "AssociateAllowList",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null,
}
```
