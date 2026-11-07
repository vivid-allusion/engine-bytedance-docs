---
title: "DescribeInstances"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeInstances-v2"
---

Call the DescribeInstances interface to get the list of instances under the current account.

<span id="ba44d71f"></span>
## Instructions for use

DescribeInstances is a paged query interface that returns a list and overview of Kafka instances that meet the filter criteria. To obtain the details of the specified Kafka instance, you can specify the instance ID to query, or directly use [DescribeInstanceDetail](https://docs.byteplus.com/en/docs/kafka/DescribeInstanceDetail-v2) Interface.

<span id="2ab43cef"></span>
## Request parameters


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|PageSize |Integer |Yes |10 |When the query results are displayed in pages, this parameter is used to represent the amount of data per page. Values range from 1 to 100. |
|PageNumber |Integer |Yes |1 |When the query results are displayed in pages, this parameter is used to represent the page number. The minimum supported value is 1. |
|InstanceId |String |No |kafka\-cnaix6r3hlqv\*\*\*\* |Instance ID. When an instance ID is specified, it means to view the information of the specified instance. At this time, other filters such as InstanceName do not take effect.<br><br>Supports precise queries. |
|InstanceName |String |No |MyInstance |Instance name. Supports fuzzy queries. |
|InstanceStatus |String |No |Running |The current state of the instance. |
|ZoneId |String |No |ap\-southeast\-1a |The ID of the Availability Zone where the instance is located.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Notice</div><br><br><br><div data-tips="true" data-tips-type="tip">Message queue Kafka Edition instances support cross\-AZ deployments. You can specify multiple Availability Zones when viewing which compute specifications are available under Specify Availability Zones. Multiple Availability Zones are separated by comma (,) IDs.</div><br><br><br><div data-tips="true" data-tips-type="tip">You can call <a href="https://docs.byteplus.com/en/docs/kafka/DescribeAvailabilityZones-v2">DescribeAvailabilityZones</a> Query the list of availability zones currently served.</div><br> |
|Tags |Map < String, Array of Strings \> |No | |The label of the instance. |
|Project |String |No |testProject |Filter according to the IAM project to which the instance belongs. When this parameter is not specified, a list of instances with viewing permissions for this operation account is returned. |


<span id="b4c2b9c1"></span>
## Response parameter


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|Total |Integer |1 |Total number of instances. |
|InstancesInfo |Array of BasicInstanceInfoObject |/ |The name, version and other basic information of the instance. For details, please refer to [Data Structure](https://docs.byteplus.com/en/docs/kafka/Data-Structure-v2) Part BasicInstanceInfoObject. |


<span id="476116a5"></span>
## Example

<span id="e9baabc7"></span>
### Request example

```JSON
POST /?Action=DescribeInstances&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "PageSize": 10,
  "PageNumber": 1
}
```


<span id="7ee18f05"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202302271712000AE823263252****4A",
        "Action": "DescribeInstances",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstancesInfo": [
            {
                "AccountId": "2000006376",
                "ChargeDetail": {
                    "ChargeStartTime": "2022-07-18T07:48:58Z",
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid",
                    "OverdueTime": ""
                },
                "ComputeSpec": "kafka.20xrate.hw",
                "CreateTime": "2022-07-18T07:48:58Z",
                "DiskEncrypted": false,
                "EipId": "eip-13g3hg4mzvy0w3n6nu44b****",
                "InstanceDescription":"Test instance",
                "InstanceId": "kafka-cnngc7an0qpv****",
                "InstanceName": "new-instance",
                "InstanceStatus": "Running",
                "PrivateDomainOnPublic": false,
                "ProjectName": "",
                "RegionId": "ap-southeast-1",
                "StorageSpace": 600,
                "StorageType": "ESSD_FlexPL",
                "SubnetId": "subnet-rrsenz6y5iwwv0x58eg****",
                "UsablePartitionNumber": 564,
                "UsedGroupNumber": 6,
                "UsedPartitionNumber": 36,
                "UsedStorageSpace": 3,
                "UsedTopicNumber": 6,
                "Version": "2.2.2",
                "VpcId": "vpc-13fz1ktl52dc03n6nu55w****",
                "ZoneId": "ap-southeast-1a"
            }
        ],
        "Total": 1
    }
}
```
