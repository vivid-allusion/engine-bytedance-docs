---
title: "DescribeInstanceDetail - Query instance details"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/DescribeInstanceDetail_-_Query_instance_details"
---

Call the DescribeInstanceDetail API to view details of a specified instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to **100 times/second**; the per\-user request frequency limit is **20 times/second**.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceDetail&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|yw4Piz">必选</span> `Example value: DescribeInstanceDetail`

The action to perform, value: DescribeInstanceDetail.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|jhwrC7">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|lmgema">必选</span> `Example value: rbtmq-5b293870****`

The RabbitMQ instance ID to query details for.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**BasicInstanceInfo** <span data-label="purple">object</span> `Example value: /`

Basic information such as the instance name and version.


**InstanceDescription** <span data-label="purple">string</span> `Example value: This is a test instance`

A brief description of the instance.



**InstanceStatus** <span data-label="purple">string</span> `Example value: Running`

Instance running status.



**InstanceName** <span data-label="purple">string</span> `Example: RabbitMQinstance`

Name of the RabbitMQ instance.



**UsedStorageSpace** <span data-label="purple">integer</span> `Example value: 100`

Storage space used by the instance. Unit: GiB.



**StorageSpace** <span data-label="purple">integer</span> `Example value: 200`

Total storage space of the instance, in GiB.



**InstanceId** <span data-label="purple">string</span> `Example value: rabbitmq-cnngqkfgdudt****`

RabbitMQ instance ID.



**RegionId** <span data-label="purple">string</span> `Example: cn-guangzhou`

Region ID of the instance.



**Version** <span data-label="purple">string</span> `Example: 3.8.18`

Supported RabbitMQ versions. Currently supported versions include:


* 3.8.18: RabbitMQ version 3.8.18.



**ZoneId** <span data-label="purple">string</span> `Example value: cn-guangzhou-a`

Availability zone of the instance. For high\-availability instances across AZs, multiple availability zone IDs are returned here.



**RegionDescription** <span data-label="purple">string</span> `Example: South China 1 (Guangzhou)`

Description information of the region.



**ApplyPrivateDNSToPublic** <span data-label="purple">boolean</span> `Example value: true`

Indicates whether public network parse is enabled.


* true: enabled

* false: closed



**ChargeDetail** <span data-label="purple">object</span> `Example value: /`

Billing details of the instance, such as billing method.


**ChargeType** <span data-label="purple">string</span> `Example value: PostPaid`

Billing method for the instance. Supported types include:


* PostPaid: pay\-as\-you\-go

* PrePaid: Subscription



**ChargeStatus** <span data-label="purple">string</span> `Example value: Normal`

Billing status of the instance. Includes:


* Normal: normal

* Overdue: pay\-as\-you\-go overdue

* Expired: subscription expired



**ChargeStartTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

The start billing time of the instance, formatted as YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**OverdueReclaimTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

Estimated release time after instance suspension due to arrears. The time format is displayed as YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**OverdueTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

Instance overdue shutdown time. Time format: YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**ChargeExpireTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

Expiration time of the Subscription instance. The time format is YYYY\-MM\-DD'T'HH:MM:SS'Z'.

This parameter is returned only for subscription instances.



**AutoRenew** <span data-label="purple">boolean</span> `Example: true`

Whether to auto\-renew the Subscription instance upon expiration.


* true: auto\-renew.

* false: no auto\-renew. Manual renewal is required after expiration. Otherwise, the instance will be stopped.



**ChargeEndTime** <span data-label="purple">string</span> `Example value: 2022-01-02T15:04:05Z07:00`

End billing time of the instance, displayed in the format YYYY\-MM\-DD'T'HH:MM:SS'Z'.




**ArchType** <span data-label="purple">string</span> `Example value: Cluster`

The type of instance, either Cluster edition or stand alone edition.



**IsEncrypted** <span data-label="purple">boolean</span> `Example value: false`

Whether cloud disk encryption is enabled.


* Cloud disk encryption is an invited test function. To use it, contact technical support to request whitelist access.

* This field is only returned by the DescribeInstanceDetail API.



**InitUserName** <span data-label="purple">string</span> `Example value: Admin`

The RabbitMQ WebUI administrator username.



**EipId** <span data-label="purple">string</span> `Example value: eip-mjhulvqza6805smt1bnc****`

ID of the EIP. This parameter is not returned if the instance does not enable public network access.



**ComputeSpec** <span data-label="purple">string</span> `Example value: rabbitmq.n3.x2.medium`

Computing specifications of RabbitMQ instance

You can query the computing specifications sold in specified availability zones through the DescribeComputeSpecsInfo interface.



**ProjectName** <span data-label="purple">string</span> `Example value: newproject`

IAM project the instance belongs to. If the instance does not belong to any IAM project, this parameter is not returned.



**AccountId** <span data-label="purple">string</span> `Example value: 20000`

ID of the BytePlus main account that creates the instance



