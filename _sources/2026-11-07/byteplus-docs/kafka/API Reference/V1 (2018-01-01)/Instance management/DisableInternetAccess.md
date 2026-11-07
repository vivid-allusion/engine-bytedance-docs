---
title: "DisableInternetAccess"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DisableInternetAccess-v1"
---

Call DisableInternetAccess interface to close public network access.

<span id="dd905b1e"></span>
## Instructions for use

If you no longer need to access the instance through the public network, you can turn off the public network access method of the instance through this interface and untie the public network Internet Protocol Address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To modify the public IP of the instance, you can first call this interface to close public network access, then open public network access through EnableInternetAccess, and bind a new Internet Protocol Address.</div>


* <div data-tips="true" data-tips-type="tip">This interface can dynamically close the instance's public network access, but it does not release EIP resources. You need to release EIP resources manually.</div>


* Version of this API is `2022-05-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="89d32556"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |


<span id="f8eddb1b"></span>
## Response parameter

null

<span id="1188a526"></span>
## Example

<span id="9e02071c"></span>
### Request example

```json
POST /?Action=DisableInternetAccess&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "kafka-****"
}
```


<span id="232ba9f1"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DisableInternetAccess",
    "Version": "2022-05-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
