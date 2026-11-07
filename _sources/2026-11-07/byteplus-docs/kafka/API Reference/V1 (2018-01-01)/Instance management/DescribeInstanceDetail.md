---
title: "DescribeInstanceDetail"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeInstanceDetail-v1"
---

Call DescribeInstanceDetail interface to get the details of the specified instance.

<span id="1e5cc06d"></span>
## Instructions for use


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="75487185"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceID |String |Required |Kafka\- \*\*\*\* |Instance ID. |


<span id="05e39c35"></span>
## Response parameter


|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|Status |String |Running |The current state of the instance. Includes:<br><br><br>* Creating: Deploying<br><br>* Upgrading: Upgrading<br><br>* Updating: Changing<br><br>* Running: running<br><br>* Scaling: more matching<br><br>* Migrating: Migrating<br><br>* RollinGiBack: Rolling back<br><br>* CreateFailed: Failed to create<br><br>* UpgradeFailed: upgrade failed<br><br>* ScaleFailed: more suitable for failure<br><br>* Closed: closed<br><br>* CreatingUnpaid: Unpaid |
|UsedTopicNumber |Integer |20 |The number of Topics created by the current instance. |
|UsedGroupNumber |Integer |20 |The number of consumer groups that the current instance has created. |
|UsedPartitionNumber |Integer |120 |The number of partitions the current instance has created. |
|LimitPartitionNumber |Integer |1500 |The current maximum number of partitions that can be created. |
|StorageCapacity |Integer |1500 |The total disk size purchased by the instance in GiB. |
|AccountId |Integer |0 |The Byteplus Engine account ID to which the instance belongs. |
|InstanceName |String |Kafka\-test |Instance name. |
|Version |String |2.2.2 |The Kafka version number of the instance. |
|CreateTime |String |2021\-12\-14 18:26:56 |Instance creation time. format is `YYYY-MM-DDTHH:mm:ss+08:00`. |
|AvaliableZones |List |*  |The availability zone to which the instance belongs. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|KafkaParams |List |*  |A list of Kafka configuration parameters. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|Description |String |Test |Instance description information. |
|KafkaSpecifications |String |Kafka.n3.x2. small |The calculation specification of the instance. |
|InstanceId |String |Kafka\- \*\*\*\* |The instance ID that uniquely identifies the instance. |
|UsedCapacity |Integer |118 |The currently used capacity of the instance, in GiB. |
|ProjectName |String |Test |The name of the IAM project to which the user belongs. Empty if there is no project. |
|VpcInfo |JSON Array |*  |Network access information for the instance. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|KafkaEndpoints |List |*  |List of Kafka access points. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|KafkaChargeInfo |JSON Array |*  |Billing information for the instance. For detailed instructions, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|OptimalPartitionNumber |Integer |200.  |The optimum number of partitions for optimal Topic performance. |


<span id="ed94d0a7"></span>
## Example

<span id="1b64c06c"></span>
### Request example

```json
POST /?Action=DescribeInstanceDetail&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "kafka-****"
}
```


<span id="412b0740"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "********",
        "Action": "DescribeInstanceDetail",
        "Version": "2018-01-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "AccountId": 2000006376,
        "AvaliableZones": [
            {
                "ZoneId": "ap-southeast-1",
                "ZoneIdInChinese": "Availability Zone A:ap-southeast-1a"
            }
        ],
        "CreateTime": "2022-01-18T14:28:36+08:00",
        "Description": "",
        "InstanceId": "****",
        "InstanceName": "test",
        "KafkaChargeInfo": {
            "ChargeStatus": "Normal",
            "ChargeSubType": "Monthly",
            "ChargeType": "PostPaid",
            "CreatedTime": 1642487317,
            "OrderId": "********",
            "OverdueTime": 0
        },
        "KafkaEndpoints": [
            {
                "AccessAddress": "kafka-ap-1ddx0b**.kafka.ibytepluses.com:9092",
                "EndpointProtocol": "PLAINTEXT",
                "EndpointType": "Private"
            },
            {
                "AccessAddress": "kafka-ap-1ddx**.kafka.ibytepluses.com:9093",
                "EndpointProtocol": "SASL_PLAINTEXT",
                "EndpointType": "Private"
            }
        ],
        "KafkaParams": [
            {
                "DefaultValue": "10",
                "Description": "Maximum Message Size",
                "Name": "MessageMaxByte",
                "ParamType": "TypeInt",
                "Restart": false,
                "RunningValue": "10",
                "Unit": "MB",
                "ValueRange": "1-12"
            },
            {
                "DefaultValue": "72",
                "Description": "Message Retention Period",
                "Name": "LogRetentionHours",
                "ParamType": "TypeInt",
                "Restart": false,
                "RunningValue": "72",
                "Unit": "h",
                "ValueRange": "0-2160"
            },
            {
                "DefaultValue": "4320",
                "Description": "Log index retention time",
                "Name": "OffsetRetentionMinutes",
                "ParamType": "TypeInt",
                "Restart": false,
                "RunningValue": "4320",
                "Unit": "m",
                "ValueRange": "1-10080"
            },
            {
                "DefaultValue": "12",
                "Description": "The default number of partitions for a topic",
                "Name": "NumPartitions",
                "ParamType": "TypeInt",
                "Restart": false,
                "RunningValue": "12",
                "Unit": "",
                "ValueRange": "1-300"
            },
            {
                "DefaultValue": "3",
                "Description": "The default number of replicas for a topic",
                "Name": "ReplicationFactor",
                "ParamType": "TypeInt",
                "Restart": false,
                "RunningValue": "3",
                "Unit": "",
                "ValueRange": "2-3"
            }
        ],
        "KafkaSpecification": "kafka.n3.x2.small",
        "LimitPartitionNumber": 300,
        "OptimalPartitionNumber": 12,
        "ProjectName": "",
        "Status": "Running",
        "StorageCapacity": 1500,
        "UsedCapacity": 0,
        "UsedGroupNumber": 0,
        "UsedPartitionNumber": 13,
        "UsedTopicNumber": 2,
        "Version": "2.2.2",
        "VpcInfo": {
            "ID": "vpc-****",
            "Name": "mq-test",
            "SubnetId": "****"
        }
    }
}
```
