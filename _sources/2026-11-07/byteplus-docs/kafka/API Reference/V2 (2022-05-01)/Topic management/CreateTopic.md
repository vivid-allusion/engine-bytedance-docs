---
title: "CreateTopic"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateTopic-v2"
---

Call the CreateTopic interface to create a Kafka Topic.

<span id="c59fc870"></span>
## **Instructions for use**

This interface is used to create a Kafka Topic under the specified instance, which users can use to publish and subscribe to messages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">During the instance matching process, it is forbidden to create a Topic in any way. Before creating a Topic, you need to confirm that the instance status is <strong>Running</strong>.</div>


<span id="5b80c1e1"></span>
## **Request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngbnntswg1\*\*\*\*x |Instance ID. |
|TopicName |String |Yes |my_topic |The name of the Topic to be created. The following requirements should be met:<br><br><br>* 3~ 64 characters.<br><br>* Must start with English or a number.<br><br>* Supported characters include English, numbers, hyphens (\-), underscores (_), and periods (.). |
|PartitionNumber |Integer |Yes |12 |The number of Topic partitions. The range is 1 to 300. If other Topics have been created in the instance, the sum of the partitions of all Topics does not exceed the upper limit of the number of partitions of the instance.<br><br>If the number of partitions cannot meet the business needs, you can purchase more partitions to increase the maximum number of partitions for your instance. For detailed instructions, please refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/kafka/upgrading-instance-specifications). |
|AllAuthority |Boolean |No |True |Whether the topic to be created has read and write permissions enabled for all users by default.<br><br><br>* True: This is the default configuration, and all users have read and write permissions for this Topic.<br><br>* False: Not all users have read and write permissions for this topic. By default, the user's permissions for this topic follow the user's default permissions. If the default permissions do not meet the requirements, you can also specify a user's custom permissions for this topic through AccessPolicies. |
|AccessPolicies |Array of AccessPolicyObject |No |/ |Custom permission configuration, that is, set custom permissions for this topic for some users. Only set when AllAuthority is false. |
|Description |String |No |Description information |Description information of the Topic. Length should not exceed 128 characters. |
|ReplicaNumber |Integer |No |2 |Number of Topic replicas. Can be set to 1, 2, or 3, the default is 3. |
|Parameters |String |No | |Topic\-level parameter configuration.<br><br>Please refer to the table below for the list of currently supported parameters and their default values. You can also go through the documentation [Modifying parameter configurations](https://docs.byteplus.com/en/docs/kafka/modifying-instance-parameter) View the details of each parameter.<br><br>When calling the API through Mail carrier, etc., you should pay attention to escaping, such as`{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MinInsyncReplicaNumber\":\"2\"}`. |


Parameters parameter description


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|MinInsyncReplicaNumber |String |No |1 |Minimum number of synchronous replicas.<br><br>When the number of synchronous replicas is less than the configuration value, the message will not be written to the corresponding Topic. The larger the configuration value, the data reliability will increase, but the availability will decrease. The default value is the number of replicas minus 1. Considering the availability of the Topic, it is recommended to set it to the number of replicas minus 1. |
|MessageMaxByte |String |No |12 |Maximum message size.<br><br>The unit is MB, and the value range is 1 to 12. The default setting of the maximum message size of the instance is used. |
|LogRetentionHours |String |No |2160 |Message retention duration.<br><br>The unit is hours, and the value range is 0~ 2160, that is, the message is retained for a maximum of 90 days. The default message retention time setting of the instance is used. |


<span id="3b333ecb"></span>
## **Response parameter**

None

<span id="ee376ef2"></span>
## **Example**

<span id="173571b0"></span>
### **Request example**

```JSON
POST /?Action=CreateTopic&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
    "InstanceId": "kafka-cnngbnntswg1****",
    "TopicName": "my_topic3",
    "PartitionNumber": 12,
    "AllAuthority": false,
    "AccessPolicies": [
        {
            "UserName": "user123",
            "AccessPolicy": "PubSub"
        }
    ],
    "Description": "123",
    "ReplicaNumber": 3,
    "Parameters": "{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MinInsyncReplicaNumber\":\"2\"}"
}
```


<span id="2759f2bd"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022719194098F0DF73611FD95FA1A2",
        "Action": "CreateTopic",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```
