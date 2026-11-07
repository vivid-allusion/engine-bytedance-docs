---
title: "ModifyTopicAuthorities"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyTopicAuthorities-v1"
---

Call ModifyTopicAuthorities interface to change the user permissions of the specified Topic.

<span id="ed52da16"></span>
## Instructions for use

This interface is used to modify the user permissions of the Topic. You can adjust the default permissions of the Topic to all users, and you can also customize the permissions of some users to this Topic. For detailed instructions on permission settings, please refer to [Creating an access control list](https://docs.byteplus.com/en/docs/kafka/creating-an-ACL).


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="1e5e77a5"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |The instance ID of the Topic. |
|TopicName |String |Required |my_topic |The name of the topic. |
|AllAuthority |Bool |Required |False |Whether all users have read and write permissions to this Topic by default. The default value is true.<br><br><br>* True: All users have read and write permissions to the current Topic by default.<br><br>* False: All users do not have read or write permissions to the current Topic by default. At this time, you can specify the user's permissions on the current Topic through the Authorities field setting. |
|Authorities |List |Optional | |Detailed permission configuration of Topic. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1).<br><br>The configuration in Authorities will only take effect if AllAuthority is configured to false, otherwise all users can read and write to this Topic regardless of the configuration in Authorities |


<span id="17354d94"></span>
## Response parameter

None

<span id="ea1a8edf"></span>
## Example

<span id="39988578"></span>
### Request example

```json
POST /?Action=ModifyTopicAuthorities&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "TopicName": "my_topic",
  "AllAuthority": false,
  "Authorities": [
    {
      "Name": "test",
      "Permission": "Read"
    }
  ]
}
```


<span id="8790021e"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "ModifyTopicAuthorities",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": null
}
```
