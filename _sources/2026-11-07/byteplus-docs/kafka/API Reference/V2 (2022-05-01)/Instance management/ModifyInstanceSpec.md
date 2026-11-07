---
title: "ModifyInstanceSpec"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/ModifyInstanceSpec-v2"
---

Call the ModifyInstanceSpec interface to modify the calculation specifications, storage specifications, and number of additional partitions of the instance.

<span id="5dd3bb70"></span>
## Instructions for use

As the business scale grows, if the instance specifications no longer meet the requirements, you can appropriately increase the specification configuration of the instance. This interface is used to change the specifications of the Kafka instance, including the configuration of calculation specifications, storage space and number of partitions. The variant interface is an asynchronous interface. After calling the interface, you can check whether the specification parameters such as calculation specifications of the instance have been changed successfully in the console instance details page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before calling this interface, make sure the instance status is Running.</div>


* <div data-tips="true" data-tips-type="tip">Currently only upgrade instance configurations are supported, not downgrades, such as downgrading compute specs or shrinking storage space.</div>


* <div data-tips="true" data-tips-type="tip">Different computing specifications correspond to different storage space ranges. When upgrading the computing specifications of an instance, the storage space needs to be upgraded synchronously.</div>



<span id="e1d4a376"></span>
## **request parameters**


|Parameter |Parameter type |Is it required |Example value |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |kafka\-cnngqkfgdudt\*\*\*\* |Instance ID. |
|ComputeSpec |String |No |Kafka.60xrate.hw |The calculation specification of the instance after the change. If you need to upgrade the calculation specification, this parameter is required. For the list of calculation specifications provided by the message queue Kafka version instance, please refer to [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications).<br><br>Only upgrade instance specifications are supported, not downgrades. |
|StorageSpace |Integer |No |1000 |The storage space after the instance has been changed. If you need to expand the storage space, this parameter is required.<br><br>The unit is GiB and must be specified as a multiple of 100. The value range depends on the currently specified calculation specification, please refer to [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications).<br><br>Only upgrade instance specifications are supported, not downgrades. |
|PartitionNumber |Integer |No |1000 |Number of partitions. To increase the number of partitions, this parameter is required.<br><br>The value range depends on the currently specified calculation specification, please refer to [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications).<br><br><br>* Only increasing the number of partitions is supported.<br><br>* The partition added when upgrading the instance specification will be charged an additional partition fee. Please refer to [Billing items](https://docs.byteplus.com/en/docs/kafka/billable-items). |
|NeedRebalance |Boolean |No |False |Whether to enable rebalancing.<br><br><br>* True: (recommended) message queue Kafka version will rebalance partitions.<br><br>* False: (default) If rebalancing is not enabled, you need to manually add partitions to the original Topic to use the new resources after the upgrade.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You only need to choose whether to rebalance when changing the calculation specification of the instance, and no rebalancing is required only when upgrading the storage specification. That is, this parameter only takes effect when the ComputeSpec parameter is specified.</div><br> |
|RebalanceTime |String |No |2022\-07\-18T07:48:58Z |The execution time of the automatic rebalancing. The time format is YYYYMMDD T'HHMMSS'Z ', for example 2022\-07\-18T07:48:58Z. Should be more than 5 minutes later than the current time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter only takes effect when NeedRebalance is true. If this parameter is not set, the rebalancing task will be executed immediately after the rebalancing is completed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">It is recommended to rebalance at night and other business peaks to reduce the impact of data migration on the business.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If this parameter is not specified, rebalancing is performed immediately after the upgrade.</div><br> |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-426655440000 |An identifier that guarantees client side request idempotency.<br><br>The identifier is a 1\-64\-bit ASCII string, case\-sensitive, generated by the client side, and should ensure that the identifier is unique between different requests.<br><br>How to use the idempotent flag, please refer to [Request Idempotence](https://docs.byteplus.com/en/docs/kafka/Request-Idempotence-v2). |


<span id="f7fd373c"></span>
## **response parameter**


|Parameter |Parameter type |Example value |Description |
|---|---|---|---|
|OrderId |String |order\-712089661643355\*\*\*\* |Order ID. |


<span id="4e2b09e8"></span>
## **example**

<span id="ca7c9f3d"></span>
### **Request example**

```JSON
POST /?Action=ModifyInstanceSpec&Version=2022-05-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
Service: kafka

{
  "InstanceId": "kafka-cnngbnntswg1****",
  "ComputeSpec": "kafka.60xrate.hw",
  "StorageSpace": 300,
  "PartitionNumber": 400
}
```


<span id="39043c10"></span>
### **Response example**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023022721230816131228CB14B15FBB72",
        "Action": "ModifyInstanceSpec",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "OrderId": "Order720482488077238****"
    }
}
```
