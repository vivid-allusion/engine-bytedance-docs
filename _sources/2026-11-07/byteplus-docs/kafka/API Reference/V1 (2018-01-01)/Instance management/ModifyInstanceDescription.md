---
title: "ModifyInstanceDescription"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyInstanceDescription-v1"
---

Call ModifyInstanceDescription interface to modify instance description information.

<span id="91482144"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="d8ed9081"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceID |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|InstanceDescription |String |Required |Description |Instance description information. |
|InstanceName |String |optional |MyInstance |Instance name. |


<span id="c39a1ee0"></span>
## Response parameter

null

<span id="ce529ac5"></span>
## Example

<span id="1b46119b"></span>
### Request example

```json
POST /?Action=ModifyInstanceDescription&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "kafka-xxxxxxxx",
  "InstanceDescription": "new-describe",
  "InstanceName": "new-name"
}
```


<span id="8070303a"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifyInstanceDescription",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
