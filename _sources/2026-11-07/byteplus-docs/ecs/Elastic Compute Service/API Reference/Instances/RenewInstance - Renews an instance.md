---
title: "RenewInstance - Renews an instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/RenewInstance"
---

Call the RenewInstance operation to renew a subscription instance, prioritizing coupon deduction for renewal. The subscription volumes and images are synchronously renewed.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* You can only call this operation to renew a subscription instance.

* Before calling this operation, you can learn about the billing method and pricing of ECS instances. [Learn more](https://docs.byteplus.com/en/docs/ecs/Billing-overview).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RenewInstance&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|vWMeAH">必选</span> `Sample value: RenewInstance`

The operation that you want to perform. Valid value: RenewInstance.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|jdOd78">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 23fa21A8823nfasd7f****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API operation times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|jfyPap">必选</span> `Sample value: i-3thhlu8byl4bwbha****`

The instance ID.



**Period ** <span data-label="purple">integer </span><span data-api-tag="require|Fz8sH5">必选</span> `Sample value: 1`

The number of months for renewal. Valid values:

1, 2, 3, 4, 5, 6, 7, 8, 9, 12, 24, 36



**PeriodUnit ** <span data-label="purple">string </span><span data-api-tag="require|ygI63o">必选</span> `Sample value: Month`

The time unit of the renewal duration, that is, the unit of the `Period` parameter. Value:


* Month (default)

* Week (not supported)



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderId ** <span data-label="purple">string </span>`Sample value: Order7007335217124******`

The order ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=RenewInstance&Version=2020-04-01&InstanceId=i-3thhlu8byl4bwbha****&Period=1&PeriodUnit=Month HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "RenewInstance",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order7007335217124******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |InvalidChargeType |The specified ChargeType is not valid, is unsupported, or cannot be used. |The specified instance billing method is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidPeriod |The specified period is not valid. |The specified number of billing cycles is invalid. |
|400 |InvalidPeriodUnit |The specified PeriodUnit is not valid, is unsupported, or cannot be used. |The specified billing cycle is invalid. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The parameter InstanceId cannot be left empty. |
|403 |InvalidInstance.RequestForbidden |Request is forbidden by the server. |The specified resource can no longer be used because your account has violated relevant rules. To restore service availability, submit a ticket to our service team for assistance. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |OperationDenied.AffinityGroupInstance |The specified operation is denied as your instance is an affinity group instance, and all instanceIds the affinity group must be specified. |The specified operation is rejected because the instance is an affinity group instance, and you must specify the IDs of all instances in the affinity group. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified operation is rejected because your resource has been locked by another operation. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
