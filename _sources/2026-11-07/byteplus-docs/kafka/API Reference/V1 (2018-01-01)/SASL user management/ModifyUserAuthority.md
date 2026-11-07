---
title: "ModifyUserAuthority"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyUserAuthority-v1"
---

Call the ModifyUserAuthority interface to change the default permissions of the specified SASL user for all users.

<span id="a688a45c"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="c29ea373"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |The instance ID of the SASL user. |
|UserName |String |Required |my_user |The name of the SASL user. |
|AllAuthority |Bool |Required |True |Whether the SASL user has read and write permissions for all topics.<br><br><br>* True: The user has read and write permissions for all topics by default.<br><br>* False: The user does not have read or write permissions to any topic by default. |


<span id="2ab50186"></span>
## Response parameter

None

<span id="e59e9370"></span>
## Example

<span id="ad42abfa"></span>
### Request example

```json
POST /?Action=ModifyUserAuthority&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "UserName": "my_user",
  "AllAuthority": true
}
```


<span id="e171be32"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifyUserAuthority",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
