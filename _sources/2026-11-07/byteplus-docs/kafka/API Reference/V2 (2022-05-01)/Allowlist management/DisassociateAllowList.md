---
title: "DisassociateAllowList"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DisassociateAllowList-v2"
---

Call DisassociateAllowList unbind instance with allowlist.

<span id="58991cfc"></span>
## **Instructions for use**

You can use this interface to unbind an instance from the corresponding allowlist.

<span id="ae258367"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|AllowListIds |Array of String |Yes |["acl\-fda2ed6365b94c909e44198fbbf48\*\*\*\*"] |The allowlist ID to be untied. |
|InstanceIds |Array of String |Yes |["kafka\-cnitzqgnk0g\*\*\*\*"] |The ID of the Kafka instance to be unbound. |


<span id="a82ef7b8"></span>
## **response parameter**

None

<span id="b63ec845"></span>
## **example**

<span id="d345a784"></span>
### **Request example**

```JSON
POST /?Action=DisassociateAllowList&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "AllowListIds": ["acl-fda2ed6365b94c909e44198fbb****"],
    "InstanceIds": ["kafka-cnitzqgnk0g4****"]
}
```


<span id="5f47ff28"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454**8CF757A9BFA1DC",
        "Action": "DisassociateAllowList",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null,
}
```
