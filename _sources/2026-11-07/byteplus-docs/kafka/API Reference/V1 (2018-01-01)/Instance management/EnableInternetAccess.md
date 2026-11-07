---
title: "EnableInternetAccess"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/EnableInternetAccess-v1"
---

Call EnableInternetAccess interface to enable public network access.

<span id="818d40c2"></span>
## Instructions for use

After creating an instance, you can enable public network access through this interface and bind the public network IP for the instance. After enabling public network access, message queue Kafka version provides a public network access point for the instance, which is used for the client side to access the Kafka instance through the public network. The public network access method of Kafka instance requires SSL authentication. Currently, it supports one\-way authentication of server level certificates by the client side, and data encryption transmission. Compared with ordinary public network access methods, it has higher security.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the client side accesses the Kafka service through the public network, it needs to use the SASL_SSL access point to connect the instance, and configure the certificate and authentication information. Otherwise, an error will be reported when accessing. Please refer to the configuration method <a href="https://docs.byteplus.com/en/docs/kafka/connecting-by-SASL_SSL">Connecting to an instance by using a SASL_SSL endpoint</a>.</div>



* Version of this API is `2022-05-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="23a861a7"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|EipIds |List |optional |["Eip\-xxxxx"] |Elastic network interface card ID, namely EIP ID. |


<span id="e97f8ad5"></span>
## Response parameter

null

<span id="58c2a22f"></span>
## Example

<span id="a5067304"></span>
### Request example

```json
POST /?Action=EnableInternetAccess&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "kafka-****",
  "EipIds": [
    ""
  ]
}
```


<span id="371f838e"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "EnableInternetAccess",
    "Version": "2022-05-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
