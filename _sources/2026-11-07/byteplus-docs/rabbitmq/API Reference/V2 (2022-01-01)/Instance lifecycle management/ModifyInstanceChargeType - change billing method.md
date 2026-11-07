---
title: "ModifyInstanceChargeType - change billing method"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/ModifyInstanceChargeType_-_change_billing_method"
---

Call the ModifyInstanceChargeType API to change the instance's billing method.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

This API changes the instance's billing method and currently only supports switching pay\-as\-you\-go instances to subscriptions. This operation does not affect the instance's running.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The status of the RabbitMQ instance is <strong>Running</strong>.</div>


* <div data-tips="true" data-tips-type="tip">When switching from pay\-as\-you\-go to subscriptions, you need to settle the pay\-as\-you\-go instance and prepay for the annual and monthly fees. Please ensure there is sufficient balance in your account.</div>


* <div data-tips="true" data-tips-type="tip">Currently, only switching from pay\-as\-you\-go to subscriptions is supported. Confirm the instance's billing method is <strong>pay\-as\-you\-go</strong> before proceeding.</div>



<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

NotesRequest frequency: This API limits requests to 100 times/second. The per\-user request frequency limit is 20 times/second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceChargeType&groupName=%E5%AE%9E%E4%BE%8B%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E7%AE%A1%E7%90%86&serviceCode=RabbitMQ&version=2022-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|a8k0ar">必选</span> `Example value: ModifyInstanceChargeType`

Action to perform, value: ModifyInstanceChargeType.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|USMVRB">必选</span> `Example value: 2022-01-01`

API version, value: 2022\-01\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|zaqiSx">必选</span> `Example value: rbtmq-5b293870****`

Instance ID.



**ChargeInfo** <span data-label="purple">object</span> <span data-api-tag="require|Khgpr1">必选</span> `Example value: /`

Billing method after switching

Currently, only instances with pay\-as\-you\-go billing can be switched to Subscription instances.


**ChargeType** <span data-label="purple">string</span> <span data-api-tag="require|e7elur">必选</span> `Example value: PostPaid`

The billing method for the instance. Supported types include:


* PostPaid: Pay\-as\-you\-go

* PrePaid: Subscription

   When PrePaid is specified, parmameters of AutoRenew, PeriodUnit, and Period must also be specified.



**AutoRenew** <span data-label="purple">boolean</span> `Optional` `Example value: false`

Whether to auto\-renew the subscription instance after expiration.


* true: auto\-renew.

* false: auto\-renew fails. Manual renewal is required after expiration. Otherwise, the instance will be shut down.

   Only subscription instances need to be specified. For example, when ChargeType is set to PrePaid, it is required.



**PeriodUnit** <span data-label="purple">string</span> `Optional` `Example: Month`

Subscription instance lifecycle unit, supports purchasing in months or years. Supports the following settings:


* Month: monthly subscription

* Year: annual subscription

   Only subscription instances need to be specified. For example, when ChargeType is set to PrePaid, it is required.



**Period** <span data-label="purple">integer</span> `Optional` `Example value: 1`

Subscription duration for subscription instances.


* When PeriodUnit is set to Month, the value ranges from 1 to 9.

* When PeriodUnit is set to Year, the value range is 1 to 3.

   Only subscription instances need to be specified. For example, when ChargeType is set to PrePaid, it is required.




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the unique response parameters of this API are listed below. For more details, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderId** <span data-label="purple">string</span> `Example value: order-712089661643355****`

Order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST https://rabbitmq.byteplusapi.com/?Action=ModifyInstanceChargeType&Version=2022-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/json
Host: rabbitmq.byteplusapi.com
X-Date: 20210328T100802Z
Authorization: HMAC-SHA256 Credential=AK********/20210328/cn-beijing/rabbitmq/request, SignedHeaders=x-date, Signature=********

{
   "InstanceId": "rbtmq-9283a61f****",
   "ChargeInfo": {
       "ChargeType":"PostPaid"
   }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "202302211942179576CA8B35BEC3E94AB6",
        "Action": "ModifyInstanceChargeType",
        "Version": "2022-01-01",
        "Service": "RabbitMQ",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "OrderId": "Order720257278320081****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this interface and business logic. Refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) section for common error codes.


|Status code |Error code |Error message |Specifications |
|---|---|---|---|
|403 |OperationDenied.AccountNotAuthorized |You are not authorized to perform this operation. |You do not have the required permissions. Authorize or switch accounts and try again. |
|403 |OperationDenied.InvalidInstanceStatus |The operation is not valid for the current status of the instance. |The current instance status does not allow this action. |
|403 |OperationDenied.TaskIsRunning |An operation is currently in progress. Try again later. |The backend task is running, please try again later. |
|404 |InvalidInstanceId.NotFound |The specified Instance ID does not exist. |The instance does not exist. |
|500 |InternalError |The request failed due to some unknown error, exception or failure. |Internal error, please try again later. |
