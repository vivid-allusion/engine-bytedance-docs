---
title: "DescribeInstanceDetail"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeInstanceDetail-v2"
---

Call DescribeInstanceDetail interface to view the details of the specified instance.

<span id="e5c2d0a2"></span>
## Request parameters


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |The Kafka instance ID for the details to be queried. |


<span id="8eb26ddf"></span>
## Response parameter


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|BasicInstanceInfo |BasicInstanceInfo |/ |The name, version and other basic information of the instance. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) Part BasicInstanceInfoObject. |
|ConnectionInfo |Array of EndpointObject |/ |Connection information for the instance. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) in the EndpointObject section. |
|ChargeDetail |ChargeDetailObject |/ |Payment method. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) In the ChargeDetailObject section. |
|Parameters |String |/ |Configuration parameters for the instance. Includes:<br><br><br>* LogAutoDeletion: Whether to automatically delete old messages.<br><br>* LogRetentionHours: Message retention duration. In hours.<br><br>* MessageMaxByte: Maximum message size. The unit is MB.<br><br>* MessageTimestampType: Message time type.<br><br>* OffsetRetentionMinutes: Spend check point retention time. The unit is minutes. |


<span id="408de198"></span>
## Example

<span id="c26c7e0a"></span>
### Request example

```JSON
POST /?Action=DescribeInstanceDetail&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnng3s31v076****"
}
```


<span id="e57ddbf2"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023071923571842DD84CF65A6B2BF84C9",
        "Action": "DescribeInstanceDetail",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "BasicInstanceInfo": {
            "AccountId": "200000****",
            "AutoUseGroup": true,
            "AutoUseTopic": false,
            "ChargeDetail": {
                "ChargeStartTime": "2023-07-19T13:11:15Z",
                "ChargeStatus": "Normal",
                "ChargeType": "PostPaid",
                "OverdueTime": ""
            },
            "ComputeSpec": "kafka.20xrate.hw",
            "CreateTime": "2023-07-19T13:11:14Z",
            "DiskEncrypted": true,
            "EipId": "eip-11vlvmhvc2znk40yrhcye****",
            "InstanceDescription": "",
            "InstanceId": "kafka-cnng3s31v076****",
            "InstanceName": "kafka-cnng3s31v076****",
            "InstanceStatus": "Running",
            "PrivateDomainOnPublic": false,
            "ProjectName": "default",
            "RegionId": "ap-southeast-1",
            "StorageSpace": 300,
            "StorageType": "ESSD_FlexPL",
            "SubnetId": "subnet-36t6c6egvp91c383g0wqf****",
            "UsableGroupNumber": 500,
            "UsablePartitionNumber": 250,
            "UsedGroupNumber": 0,
            "UsedPartitionNumber": 0,
            "UsedStorageSpace": 0,
            "UsedTopicNumber": 0,
            "Version": "2.2.2",
            "VpcId": "vpc-11w4ygf1zls7440yrhcq****",
            "ZoneId": "ap-southeast-1a"
        },
        "ChargeDetail": {
            "ChargeStartTime": "2023-07-19T13:11:15Z",
            "ChargeStatus": "Normal",
            "ChargeType": "PostPaid",
            "OverdueTime": ""
        },
        "ConnectionInfo": [
            {
                "EndpointType": "PLAINTEXT",
                "InternalEndpoint": "kafka-ap-1ddx0b**.kafka.ibytepluses.com:9092",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": ""
            },
            {
                "EndpointType": "SASL_PLAINTEXT",
                "InternalEndpoint": "kafka-ap-1ddx***.kafka.ibytepluses.com:9093",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "kafka-ap-1cnng3s31v076****.kafka.bytepluses.com:9592,kafka-ap-1cnng3s31v076****.kafka.bytepluses.com:9593,kafka-ap-1cnng3s31v076****.kafka.bytepluses.com:9594"
            },
            {
                "EndpointType": "SASL_SSL",
                "InternalEndpoint": "kafka-ap-1cnng3s31v076****.kafka.ibytepluses.com:9095",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "kafka-ap-1cnng3s31v076****.kafka.bytepluses.com:9492,kafka-ap-1cnng3s31v076****.kafka.bytepluses.com:9493,kafka-ap-1cnng3s31v076****.kafka.bytepluses.com:9494"
            }
        ],
        "Parameters": "{\"LogRetentionHours\":\"72\",\"MessageMaxByte\":\"10\",\"MessageTimestampType\":\"CreateTime\",\"OffsetRetentionMinutes\":\"4320\"}"
    }
}
```
