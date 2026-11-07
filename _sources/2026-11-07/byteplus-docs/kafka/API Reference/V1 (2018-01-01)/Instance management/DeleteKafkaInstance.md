---
title: "DeleteKafkaInstance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteKafkaInstance-v1"
---

Call the DeleteKafkaInstance interface to delete the instance.

<span id="5b5885cd"></span>
## Instructions for use

Deleting instances is generally used in scenarios such as application offline.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before deleting, perform the following resource checks:</div>


   * <div data-tips="true" data-tips-type="tip">All Topics and Groups in the instance have been deleted.</div>


   * <div data-tips="true" data-tips-type="tip">Connctor for an instance has been unsubscribed.</div>


* Version of this API is`2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="483fc590"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceID |String |Required |Kafka\- \*\*\*\* |Instance ID. |


<span id="0c4f2cbe"></span>
## Response parameter

null

<span id="17b0baf7"></span>
## Example

<span id="48e6df4b"></span>
### Request example

```json
POST /?Action=DeleteKafkaInstance&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceID": "kafka-****"
}
```


<span id="5010522c"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DeleteKafkaInstance",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
