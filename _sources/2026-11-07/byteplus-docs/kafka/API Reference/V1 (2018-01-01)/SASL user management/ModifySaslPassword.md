---
title: "ModifySaslPassword"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifySaslPassword-v1"
---

Call the ModifySaslPassword interface to reset the SCRAM user's password.

<span id="ff43fb15"></span>
## Instructions for use

This interface only supports changing the password of SCRAM users.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="be3a61c8"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|UserName |String |Required |my_user |User name. |
|Password |String |Required |new_password |The user's new password. |


<span id="637e593e"></span>
## Response parameter

null

<span id="a0d6fd2e"></span>
## Example

<span id="791269bb"></span>
### Request example

```json
POST /?Action=ModifySaslPassword&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "UserName": "my_user",
  "Password": "new_password"
}
```


<span id="1ee6ddbf"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifySaslPassword",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
