---
title: "DescribeInstances - Get the current instances list"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DescribeInstances_-_Get_the_current_instances_list"
---

Call the DescribeInstances API to get the list of instances under the current account.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

DescribeInstances is a paginated query API. It returns the list and overview information of Message Queue for RabbitMQ instances matching the filter criteria. To get detailed information for a specific Message Queue for RabbitMQ instance, specify the instance ID for query or directly use the [DescribeInstanceDetail](https://docs.byteplus.com/en/docs/rabbitmq/DescribeInstanceDetail_-_Query_instance_details) API.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 100 times/second. The per\-user request frequency limit is 20 times/second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstances&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|Rf0W5a">必选</span> `Example value: DescribeInstances`

Action to execute, value: DescribeInstances.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|SxT02A">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**PageNumber** <span data-label="purple">integer</span> <span data-api-tag="require|D8QiM4">必选</span> `Example value: 1`

This parameter represents the page number when query results are paginated. The minimum supported value is 1.



**PageSize** <span data-label="purple">integer</span> <span data-api-tag="require|ztatYW">必选</span> `Example value: 10`

This parameter indicates the amount of data per page when displaying paged query results. The value range is 1 to 100.



**VpcId** <span data-label="purple">string</span> `Optional` `Example: myvpc`

The VPC name where the instance is located. Supports fuzzy matching.



**ChargeType** <span data-label="purple">string</span> `Optional` `Example value: PostPaid`

The instance's payment type. Exact query. Supports the following settings:


* PostPaid: pay\-as\-you\-go

* PrePaid: Subscription



**ZoneId** <span data-label="purple">string</span> `Optional.` `Example value: cn-beijing-a`

Availability zone ID of the instance. Fuzzy match.



**InstanceStatus** <span data-label="purple">string</span> `Optional` `Example value: Running`

Current status of the instance. Precise query.



**InstanceName** <span data-label="purple">string</span> `Optional` `Example value: test-instance`

Instance name. Supports fuzzy matching.



**Spec** <span data-label="purple">string</span> `Optional` `Example value: rabbitmq.n3.x2.medium`

Instance specifications. Exact query.

The specification list for Message Queue for RabbitMQ instances is provided. Please refer to the [product specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications).



**ProjectName** <span data-label="purple">string</span> `Optional` `Example value: default`

Filter based on the IAM project to which the instance belongs. If this parameter is not specified, it returns the instances with viewing permission of this operation account.



**TagFilters** <span data-label="purple">object[]</span> `Optional` `Example value: /`

Filter instances by their tags.


**Key** <span data-label="purple">string</span> <span data-api-tag="require|mhfMCJ">必选</span> `Example value: owner`

tag key



**Value** <span data-label="purple">string</span> `Optional` `Example value: zhangsan`

Tag value.




**InstanceId** <span data-label="purple">string</span> `Optional` `Example value: rbtmq-5b293870****`

Instance ID. Specifying the instance ID retrieves information of the specified instance. Other filters like InstanceName do not apply. Supports fuzzy matching.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Total** <span data-label="purple">integer</span> `Example value: 2`

Total number of instances.



**InstancesInfo** <span data-label="purple">object[]</span> `Example value: /`

Basic information such as the instance name and version.


**InstanceDescription** <span data-label="purple">string</span> `Example value: this is a test instance`

Simple description of the instance.



**InstanceStatus** <span data-label="purple">string</span> `Example: Running`

Instance status.



**InstanceName** <span data-label="purple">string</span> `Example value: RabbitMQinstance`

Name of the RabbitMQ instance.



**UsedStorageSpace** <span data-label="purple">integer</span> `Example value: 100`

The instance has used storage space. Unit: GiB.



**StorageSpace** <span data-label="purple">integer</span> `Example value: 200`

Total instance storage space in GiB.



**InstanceId** <span data-label="purple">string</span> `Example value: rabbitmq-cnngqkfgdudt****`

RabbitMQ instance ID.



**RegionId** <span data-label="purple">string</span> `Example value: cn-guangzhou`

Region ID where the instance is located.



**Version** <span data-label="purple">string</span> `Example value: 3.8.18`

Supported RabbitMQ versions. Currently supported versions include:


* 3.8.18: RabbitMQ version 3.8.18.



**ZoneId** <span data-label="purple">string</span> `Example value: cn-guangzhou-a`

Availability zone ID where the instance is located. For high availability instances across AZs, multiple availability zone IDs will be returned here.



**RegionDescription** <span data-label="purple">string</span> `Example value: South China 1 (Guangzhou)`

Description information of the region.



**ApplyPrivateDNSToPublic** <span data-label="purple">boolean</span> `Example value: true`

Indicates whether the public network parse function is enabled.


* true: enabled

* false: disabled



**ChargeDetail** <span data-label="purple">object</span> `Example value: /`

Billing information such as the instance's billing method.


**ChargeType** <span data-label="purple">string</span> `Example value: PostPaid`

The billing method for the instance. Supported types include:


* PostPaid: pay\-as\-you\-go

* PrePaid: Subscription



**ChargeStatus** <span data-label="purple">string</span> `Example value: Normal`

Instance billing status. Includes:


* Normal: normal

* Overdue: pay\-as\-you\-go arrears

* Expired: subscription expired



**ChargeStartTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

The instance's billing start time, formatted as YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**OverdueReclaimTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

The expected release time after the instance is suspended due to overdue payment. The time format is YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**OverdueTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

Shutdown time of overdue instance. The time display format is YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**ChargeExpireTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

Expiration time of the subscription instance. The time format is YYYY\-MM\-DD'T'HH:MM:SS'Z'.

This parameter is returned only for subscription instances.



**AutoRenew** <span data-label="purple">boolean</span> `Example value: true`

Whether to auto\-renew the subscription instance after expiration.


* true: Auto\-renewal enabled.

* false: Auto\-renewal disabled. Manual renewal is required after expiration. Otherwise, the instance will be shut down.



**ChargeEndTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

The instance's billing end time, displayed in the format YYYY\-MM\-DD'T'HH:MM:SS'Z'.




**ArchType** <span data-label="purple">string</span> `Example value: Cluster`

Type of instance, either cluster or stand alone.


* SingleNode: single\-node version

* Cluster: cluster version



**IsEncrypted** <span data-label="purple">boolean</span> `Example value: false`

Whether cloud disk encryption is enabled.


* Cloud disk encryption is an invite\-only feature. To use it, contact technical support to request whitelist access.

* This field is returned only by the DescribeInstanceDetail API.



**InitUserName** <span data-label="purple">string</span> `Example value: Admin`

RabbitMQ WebUI administrator username.



**EipId** <span data-label="purple">string</span> `Example value: eip-mjhulvqza6805smt1bnc****`

ID of the EIP. If the instance does not enable public network access, this parameter will not be returned.



**ComputeSpec** <span data-label="purple">string</span> `Example value: rabbitmq.n3.x2.medium`

Computing specifications of RabbitMQ instance

You can query the computing specifications for sale in a specified availability zone through the DescribeComputeSpecsInfo API.



**ProjectName** <span data-label="purple">string</span> `Example value: newproject`

IAM project the instance belongs to. If the instance does not belong to any IAM project, this parameter will not be returned.



**AccountId** <span data-label="purple">string</span> `Example value: 20000`

Create Instance BytePlus main account ID.



**ZoneDescription** <span data-label="purple">string</span> `Example value: South China 1 (Guangzhou) - availability zone B`

Description of the availability zone



**VpcId** <span data-label="purple">string</span> `Example value: vpc-13fo9gkz6j6683n6nu5ec****`

Private network (VPC) ID.



**SubnetId** <span data-label="purple">string</span> `Example value: subnet-min6uy01kuf45smt1a2i****`

Subnet ID of the VPC.



**CreateTime** <span data-label="purple">string</span> `Example value: 1654485759`

Instance creation time. The time format is YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**Tags** <span data-label="purple">object[]</span> `Example value: /`

Tags of the instance.


**Key** <span data-label="purple">string</span> `Example value: owner`

Tag key.



**Value** <span data-label="purple">string</span> `Example value: zhangsan`

Tag value.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DescribeInstances&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
    "PageSize":10,
    "PageNumber":1
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230217143155B04E2C25D739C689****",
        "Action": "DescribeInstances",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstancesInfo": [
            {
                "ArchType": "Cluster",
                "ChargeDetail": {
                    "ChargeEndTime": "1970-01-01 08:00:00 +0800 CST",
                    "ChargeStartTime": "2022-05-31 18:47:38 +0800 CST",
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid"
                },
                "ComputeSpec": "rabbitmq.n3.x2.medium",
                "CreateTime": "1653994058",
                "InstanceDescription": "",
                "InstanceId": "rbtmq-928c0619****",
                "InstanceName": "Do not delete",
                "InstanceStatus": "Running",
                "ProjectName": "default",
                "RegionDescription": "",
                "RegionId": "cn-beijing",
                "StorageSpace": 500,
                "SubnetId": "subnet-13fvfm1q5rpq83n6nu5ep****",
                "UsedStorageSpace": 11,
                "Version": "3.8.18",
                "VpcId": "vpc-rs5811nceqyov0x58x4****",
                "ZoneDescription": "China (Beijing) - Availability Zone A",
                "ZoneId": "cn-beijing-a"
            },
            {
                "ArchType": "Cluster",
                "ChargeDetail": {
                    "ChargeEndTime": "1970-01-01 08:00:00 +0800 CST",
                    "ChargeStartTime": "2022-06-29 11:10:05 +0800 CST",
                    "ChargeStatus": "Normal",
                    "ChargeType": "PostPaid"
                },
                "ComputeSpec": "rabbitmq.n3.x2.medium",
                "CreateTime": "1656472205",
                "InstanceDescription": "",
                "InstanceId": "rbtmq-5b293870****",
                "InstanceName": "Do not delete-azB",
                "InstanceStatus": "Running",
                "ProjectName": "default",
                "RegionDescription": "",
                "RegionId": "cn-beijing",
                "StorageSpace": 1000,
                "SubnetId": "subnet-rs302h1mqrr4v0x57kq****",
                "Tags": {
                    "Do not delete-wzy": "123123"
                },
                "UsedStorageSpace": 19,
                "Version": "3.8.18",
                "VpcId": "vpc-rs5811nceqyov0x58x4****",
                "ZoneDescription": "China (Beijing) - Availability Zone B",
                "ZoneId": "cn-beijing-b"
            }
        ],
        "Total": 2
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |Parameter value of  %s is invalid. |
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
