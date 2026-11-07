---
title: "CreateUser"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateUser-v2"
---

Call the CreateUser interface to create a Kafka SASL user.

<span id="1a0ad89f"></span>
## **Instructions for use**

The CreateUser interface is used to create a SASL user under a Kafka instance that can publish and subscribe to messages using the SASL/SCRAM or SASL/PLAIN mechanisms.

<span id="1f96ea0b"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID to which the SASL user belongs. |
|UserName |String |Yes |Test1 |SASL user name. The following requirements should be met:<br><br><br>* Consists of letters, numbers, hyphens (\-), or underscores.<br><br>* The length is 3 to 64 characters.<br><br>* The user name is not supported to be set to admin or monitor, and the user name is unique within the instance. |
|UserPassword |String |Yes |Test@123456 |The password of the SASL user. The following requirements should be met:<br><br><br>* The length is 8 to 32 characters.<br><br>* It should contain at least any three of uppercase letters, lowercase letters, numbers, and special characters.<br><br>* Special characters supported include`!@#$%^&*()_+-=`. |
|AllAuthority |Boolean |Yes |True |Whether the SASL user has read and write permissions for all topics by default.<br><br><br>* True: This user has read and write permissions for all topics.<br><br>* False: This user does not have read and write permissions for all topics. |
|PasswordType |String |No |Plain |The user password type, which is the type of SASL user, is supported as:<br><br><br>* Scram: SASL user of type SCRAM.<br><br>* Plain: SASL user of type PLAIN.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you create a PLAIN type user, the effect will be delayed by 1 minute. Please be patient after creation.</div><br> |
|Description |String |No |Describe |SASL user description information. |


<span id="0d0443a0"></span>
## **response parameter**

None

<span id="8adb8a01"></span>
## **example**

<span id="5d559f05"></span>
### **Request example**

```JSON
POST /?Action=CreatCreateUserePublicAddress&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "UserName": "user1123123123",
  "UserPassword": "Test@123456",
  "AllAuthority":true,
  "Description": "vip"
}
```


<span id="af96004e"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230227211906E9F948120F87D27F1AEE",
        "Action": "CreateUser",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
