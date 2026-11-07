---
title: "CreateInstance - Create instance"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Create_Instance_-_Create_instance"
---

Call CreateInstance to create a Message Queue for RabbitMQ instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

An instance is a virtual machine resource of the Message Queue for RabbitMQ service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If creating a RabbitMQ instance for the first time, you must complete cross\-service access authorization first. We recommend that you use the BytePlus main account to perform this. For details, refer to <a href="https://docs.byteplus.com/en/docs/kafka/cross-service-authorization">Cross\-service access authorization</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you need to access the message queue for RabbitMQ instance through a private network, first create an ECS cloud server, private network, and subnet in the same region. After creating instance, you can not change its private network and subnet.</div>


* <div data-tips="true" data-tips-type="tip">If you need to access the Message Queue Kafka instance via a public network, first apply for an EIP in the same region. For detailed operation steps, refer to <a href="https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP">apply for Elastic IP</a>.</div>


* <div data-tips="true" data-tips-type="tip">By default, you can create 5 RabbitMQ instances in each region. To increase quotas, apply in the <a href="https://console.byteplus.com/quota/productList/coParameterList?ServiceCode=Kafka&ProviderCode=RabbitMQ">Quota Center</a> to raise the maximum number of instances per region (InstanceNum), up to 10.</div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Request frequency: This API limits requests to 100 times per second; the per\-user request frequency limit is 20 times per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateInstance&groupName=%E5%AE%9E%E4%BE%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|AQ4ERR">必选</span> `example value: CreateInstance`

Actions to perform, values: CreateInstance.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|W7VvBt">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**UserName** <span data-label="purple">string</span> <span data-api-tag="require|AotecQ">必选</span> `Example value: Test1`

User name. The following requirements must be met:


* Can only include English letters, numbers, hyphens (\-), or underscores (_).

* Length should be 3 to 64 characters.



**ComputeSpec** <span data-label="purple">string</span> <span data-api-tag="require|p8LPAO">必选</span> `Example value: rabbitmq.n3.x2.medium`

Instance specifications.

The list of computing specifications provided by Message Queue for RabbitMQ instances. See [product specifications](https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications) for details.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|TdGZae">必选</span> `Example: 3.8.18`

Supported RabbitMQ versions. Currently supported versions include:


* 3.8.18: RabbitMQ version 3.8.18.

* 3.12: RabbitMQ version 3.12.



**ZoneId** <span data-label="purple">string</span> <span data-api-tag="require|HaTYkB">必选</span> `Example value: cn-beijing-a`

Availability zone ID of the instance.

Message Queue for RabbitMQ instances support cross\-availability zone deployment. When checking which specifications are available in designated zones, you can specify multiple availability zones. Separate multiple availability zone IDs with commas (,).

