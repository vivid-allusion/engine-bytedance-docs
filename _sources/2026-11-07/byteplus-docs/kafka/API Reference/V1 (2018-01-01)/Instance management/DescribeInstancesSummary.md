---
title: "DescribeInstancesSummary"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/DescribeInstancesSummary-v1"
---

Call DescribeInstancesSummary interface to get the list of instances under the current account.

<span id="8f3fdfd8"></span>
## Instructions for use

The Query Instance List provides a paged query interface that returns only an overview of Kafka instances. For more information, use the DescribeInstanceDetail interface.


* Version of this API is `2018-01-01`.

* The calling frequency of this interface is limited to 100 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="6f350d9f"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|PageNumber |Integer |Required |1 |The page number to query. Values range from non\-zero integers. |
|PageSize |Integer |Required |10 |The size of the single page to be queried. Values range from 1 to 50. |
|Filters |List |Optional |*  |Filter fields used by the instance query. Currently supported filter fields are:<br><br><br>* Name: instance name filter, fuzzy match.<br><br>* InstanceId: instance ID filtering, fuzzy matching. |
|SortFiledName |String |Optional |Name |Instance query result sorting field. Status is used for sorting by default. Can be set to:<br><br><br>* Name: Instance name<br><br>* InstanceID: instance ID<br><br>* Status: instance status<br><br>* CreateTime: Instance creation time<br><br>* UsedTopicNum: Number of Topics for instances |
|SortOrder |String |Optional |Asc |The sort used by the instance query. Defaults to ascending order.<br><br><br>* Asc: ascending<br><br>* Desc: Descending order. |


<span id="15b9f38b"></span>
## Response parameter


|**parameter** |**parameter type** |**explain** |
|---|---|---|
|Total |Integer |Number of instances. |
|Instances |List |List of instance information. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |


<span id="7afa84fb"></span>
## Example

<span id="340ed835"></span>
### Request example

```json
POST /?Action=DescribeInstancesSummary&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "PageNumber": 1,
  "PageSize": 1,
  "Filters": [
    {
      "Name": "Name",
      "Values": [
        ""
      ]
    }
  ],
  "SortFiledName": "",
  "SortOrder": "Asc"
}
```


<span id="1503968b"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeInstancesSummary",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
        "Instances": [
            {
                "AccountId": 2000006376,
                "AvaliableZones": [
                    {
                        "ZoneId": "ap-southeast-1a",
                        "ZoneIdInChinese": "Availability Zone A:ap-southeast-1a"
                    }
                ],
                "CreateTime": "2022-01-18T14:28:36+08:00",
                "Description": "",
                "InstanceId": "kafka-******",
                "InstanceName": "kafka",
                "KafkaChargeInfo": {
                    "ChargeStatus": "Normal",
                    "ChargeSubType": "Monthly",
                    "ChargeType": "PostPaid",
                    "CreatedTime": 1642487317,
                    "OrderId": "******",
                    "OverdueTime": 0
                },
                "KafkaSpecification": "kafka.n3.x2.small",
                "ProjectName": "",
                "Status": "Running",
                "UsedGroupNumber": 0,
                "UsedTopicNumber": 2,
                "VpcInfo": {
                    "ID": "vpc-******",
                    "Name": "mq-test",
                    "SubnetId": "******"
                }
            }
        ],
        "Total": 3
    }
```
