---
title: "RemoveTagsFromResource"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/RemoveTagsFromResource-v2"
---

Call RemoveTagsFromResource interface to untie labels for one or more instances.

<span id="8cc4d055"></span>
## Interface description

This interface is used to unlabel instances and supports batch operations.

<span id="20847546"></span>
## **request parameters**


|Name |Type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["kafka\-cnngoanq4pxw\*\*\*\*"] |The instance ID that needs to be untied.<br><br>Support multiple instance IDs at a time, up to 50 instance IDs at the same time. |
|TagKeys |Array of String |No |["instancetype", "chargetype"] |Tag that needs to be deleted.<br><br>Support multiple label keys at a time, separated by English commas (,) between multiple label keys. Up to 20 label keys are passed in at the same time. |
|All |Boolean |No |False |Whether to unbind all labels on the specified instance. The value range is as follows:<br><br><br>* True: Unbind all labels on the specified instance.<br><br>* False: (default) does not unbind all labels on the specified instance.<br><br><br>All parameters take effect only if the TagKeys value is empty. |


<span id="bd3bcbb8"></span>
## **response parameter**

None

<span id="28c98f22"></span>
## Example

<span id="6e5ba577"></span>
### **Request example**

```JSON
POST /?Action=RemoveTagsFromResource&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
   "InstanceIds":["kafka-cnngoanq4pxw****"],
   "Tags":["instancetype","chargetype"],
   "All":false
}
```


<span id="6c6b9096"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230217175421E698024A11179196218F",
        "Action": "RemoveTagsFromResource",
        "Version": "2022-01-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
