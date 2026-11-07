---
title: "DescribeTopicAuthorities"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeTopicAuthorities-v1"
---

Call the DescribeTopicAuthorities interface to view the permission list of the Topic.

<span id="c044e14c"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="baa8268c"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\- \*\*\*\* |Instance ID. |
|TopicName |String |Required |my_topic |Topic name.<br><br>is 3 to 64 characters long and can only contain uppercase and lowercase letters, numbers, hyphens (\-), and underscores (_). |
|UserName |String |Optional |my_user |The user name used for filtering, matching exactly.<br><br>When specifying a user name, only the specified user's permissions on this Topic are returned. |


<span id="ab657a16"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|AllAuthority |Bool |Is the Topic configured to be accessible to all users?<br><br><br>* True: All users have read and write access to this Topic.<br><br>* False: Any user does not have read and write permissions for this topic by default. Please refer to the user with custom permissions and their permissions `Authorities`. |
|Authorities |List |The user configuration list found, please refer to the detailed information [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="ff94357c"></span>
## Example

<span id="682f8e33"></span>
### Request example

```json
POST /?Action=DescribeTopicAuthorities&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-****",
  "TopicName": "my_topic",
  "UserName": "my_user"
}
```


<span id="83ddde85"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeTopicAuthorities",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "AllAuthority": false,
    "Authorities": [
      {
        "Name": "tetuser",
        "Permission": "Read"
      }
    ]
  }
}
```
