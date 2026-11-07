---
title: "DeleteUser"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteUser-v2"
---

Call the DeleteUser interface to delete the Kafka SASL user.

<span id="466f3dff"></span>
## **Instructions for use**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before deleting an account, please confirm that no relevant running producer and consumer instances are being authenticated by this user.</div>


<span id="d936e3b4"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID to which the account to be deleted belongs. |
|UserName |String |Yes |my_user |The name of the account to be deleted. |


<span id="52885686"></span>
## **response parameter**

None

<span id="3636d995"></span>
## **example**

<span id="c716196b"></span>
### **Request example**

```JSON
POST /?Action=DeleteUser&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "UserName": "123123"
}
```


<span id="418fadb9"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302272116312EE0067923D13C76F445",
        "Action": "DeleteUser",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
