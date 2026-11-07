---
title: "CreateAcl"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateAcl-v2"
---

Call the CreateAcl interface to create an ACL policy.

<span id="c653c253"></span>
## **Instructions for use**

This interface is used to create ACL policy rules and set access permissions to Topic or Group for users.

<span id="0ffbee96"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnoe8qu6hgw1\*\*\*\* |The instance ID of the ACL to be created. |
|UserName |String |Yes |Test |SASL users that the rule allows access to. Specify support as "\*" to allow access by any user. |
|Ip |String |Yes |192.168.0.1/18, 127.0.0.1 |The IP address or network segment that the rule allows access to. Specify support as "\*" to allow arbitrary IP access. Use "," to separate multiple IPs. |
|ResourceType |String |Yes |Topic |The resource type of the rule binding. Configuration as Topic or Group is supported. |
|PatternType |String |Yes |Literal |The match type of the rule.<br><br><br>* Literal: exactly match type. ACL policies only match resources with exactly the same name. The resource name needs to be set at this point.<br><br>* Prefixed: Prefix match type. The ACL policy matches the resource with the specified prefix. At this time, the resource name prefix needs to be set. |
|Resources |String |Yes |Test |The resource name or name prefix of the bound Topic or Group.<br><br><br>* When the resource name match type (PatternType) is an exact match (Literal), this field is used to specify the resource name, indicating that the specified user has permissions on a resource. Support is set to "\*" to represent all resources of Topic or Group type.<br><br>* When the resource name match type (PatternType) is Prefixed, this field is used to specify which resources with prefixed names the user has permissions on. |
|AccessPolicy |String |Yes |Read |The type of permission the SASL user has.<br><br><br>* `Read`: That is, consume messages from Topic or join a consumption group, leave a consumption group, reset consumption check points, etc.<br><br>* `Write`: that is, write a message to the Topic.<br><br>* `Read,Write`: both have `Read` and `Write` Permissions.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the resource type (ResourceType) is Group, only the Read permission is supported, not the Write permission.</div><br> |


<span id="74fb57a7"></span>
## **response parameter**

None

<span id="f7113520"></span>
## **example**

<span id="691d3b6b"></span>
### **Request example**

```JSON
POST /?Action=CreateAcl&Version=2022-05-01 HTTP/1.1
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


<span id="197a0884"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231009164722454D149CF757A9BFA1DC",
        "Action": "CreateAcl",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null,
}
```
