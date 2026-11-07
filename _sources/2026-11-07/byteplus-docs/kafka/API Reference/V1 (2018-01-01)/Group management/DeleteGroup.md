---
title: "DeleteGroup"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteGroup-v1"
---

Call DeleteGroup to delete the ConsumerGroup.

<span id="9d81e555"></span>
## Instructions for use

This interface will delete the consumption group under the instance, and it cannot be restored after deletion. Please call carefully.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="6ff771d5"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceID |String |Required |Kafka\- \*\*\*\* |The instance ID of the consumer group to be deleted. |
|ConsumerID |String |Required |my_group |The consumer group ID to be deleted. |


<span id="b5bd306e"></span>
## Response parameter

null

<span id="f550e5c4"></span>
## Example

<span id="2c881f26"></span>
### Request example

```json
POST /?Action=DeleteGroup&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceID": "kafka-****",
  "ConsumerID": "my_group"
}
```


<span id="9f63e276"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DeleteGroup",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
