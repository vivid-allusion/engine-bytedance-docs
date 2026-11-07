---
title: "DeletePublicAddress"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeletePublicAddress-v2"
---

Call the DeletePublicAddress interface to turn off public network access.

**Instructions for use**

If you no longer need to access the instance through the public network, you can turn off the public network access method of the instance through this interface and unbind the public network IP address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To modify the public network IP of the instance, you can call this interface to close public network access first, and then pass <a href="https://docs.byteplus.com/en/docs/kafka/CreatePublicAddress-v2">CreatePublicAddress</a> Open public network access and bind a new Internet Protocol Address.</div>


* <div data-tips="true" data-tips-type="tip">This interface can dynamically close the public network access of the instance, but it does not release EIP resources. You need to release EIP resources manually.</div>



<span id="568f0f77"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |The Kafka instance ID of the public access method to be closed. |


<span id="b9303059"></span>
## **response parameter**

None

<span id="ce70a621"></span>
## **example**

<span id="0ea0fdab"></span>
### **Request example**

```JSON
POST /?Action=CreatePublicAddress&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng3s31v076****"
}
```


<span id="031da119"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022719153124D1D2D50917B7639137",
        "Action": "DeletePublicAddress",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
