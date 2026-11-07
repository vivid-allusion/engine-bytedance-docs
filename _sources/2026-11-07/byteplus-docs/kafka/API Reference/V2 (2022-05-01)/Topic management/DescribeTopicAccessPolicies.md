---
title: "DescribeTopicAccessPolicies"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopicAccessPolicies-v2"
---

Call the DescribeTopicAccessPolicies interface to view the permission list of the Topic.

<span id="484f58af"></span>
## **Instructions for use**

This interface is used to view the list of permissions for a given topic, i.e. which SASL users have what permissions for this topic.

<span id="5fd3449c"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\* |Instance ID. |
|TopicName |String |Yes |my_topic |Topic name. |
|UserName |String |No |my_user |The user name used for filtering, only exact matches are supported.<br><br>When specifying a username, only the specified user's permissions on this Topic are returned. |


<span id="22cb6a51"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|AllAuthority |Boolean |True |Is the Topic configured to be accessible to all users?<br><br><br>* True: All users have read and write access to this Topic.<br><br>* False: Any user does not have read and write permissions for this topic by default. For users with custom permissions and their permissions, please refer to AccessPolicies. |
|AccessPolicies |Array of AccessPolicyObject |/ |Custom permission configuration, that is, to set custom permissions for this topic for some users. This is only required when AllAuthority is False. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) The AccessPolicyObject section in. |


<span id="f42c0efc"></span>
## **example**

<span id="cb1551e0"></span>
### **Request example**

```JSON
POST /?Action=DescribeTopicAccessPolicies&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "TopicName": "123",
  "UserName": "user123"
}
```


<span id="bf58a1ea"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302272011074873E7AD95D343684BEE",
        "Action": "DescribeTopicAccessPolicies",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AccessPolicies": [
            {
                "AccessPolicy": "PubSub",
                "UserName": "user123"
            }
        ],
        "AllAuthority": false
    }
}
```