**ZoneDescription** <span data-label="purple">string</span> `Example value: South China 1 (Guangzhou) - availability zone B`

Description of the availability zone



**VpcId** <span data-label="purple">string</span> `Example value: vpc-13fo9gkz6j6683n6nu5ec****`

Private network (VPC) ID.



**SubnetId** <span data-label="purple">string</span> `Example value: subnet-min6uy01kuf45smt1a2i****`

The subnet ID of the VPC.



**CreateTime** <span data-label="purple">string</span> `Example value: 1654485759`

Instance creation time. Time format is YYYY\-MM\-DD'T'HH:MM:SS'Z'.



**Tags** <span data-label="purple">object[]</span> `Example value: /`

Tags of the instance.


**Key** <span data-label="purple">string</span> `Example value: owner`

Tag key.



**Value** <span data-label="purple">string</span> `Example: zhangsan`

tag value.





**Endpoints** <span data-label="purple">object[]</span> `Example: /`

Instance connection information.


**EndpointType** <span data-label="purple">string</span> `Example value: WEB`

Type of the instance's access point. For detailed information about access points, see [Access Points](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).

RabbitMQ instance provides the following types of access points:


* WEB: Web UI endpoint

* AMQP0_9_1: AMQP access point

* MQTT: MQTT access point

* WEB_MQTT: Web MQTT access point

* STOMP: Stomp access point



**NetworkType** <span data-label="purple">string</span> `Example value: PrivateNetwork`

The network type of the access point. PrivateNetwork indicates a private network VPC.



**InternalEndpoint** <span data-label="purple">string</span> `Example value: rbtmq-322db6ab****.rabbitmq.ivolces.com:5672`

Instance's private network access domain name.



**PublicEndpoint** <span data-label="purple">string</span> `Example value: rbtmq-322db6ab****.rabbitmq.volces.com:5671`

Instance public network access domain name. Displayed only after enabling public network access.



**InternalIpEndpoint** <span data-label="purple">string</span> `Example value: 10.249.15.63:5672`

Public service area IP access point.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DescribeInstanceDetail&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
    "InstanceId": "rbtmq-bdb8a520****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20230220223226D0ACEF02D32FFCE8AB00",
        "Action": "DescribeInstanceDetail",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "BasicInfo": {
            "ApplyPrivateDNSToPublic": false,
            "ArchType": "Cluster",
            "ChargeDetail": {
                "ChargeStartTime": "1654485759",
                "ChargeStatus": "Normal",
                "ChargeType": "PostPaid"
            },
            "ComputeSpec": "rabbitmq.n3.x2.medium",
            "CreateTime": "1654485759",
            "EipId": "eip-3ez7smk9xdszk72200swh****",
            "InitUserName": "wangziyi",
            "InstanceDescription": "",
            "InstanceId": "rbtmq-4e688d7d****",
            "InstanceName": "Do not delete-azA",
            "InstanceStatus": "Running",
            "IsEncrypted": false,
            "ProjectName": "default",
            "RegionDescription": "China (Guangzhou)",
            "RegionId": "cn-guangzhou",
            "StorageSpace": 1000,
            "SubnetId": "subnet-3ezlsilsuu68072200t33****",
            "UsedStorageSpace": 346,
            "Version": "3.8.18",
            "VpcId": "vpc-11woocw780tfk40yrhcc2****",
            "ZoneDescription": "China (Guangzhou) - Availability Zone A",
            "ZoneId": "cn-guangzhou-a"
        },
        "Endpoints": [
            {
                "EndpointType": "WEB",
                "InternalEndpoint": "http://rbtmq-4e688d7d****.rabbitmq.ibytepluses.com:15672",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "https://rbtmq-4e688d7d****.rabbitmq.bytepluses.com:15671"
            },
            {
                "EndpointType": "AMQP0_9_1",
                "InternalEndpoint": "rbtmq-4e688d7d****.rabbitmq.ibytepluses.com:5672",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "rbtmq-4e688d7d****.rabbitmq.bytepluses.com:5671"
            },
            {
                "EndpointType": "MQTT",
                "InternalEndpoint": "rbtmq-4e688d7d****.rabbitmq.ibytepluses.com:1883",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "rbtmq-4e688d7d****.rabbitmq.bytepluses.com:8883"
            },
            {
                "EndpointType": "WEB_MQTT",
                "InternalEndpoint": "ws://rbtmq-4e688d7d****.rabbitmq.ibytepluses.com:15675",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "wss://rbtmq-4e688d7d****.rabbitmq.bytepluses.com:15676"
            },
            {
                "EndpointType": "STOMP",
                "InternalEndpoint": "rbtmq-4e688d7d****.rabbitmq.ibytepluses.com:61613",
                "NetworkType": "PrivateNetwork",
                "PublicEndpoint": "rbtmq-4e688d7d****.rabbitmq.bytepluses.com:61614"
            }
        ]
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is not valid. |Parameter value %s is invalid. |
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You are not authorized. Please authorize or switch accounts and try again. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
