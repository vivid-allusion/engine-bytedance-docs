---
title: "ListKafkaConf"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ListKafkaConf-v1"
---

Call the ListKafkaConf interface to obtain the relevant configuration supported by the message queue Kafka version.

<span id="0c955bb4"></span>
## Instructions for use

Before creating the message queue Kafka version, you can obtain the configuration supported by the Kafka instance through this interface, such as network configuration, specification information, availability zone, etc.


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="d9962159"></span>
## Request parameters

None

<span id="4f3674b8"></span>
## Response parameter


|**parameter** |**type** |**explain** |
|---|---|---|
|AvailableVersions |String |List of all supported Kafka versions. |
|ChargeTypes |String |The billing methods currently supported by the Kafka service.<br><br><br>* PostPaid: Billed on demand<br><br>* PrePaid: Annual/Monthly |
|InstanceParams |List |A list of Kafka parameters that can be configured for the purchase instance. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|InstanceSpec |List |For all available Kafka instance specifications, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|NetType |List < String \> |All supported Kafka instance network types.<br><br><br>* Private: Private network VPC access.<br><br>* Internet: Public network access. |
|ZoneInfos |List |Availability zone information that can be selected for the purchase instance. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="3537dd12"></span>
## Example

<span id="9e1c2849"></span>
### Request example

```json
POST /?Action=ListKafkaConf&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka
```


<span id="9efaa183"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "******",
    "Action": "ListKafkaConf",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1 "
  },
  "Result": {
        "AvailableVersions": [
            "2.2.2"
        ],
        "ChargeTypes": [
            "PostPaid"
        ],
        "InstanceParams": [
            {
                "DefaultValue": "10",
                "Description": "Maximum Message Size",
                "Name": "MessageMaxByte",
                "PType": "TypeInt",
                "Restart": false,
                "RunningValue": "10",
                "Unit": "MB",
                "ValueRange": "1-12"
            },
            {
                "DefaultValue": "72",
                "Description": "Message Retention Period",
                "Name": "LogRetentionHours",
                "PType": "TypeInt",
                "Restart": false,
                "RunningValue": "72",
                "Unit": "h",
                "ValueRange": "0-2160"
            },
            {
                "DefaultValue": "4320",
                "Description": "Log index retention time",
                "Name": "OffsetRetentionMinutes",
                "PType": "TypeInt",
                "Restart": false,
                "RunningValue": "4320",
                "Unit": "m",
                "ValueRange": "1-10080"
            },
            {
                "DefaultValue": "12",
                "Description": "The default number of partitions for a topic",
                "Name": "NumPartitions",
                "PType": "TypeInt",
                "Restart": false,
                "RunningValue": "12",
                "Unit": "",
                "ValueRange": "1-300"
            },
            {
                "DefaultValue": "3",
                "Description": "The default number of replicas for a topic",
                "Name": "ReplicationFactor",
                "PType": "TypeInt",
                "Restart": false,
                "RunningValue": "3",
                "Unit": "",
                "ValueRange": "2-3"
            },
            {
                "DefaultValue": "true",
                "Description": "Data is automatically deleted",
                "Name": "LogAutoDeletion",
                "PType": "TypeString",
                "Restart": false,
                "RunningValue": "true",
                "Unit": "",
                "ValueRange": "0-1"
            }
        ],
        "InstanceSpec": [
            {
                "DiskIncStep": 300,
                "DiskMaxSize": 90000,
                "DiskMinSize": 600,
                "ElasticIpNumber": 3,
                "IsSoldOut": {
                    "cn-beijing-a": false
                },
                "MaxPartitionNumber": 3000,
                "PartitionNum": 300,
                "SpecName": "kafka.n3.x2.small"
            },
            {
                "DiskIncStep": 300,
                "DiskMaxSize": 90000,
                "DiskMinSize": 1800,
                "ElasticIpNumber": 5,
                "IsSoldOut": {
                    "cn-beijing-a": false
                },
                "MaxPartitionNumber": 3000,
                "PartitionNum": 900,
                "SpecName": "kafka.n5.x2.medium"
            },
            {
                "DiskIncStep": 300,
                "DiskMaxSize": 90000,
                "DiskMinSize": 2400,
                "ElasticIpNumber": 5,
                "IsSoldOut": {
                    "ap-southeast-1a": true
                },
                "MaxPartitionNumber": 5000,
                "PartitionNum": 1800,
                "SpecName": "kafka.n5.x2.large"
            }
        ],
        "NetType": [
            "Private"
        ],
        "ZoneInfos": [
            {
                "Zone": {
                    "Desc": "ap-southeast-1a",
                    "ID": "ap-southeast-1a",
                    "IsSoldOut": false,
                    "Value": "ap-southeast-1a"
                }
            }
        ]
    }
}
```