You can call [DescribeAvailabilityZones](https://docs.byteplus.com/en/docs/rabbitmq/DescribeAvailabilityZones_-_View_the_availability_zone_list) to query the list of currently available zones.



**UserPassword** <span data-label="purple">string</span> <span data-api-tag="require|Im8mtY">必选</span> `Example: Test@123456`

User password. Must meet the following requirements:


* Length between 8 and 32 characters.

* Composed of any three types among uppercase letters, lowercase letters, numbers, and special characters.

* Supported special characters include `!@#$%^&*()_+-=`.



**StorageSpace** <span data-label="purple">integer</span> <span data-api-tag="require|5hIkkL">必选</span> `Example value: 1000`

Instance storage space.

Unit is GiB and must be specified in multiples of 100. The value range and default depend on the currently specified compute specification.



**InstanceName** <span data-label="purple">string</span> `No` `Example: Name123`

Name of the RabbitMQ instance.  The following requirements must be met:


* Can only contain Chinese characters, letters, numbers, underscores (_), and hyphens (\-).

* Cannot start with a number or hyphen (\-).

* The length of characters ranges from 1 to 128.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no name is specified when creating the instance, the instance ID will be used as the instance name by default.</div>




**EipId** <span data-label="purple">string</span> `No` `Example value: eip-mjhulvqza6805smtxxxx`

The ID of the EIP.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Specifying EipId enables public network access for the instance.</div>


* <div data-tips="true" data-tips-type="tip">An EIP provides independent public IP resources, including a public IP address and outbound bandwidth service. When this parameter is specified to enable public network access, the public address will bind to your Elastic IP (EIP), and fees are charged by the EIP.</div>




**SubnetId** <span data-label="purple">string</span> <span data-api-tag="require|xikkdj">必选</span> `Example value: subnet-min6uy01kuf45sxxxxx`

VPC subnet ID where the instance is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the instance is created, the associated private network and subnet cannot be changed. Choose carefully when creating the instance.</div>


* <div data-tips="true" data-tips-type="tip">You can call the DescribeVpcs API of the private network (VPC) to query the available VPC and subnet lists.</div>




**ChargeInfo** <span data-label="purple">object</span> <span data-api-tag="require|Mj0BuR">必选</span> `Example value: /`

Billing information such as the billing method of the RabbitMQ instance.


**ChargeType** <span data-label="purple">string</span> <span data-api-tag="require|5ATE7Y">必选</span> `Example value: PostPaid`

Billing method of the instance. Supported types include:


* PostPaid: pay\-as\-you\-go

* PrePaid: subscription

   When set to PrePaid, AutoRenew, PeriodUnit, and Period must also be specified.



**AutoRenew** <span data-label="purple">boolean</span> `No` `example value: false`

whether to auto\-renew after the subscription instance expires.


* true: auto\-renew.

* false: do not auto\-renew. Manual renewal is required after expiration. Otherwise, the instance will be shut down.



**PeriodUnit** <span data-label="purple">string</span> `No` `Example value: Month`

Subscription instance lifecycle unit, supports purchasing in months or years. Supports the following settings:


* Month: Monthly subscription

* Year: subscription



**Period** <span data-label="purple">integer</span> `No`

Subscription duration for subscription\-type instances.


* When PeriodUnit is set to Month, the valid range is 1 to 9.

* When PeriodUnit is set to Year, the valid range is 1 to 3.




**VpcId** <span data-label="purple">string</span> <span data-api-tag="require|1YP0ou">必选</span> `Example value: vpc-13fo9gkz6j6683n6xxxxx`

The private network (VPC) ID where the instance is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the instance is created, you cannot modify its private network or subnet. Proceed carefully when creating the instance.</div>


* <div data-tips="true" data-tips-type="tip">You can call the DescribeVpcs interface of the Virtual Private Cloud (VPC) to query the list of available VPCs and subnets.</div>




**InstanceDescription** <span data-label="purple">string</span> `No` `Example value: instance for test`

Brief description of the RabbitMQ instance. The length of characters ranges from 1 to 128.



**ClientToken** <span data-label="purple">string</span> <span data-api-tag="require|ekJoXi">必选</span> `Example value: 123e4567-e89b-12d3-a456-426655440000`

Identifier ensuring idempotency of client requests.

This identifier is a 1 to 64 character ASCII string, case\-sensitive, generated by the client. It must be unique across different requests.

For how to use the idempotency identifier, refer to [request idempotency](https://docs.byteplus.com/en/docs/rabbitmq/Request_idempotency).



**Tags** <span data-label="purple">object[]</span> `No` `Example value: /`

Cloud resource tags. Instances can be categorized using tags for easier searching and resource aggregation. For detailed information, refer to [Tag management](https://docs.byteplus.com/en/docs/rabbitmq/Tag_overview).


**Key** <span data-label="purple">string</span> <span data-api-tag="require|MUEOin">必选</span> `Example: owner`

Key of the tag.



**Value** <span data-label="purple">string</span> `No` `Example value: zhangsan`

The tag value.




**ProjectName** <span data-label="purple">string</span> `No` `Example: newproject`

The IAM project to which the currently created RabbitMQ instance belongs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no IAM project is specified, message queue for RabbitMQ will add the new instance to the IAM project named Default.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId** <span data-label="purple">string</span> `Example: rbtmq-5b293870****`

RabbitMQ instance ID.



**OrderId** <span data-label="purple">string</span> `Example value: order-712089661643355****`

Order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=DescribeComputeSpecsInfo&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "ZoneId": "cn-guangzhou-a",
   "Version": "3.8.18",
   "ComputeSpec": "rabbitmq.n3.x2.medium",
   "StorageSpace": 1000,
   "UserName": "Admin",
   "UserPassword": "Admin-***",
   "ChargeInfo": {
       "ChargeType":"PostPaid"
   },
   "VpcId":"vpc-3ezqp84nkhlvk72200sck****",
   "SubnetId": "subnet-3ezqp8sbxu9kw72200smp****"
}

```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "202302211942179576CA8B35BEC3E94AB6",
        "Action": "CreateInstance",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "InstanceId": "rbtmq-7585af44****",
        "OrderId": "Order720257278320081****"
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |UnSupportedConfig |Unsupported instance configuration, please check. |Configuration does not meet the specifications. |
|400 |InvalidParameter |The specified parameter %s is not valid. |The parameter value %s is invalid. |
|400 |InstanceCountExceedLimit |The number of instances exceeds the limit. |The number of instances has reached the limit. |
|400 |InsufficientBalance |Insufficient account balance. |Insufficient balance. |
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You are not authorized. Authorize or switch accounts and try again. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
|500 |InsufficientResource |Insufficient resources, please switch to another available zone or region and try again. |Insufficient resources, please try again later. |
