---
title: "DeleteAllowList"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteAllowList-v2"
---

Call DeleteAllowList to delete an already created allowlist rule.

<span id="c81e59c4"></span>
## **Instructions for use**

After creating an allowlist rule, you can use this interface to delete the corresponding allowlist rule. If the allowlist has bound a Kafka instance, it cannot be deleted directly. You should unbind all bound instances before deleting.

<span id="04412881"></span>
## **Request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|AllowListId |String |Yes |acl\-fda2ed6365b94c909e44198fbbf48bcd |The allowlist ID to be deleted. |


<span id="181d9754"></span>
## **Response parameter**

None

<span id="bd3d4133"></span>
## **Example**

<span id="3254e0dd"></span>
### **Request example**

```JSON
POST /?Action=DeleteAllowList&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "AllowListId":"acl-fda2ed6365b94c909e44198fbbf4****"
}
```


<span id="a6135eae"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454***7A9BFA1DC",
        "Action": "DeleteAllowList",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
