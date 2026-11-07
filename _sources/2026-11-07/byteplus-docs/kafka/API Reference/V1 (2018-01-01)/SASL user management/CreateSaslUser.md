---
title: "CreateSaslUser"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateSaslUser-v1"
---

Call the CreateSaslUser interface to create a Kafka SASL user.

<span id="db08e9df"></span>
## The

CreateSaslUser interface is used to create a SASL user under a Kafka instance that can publish and subscribe to messages using the SASL/SCRAM mechanism.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="ce30b9d7"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |The instance ID to which the SASL user belongs. |
|UserName |String |Required |my_user |The name of the SASL user. |
|Password |String |Required |Password |The password for the SASL user. |
|Description |String |optional |describe |Describe the information. |
|AllAuthority |Bool |Optional |True |Whether the SASL user has read and write permissions for all topics by default. Default is true.<br><br><br>* True: This user has read and write permissions for all topics.<br><br>* False: This user does not have read and write permissions for all topics. |


<span id="8551c008"></span>
## Response parameter

null

<span id="9ca57e6c"></span>
## Example

<span id="86ef577d"></span>
### Request example

```json
POST /?Action=CreateSaslUser&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "UserName": "my_user",
  "Password": "password",
  "Description": "describe",
  "AllAuthority": true
}
```


<span id="fe0b450f"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "CreateSaslUser",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
