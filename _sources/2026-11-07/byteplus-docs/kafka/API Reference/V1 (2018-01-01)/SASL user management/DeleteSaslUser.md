---
title: "DeleteSaslUser"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DeleteSaslUser-v1"
---

Call the DeleteSaslUser interface to delete the user of the SASL/SCRAM mechanism.

<span id="3713c378"></span>
## Instructions for use


* This interface will delete the relevant resources SASL_SCRAM the user under the instance. After the user is deleted, it cannot be restored. Please call carefully.

* Deleting Plain users is not supported.

* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="98a30db1"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Yes |Kafka\- \*\*\*\* |The instance ID to which the SASL user belongs to be deleted. |
|UserName |String |Yes |my_user |The name of the SASL user to be deleted. |


<span id="441b3b77"></span>
## Response parameter

None

<span id="47c5907a"></span>
## Example

<span id="7448447e"></span>
### Request example

```json
POST /?Action=DeleteSaslUser&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "UserName": "my_user"
}
```


<span id="2c6ea623"></span>
### Response example

```json
"RequestId": "****************",
    "Action": "DeleteSaslUser",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
