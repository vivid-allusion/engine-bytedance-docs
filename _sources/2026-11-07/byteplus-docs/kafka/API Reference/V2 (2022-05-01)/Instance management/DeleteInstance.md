---
title: "DeleteInstance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteInstance-v2"
---

Call the DeleteInstance interface to release the pay\-per\-amount instance.

<span id="f5e412c2"></span>
## Instructions for use

Deleting instances is generally used in scenarios such as application offline.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before deleting an instance, make sure the Topic is empty.</div>


* <div data-tips="true" data-tips-type="tip">The instance cannot be restored after being deleted, please call with caution.</div>


* <div data-tips="true" data-tips-type="tip">Only pay\-as\-you\-go instances support deletion through this interface. It is automatically deleted after the package year\-to\-month instance expires, and deletion is not supported during the contract period.</div>



<span id="8b126aeb"></span>
## Request parameters


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |Instance ID. |


<span id="e3578854"></span>
## Response parameter

None

<span id="fc2615dd"></span>
## Example

<span id="bb82e4cc"></span>
### Request example

```JSON
POST /?Action=DeleteInstance&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng3s31v076****"
}
```


<span id="04907da3"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022719153124D1D2D50917B7639137",
        "Action": "DeleteInstance",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
