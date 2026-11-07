---
title: "ScaleKafkaInstance"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ScaleKafkaInstance-v1"
---

Call ScaleKafkaInstance to change the instance specification.

<span id="3bb6c1cb"></span>
## Instructions for use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before calling this interface, make sure the instance status is Running.</div>


* <div data-tips="true" data-tips-type="tip">Currently only upgrade instance configurations are supported, and downgrading compute specs or shrinking storage space is not supported.</div>


* <div data-tips="true" data-tips-type="tip">Different computing specifications correspond to different storage space ranges. When upgrading the computing specifications of an instance, the storage space needs to be upgraded synchronously.</div>


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<span id="c447bca0"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|InstanceId |String |Required |Kafka\-xxxxxxxxxx |Instance ID. |
|NewKafkaSpecification |String |Optional |Kafka.n5.x2.medina |Instances are updated with new calculation specifications.<br><br><br>* NewKafkaSpecification and NewDiskCapacity, specify at least one.<br><br>* The default is not to perform the calculation specification match. |
|NewDiskCapacity |Integer |optional |1800 |The instance is equipped with a new storage capacity in GiB. Storage specification matching is not performed by default. |
|NeedRebalance |Bool |Optional |False |Whether to perform automatic rebalancing after matching ends.<br><br><br>* True: Instance needs to be rebalanced.<br><br>* False: (default) No rebalancing task is performed. |
|RebalanceTime |String |optional |2022\-03\-15 21:00:00 |The time of automatic rebalancing, the time format is: YYYY\-MM\-DD HH: mm: ss. The default is to trigger the rebalancing task immediately after completion. |
|EipIds |List |Optional |[Eip\-xxxxx, eip\-yyyyy] |EIP ID, required when opening public network access.<br><br><br>* Higher computing specifications require more public IPs. When upgrading the instance specification, you need to pass in the increased public IP ID through this parameter.<br><br>* You can view the number of public IPs required by each instance through the ListKafkaConf interface. |
|PartitionOfBuy |Integer |Optional |900 |The number of partitions for Kafka instances, please set the number of partitions reasonably according to business needs.<br><br>Different specifications provide different numbers of free partitions, and the part exceeding the free quota will be charged separately. Please refer to the range of partitions that can be created for each specification [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications) Please refer to the billing method of the partition [Billing items](https://docs.byteplus.com/en/docs/kafka/billable-items). |


<span id="8aa96bb9"></span>
## Response parameter


|**parameter** |**parameter type** |**sample value** |**explain** |
|---|---|---|---|
|OrderId |String |Order\-xxxxxxx |Instance Order ID. |


<span id="95add3d5"></span>
## Example

<span id="87d7fb3a"></span>
### Request example

```json
POST /?Action=ScaleKafkaInstance&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "InstanceId": "kafka-xxxxxxxxxx",
  "NewKafkaSpecification": "kafka.n5.x2.medinum",
  "NewDiskCapacity": 1800,
  "NeedRebalance": false,
  "RebalanceTime": "2022-03-15 21:00:00",
  "EipIds": [
    "********"
  ]
}
```


<span id="a4e4f045"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "540CFF28-407A-40B5-B6A5-74B",
    "Action": "ScaleKafkaInstance",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "OrderId": "order-xxxxxxx"
  }
}
```
