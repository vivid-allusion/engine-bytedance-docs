---
title: "ModifyUserAuthority"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyUserAuthority-v2"
---

Call the ModifyUserAuthority interface to change the default permissions of the specified SASL user for all users.

<span id="ff287c77"></span>
## **Instructions for use**

Message queue Kafka version provides flexible permission policies for SASL users and supports topic\-granular permission control. You can specify the default permission of SASL users for all topics through this interface, that is, whether to enable All Permitted. If it is closed, you can set more fine permission control policies for different topics. For detailed instructions, please refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).

<span id="a80cd364"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID to which the SASL user belongs. |
|UserName |String |Yes |my_user |SASL user name. |
|AllAuthority |Boolean |Yes |True |Specifies whether the user has read and write permissions for all topics.<br><br><br>* True: This user has read and write permissions for all topics.<br><br>* False: This user does not have read and write permissions for all topics. |


<span id="80efcff0"></span>
## **response parameter**

None

<span id="939e82f4"></span>
## **example**

<span id="0afb0fd3"></span>
### **Request example**

```JSON
POST /?Action=ModifyUserAuthority&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng1si21igu****",
  "AllAuthority": true,
  "UserName": "test"
}
```


<span id="6d851b07"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302272112469B56E707EFFA7E6BAA4E",
        "Action": "ModifyUserAuthority",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
