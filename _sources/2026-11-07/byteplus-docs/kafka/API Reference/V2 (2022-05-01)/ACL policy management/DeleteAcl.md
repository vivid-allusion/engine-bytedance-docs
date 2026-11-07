---
title: "DeleteAcl"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteAcl-v2"
---

Call the DeleteAcl interface to remove the ACL policy.

<span id="8145bbbe"></span>
## **Instructions for use**

This interface is used to delete the specified ACL policy. Delete one ACL at a time. If you need to delete multiple ACLs, call this API multiple times to delete them in turn.

<span id="692e69eb"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnoe8qu6hgw1\*\*\*\* |The instance ID of the ACL to be deleted. |
|UserName |String |Yes |Test |The username of the rule configuration to be deleted. |
|Ip |String |Yes |192.168.0.1/18 |The IP network segment configured by the rule to be deleted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only specifying an IP address or network segment is supported.</div><br> |
|ResourceType |String |Yes |Topic |The type of resource configured by the rule to delete. |
|PatternType |String |Yes |Literal |The match type of the rule configuration to delete. |
|Resources |String |Yes |Test |The resource name of the rule configuration to be deleted. |
|AccessPolicy |String |Yes |Read |The access policy configured by the rule to be deleted.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Specifying only one access policy is supported.</div><br> |


<span id="b2a64a3b"></span>
## **response parameter**

None

<span id="b14bfae7"></span>
## **example**

<span id="0b1a66fb"></span>
### **Request example**

```JSON
POST /?Action=DeleteAcl&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "InstanceId": "kafka-cnoe8qu6hgw1****",
    "UserName": "test",
    "Ip": "192.168.0.1/18",
    "ResourceType": "Topic",
    "PatternType": "Literal",
    "Resource": "test",
    "AccessPolicy": "Read"
}
```


<span id="148d0a09"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D149CF757A9BFA1DC",
        "Action": "DeleteAcl",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null,
}
```
