---
title: "ModifyInstanceParams"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyInstanceParams-v1"
---

Call ModifyInstanceParams modify the configuration parameters of the instance.

<span id="e7fdfd99"></span>
## Instructions for use

This interface is used to modify the configuration parameters of the instance, such as parameters such as message retention length and maximum message size.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Modifying some configurations will cause the instance to restart, please proceed with caution.</div>



* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="6f7d2e12"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceID |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|Parameters |List |Required |*  |Parameters related to Kafka instances. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="7ef18ca5"></span>
## Response parameter

null

<span id="ecb2fe86"></span>
## Example

<span id="faeea92c"></span>
### Request example

```json
POST /?Action=ModifyInstanceParams&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "",
  "Parameters": [
    {
      "Name": "max_byte",
      "RunningValue": "1"
    }
  ]
}
```


<span id="83cb9f21"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifyInstanceParams",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
