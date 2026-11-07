---
title: "ModifyTopicAccessPolicies"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyTopicAccessPolicies-v2"
---

Call ModifyTopicAccessPolicies interface interface to change the user permissions of the specified Topic.

<span id="77577b41"></span>
## **Instructions for use**

This interface is used to modify the user permissions of the Topic. You can adjust the default permissions of the Topic to all users, and you can also customize the permissions of some users to this Topic. For detailed instructions on permission settings, please refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).

<span id="6298aba6"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |The instance ID for the Topic. |
|TopicName |String |Yes |my_topic |The name of the Topic. |
|AllAuthority |Boolean |Yes |True |Whether the topic to be created has read and write permissions enabled for all users by default.<br><br><br>* True: All users have read and write access to this Topic.<br><br>* False: Not all users have read and write permissions for this topic. By default, the user's permissions for this topic follow the user's default permissions. If the default permissions do not meet the requirements, you can also specify a user's custom permissions for this topic through AccessPolicies. |
|AccessPolicies |Array of<br><br>AccessPolicyObject |No |/ |Custom permission configuration, that is, to set custom permissions on this topic for some users. This is only required when AllAuthority is False. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) The AccessPolicyObject section in. |
|DeletePolicies |Array of String |No |["User1", "user2"] |List of users to remove Topic permissions, where the user name should be specified. |


<span id="bd9da3a1"></span>
## **response parameter**

None

<span id="46816244"></span>
## **example**

<span id="94c89fd8"></span>
### **Request example**

```JSON
POST /?Action=ModifyTopicAccessPolicies&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "TopicName":"123",
  "AllAuthority":false,
  "AccessPolicies":[{"UserName":"user123","AccessPolicy":"PubSub"}]
}
```


<span id="89985acc"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302272036532B034FE726F55372A619",
        "Action": "ModifyTopicAccessPolicies",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
