---
title: "CreatePublicAddress"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreatePublicAddress-v2"
---

Call the CreatePublicAddress interface to enable public network access for Kafka instances.

<span id="8cfb5bca"></span>
## **Instructions for use**

If the public network access is not enabled when creating an instance, you can call this interface to bind the elastic public network IP (EIP) after creating the instance to enable the public network access method of the instance. After enabling public network access, the message queue Kafka version provides a public network access point for the instance, which is used by the client side to access the Kafka instance through the public network. You can select the corresponding access point according to whether SSL authentication is required. Support client side one\-way SSL authentication of server level certificate, data encrypted transmission, which has higher security than ordinary public network access methods.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">EIP provides independent public IP resources, including public IP addresses and public egress bandwidth services. The public address will be bound to your Elastic Public IP (EIP), and the fee will be charged by EIP.</div>


* <div data-tips="true" data-tips-type="tip">After enabling public network access, the message queue Kafka version provides a public network access point for the instance, which is used for the client side to access the Kafka instance through the public network. Please refer to <a href="https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL">Connecting to an instance by using a SASL_SSL endpoint</a>.</div>



<span id="53a324f2"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |Instance ID. |
|EipId |String |Yes |EIP\-2ZEUJXS \*\*\*\* 6cd |The ID of the EIP. |


<span id="3fe4f27b"></span>
## **response parameter**

None

<span id="e48ec512"></span>
## **example**

<span id="31f255af"></span>
### **Request example**

```JSON
POST /?Action=CreatePublicAddress&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng3s31v076****",
  "EipId": "eip-mio5dafp42685smt1b37****"
}
```


<span id="26dacbab"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227191417E460FF199EB6A16E7B23",
        "Action": "CreatePublicAddress",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
