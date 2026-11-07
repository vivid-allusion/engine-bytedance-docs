---
title: "AddTagsToResource"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/AddTagsToResource-v2"
---

Call the AddTagsToResource interface to bind the label for the specified instance.

<span id="a1fa7ea8"></span>
## Interface description


* When setting a label, the label key (Key) and label value (Key) must meet certain rules. For more information, see [Associating with tags](https://docs.byteplus.com/en/docs/kafka/associating-with-tags).

* Label keys for multiple labels in the same instance cannot be repeated, and each label key can only have one label value.

* If the newly bound label key coincides with the already bound label key of the instance, the new label value will overwrite the original label value, please proceed with caution.


<span id="28a98d8a"></span>
## **request parameters**


|Name |Type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceIds |Array of String |Yes |["kafka\-cnngoanq4pxw\*\*\*\*"] |The instance ID of the tag that needs to be bound.<br><br>Support multiple instance IDs at a time, up to 50 instance IDs at the same time. |
|Tags |Array of TagObject |Yes |[{"Key": "test", "Value": "test"}] |The label key and label value array objects that need to be bound. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) The TagObject part in.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Support multiple groups of label key\-value objects at a time, and multiple groups of label key\-value objects are separated by English commas (,). Pass in up to 20 groups of label key\-value pairs at the same time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The label key value must meet the setting rules, please refer to the details <a href="https://docs.byteplus.com/en/docs/kafka/associating-with-tags">Associating with tags</a>.</div><br> |


<span id="fe321c32"></span>
## **response parameter**

None

<span id="5bc319cd"></span>
## Example

<span id="da2a14c5"></span>
### **Request example**

```JSON
POST /?Action=AddTagsToResource&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
   "InstanceIds":["kafka-cnngoanq4pxw****"],
   "Tags":[{"Key":"test","Value":"test"}]
}
```


<span id="c24cdc50"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227222006AC5A41DE7FA9D36772F9",
        "Action": "AddTagsToResource",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
