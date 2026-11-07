---
title: "ModifyInstanceAttributes"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyInstanceAttributes-v2"
---

Call ModifyInstanceAttributes interface to modify the corresponding instance name, description and other instance information.

<span id="dac5dd48"></span>
## Request parameters


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |Instance ID. |
|InstanceName |String |No |MyInstance |Instance name. |
|InstanceDescription |String |No |New instance |Example description. |


<span id="192656ae"></span>
## Response parameter

None

<span id="2559b37e"></span>
## Example

<span id="fc0ef104"></span>
### Request example

```JSON
POST /?Action=ModifyInstanceAttributes&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng5ysg5vv9****",
  "InstanceName": "DTS-all",
  "InstanceDescription": "DTS-all"
}
```


<span id="2b622d4e"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302271847143C6FF96F30A58C7F0FE4",
        "Action": "ModifyInstanceAttributes",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
