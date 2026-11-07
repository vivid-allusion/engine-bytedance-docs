---
title: "CreateKafkaInstance "
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/CreateKafkaInstance-v1"
---

Call the CreateKafkaInstance interface to create a Kafka instance.

<span id="59becfee"></span>
## Instructions for use

The instance is the virtual machine resource of the message queue Kafka Edition service, which is used to manage and store resources such as Topic and Group.


* Version of this API is `2018-01-01`.

* The call frequency of this interface is limited to 20 times/s, and an error "AccountFlowLimitExceeded" will be reported if the frequency limit is exceeded.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When creating an interface through the API, it is not supported to open the public network access function at the same time. If you need to open the public network access of the instance, it is recommended to call the EnableInternetAccess to open the public network access of the instance after the creation of the instance is completed and the instance state is Running.</div>


* <div data-tips="true" data-tips-type="tip">By default, you can create 5 Kafka instances in each region. The total storage capacity of all instances in each region for each account is up to 10TiB. Otherwise, the error "The instance_num/storage_sum has exceeded quota" will be reported when creating the instance. To increase the quota, please click Quota Center submit an application, such as applying to increase the maximum number of instances (InstanceNum) under each region, which can be adjusted up to 10.</div>



<span id="02142bde"></span>
## Request parameters


|**parameter** |**parameter type** |**Is it required?**  |**sample value** |**explain** |
|---|---|---|---|---|
|ZoneId |String |Required |ap\-southeast\-1a |The availability zone where the instance is located.<br><br>Message queue Kafka version supports multi\-Availability Zone deployment of Kafka instances. For regions with 3 or more Availability Zones, you can deploy across Availability Zones by specifying 3 Availability Zones. Multiple Availability Zones are separated by commas (,), for example `cn-guangzhou-a,cn-guangzhou-b`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The multi\-availability zone is deployed as an invitation\-to\-test function in the East China 1 (Guangzhou) region. If you have relevant business needs, please pass ticket system contact technical support to request a whitelist.</div><br> |
|KafkaSpecifications |String |Required |Kafka.n3.x2. small |Calculation specifications. Please refer to the currently supported calculation specifications [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications). |
|DiskCapacity |Integer |Required |1500 |Storage space size, in GiB, step size is 300. you can check [Specifications](https://docs.byteplus.com/en/docs/kafka/specifications) documentation to obtain detailed information on calculation specifications and storage space. |
|NetTypes |List < String \> |Required |[<br><br>"Private"<br><br>], |The network type of the instance. Supported values include:<br><br><br>* Private: (required) Private network VPC access. When setting up to enable VPC access, you need to specify the VPC and subnet corresponding to the instance through VpcId and SubnetId. |
|VpcInfo |JSON Array |Required |*  |For VPC related information, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|Users |String |Required |Test |Kafka instances use the user name of the PLAIN schema. |
|Passwords |String |Required |XXXxiiiiixxx |Kafka instances use user passwords in PLAIN mode. |
|ChargeInfo |JSON Array |Required |*  |Billing information for the instance. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|Region |String |Optional |ap\-southeast\-1 |Region where the instance is located.<br><br>Cross\-Region calls are not supported. The value specified by this parameter needs to be the same as the Region in the header. |
|InstanceName |String |Optional |Kafka |Kafka instance name. The following requirements must be met:<br><br><br>* Can only contain Chinese, English letters, numbers, underscores (_) and hyphens (\-).<br><br>* Cannot start with a number or a hyphen (\-).<br><br>* The length is 0~ 128 characters.<br><br>   When the Kafka instance name is not set, the instance ID will be used as the instance name. |
|Description |String |optional |Instance Description |Descriptive information for the instance. |
|Params |List |optional |*  |Parameters related to Kafka instances. For details, please refer to [Data structure](https://docs.byteplus.com/en/docs/kafka/Data-structure-v1). |
|ProjectName |String |optional |Kafka\-project |The IAM project to which the instance belongs. By default, message queue Kafka Edition does not add instances to any IAM projects. |


<span id="3266dfeb"></span>
## Response parameter


|**parameter** |**parameter type** |**example** |**explain** |
|---|---|---|---|
|InstanceID |String |kafka\-cndvg8bj1q67\*\*\*\* |Instance ID. |
|OrderId |String |Order\-dvsgsgg8 \*\*\*\* |Order ID. |


<span id="6f9647b6"></span>
## Example

<span id="296cc8b3"></span>
### Request example

```json
POST /?Action=CreateKafkaInstance&Version=2018-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com 
Region: ap-southeast-1 
Service: kafka

{
  "Region": "cn-beijing",
  "VpcInfo": {
    "ID": "vpc-testtesttest",
    "Name": "kafka-test",
    "SubnetId": "subnet-xxxxxxxxxx"
   },
  "DiskCapacity": 1500,
  "KafkaSpecification": "kafka.n3.x2.small",
  "NetTypes": [
    "Private"
  ],
  "InstanceName": "kafka-****",
  "ZoneId": "cn-beijing-a",
  "Description": "test",
  "Users": "test",
  "Passwords": "xxxxiiiiiixxx",
  "Params": [
    {
      "Name": "max_byte",
      "RunningValue": "1"
    }
  ],
  "ChargeInfo": {
    "ChargeType": "PostPaid",
    "ChargeSubType": "Monthly",
    "ChargeUnitNum": 1,
    "AutoReNew": false
  },
  "ProjectName": "kafka-project"
}
```


<span id="e36deeea"></span>
### Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "CreateKafkaInstance",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "InstanceID": "kafka-cndvg8bj1q67****",
    "OrderId": "order-*******"
  }
}
```
