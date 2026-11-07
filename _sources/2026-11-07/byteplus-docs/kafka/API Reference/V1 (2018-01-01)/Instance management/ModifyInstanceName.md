---
title: "ModifyInstanceName "
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyInstanceName-v1"
---

Call the ModifyInstanceName interface to modify the instance name.

<span id="9ac68853"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="5017db85"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceID |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|InstanceDescription |String |optional |Description |Instance description information. |
|InstanceName |String |Required |MyInstance |Instance name. |


<span id="ad14ca1e"></span>
## Response parameter

null

<span id="a61b0eed"></span>
## Example

<span id="12def799"></span>
### Request example

```json
POST /?Action=ModifyInstanceName&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "kafka-xxxxxxxx",
  "InstanceDescription": "new-describe",
  "InstanceName": "new-name"
}
```


<span id="0b8623ad"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifyInstanceName",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
