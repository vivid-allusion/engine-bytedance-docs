---
title: "ModifyNatGatewayAttributes - Modifying a NAT gateway"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/ModifyNatGatewayAttributes"
---

Call the ModifyNatGatewayAttributes API to modify the specification, name, and description of a NAT gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The current account is not in arrears and has sufficient balance to cover subsequent NAT costs.

* Subscription NAT gateways only support specification upgrades. Specification downgrades are not supported.

* Leaving optional parameters of this API unset means no modifications to them.

* If the following optional parameters are not configured, the existing configurations will be preserved.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyNatGatewayAttributes&groupName=NAT%E7%BD%91%E5%85%B3&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|XYU3yI">必选</span> `Example: ModifyNatGatewayAttributes`

The action that you want to perform. Value: ModifyNatGatewayAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|TzOnXr">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**Description ** <span data-label="purple">string </span>`optional` `Example: This is a NAT`

Description of the NAT gateway.


* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters. If not provided, the original configuration remains.



**NatGatewayName ** <span data-label="purple">string </span>`optional` `Example: nat-01`

The name of the NAT gateway.


* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters. If not provided, the original configuration remains.



**Spec ** <span data-label="purple">string </span>`optional` `Example: Medium`

The target specification of the NAT gateway. Values:


* Small (default)

* Medium.

* Large.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VPC NAT gateways do not have a specification attribute and cannot be modified.​</div>




**SmartScheduleEnabled ** <span data-label="purple">boolean </span>`optional` `Example: true`

Describe whether to enable smart scheduling. Values:


* true: Enable.

* false: Disable.



**SmartScheduleRule ** <span data-label="purple">string </span>`optional` `Example: BGP`

The smart scheduling policy rule. Values:


* ChinaMobile: China Mobile.

* ChinaTelecom: China Telecom.

* ChinaUnicom: China Unicom.

* BGP: BGP line.



**DirectMode ** <span data-label="purple">boolean </span>`optional` `Example: false`

Modify the direct mode for the NAT gateway. Values:


* false: Convert the NAT gateway to non\-direct mode



**NatGatewayId ** <span data-label="purple">string </span><span data-api-tag="require|PMaxSY">必选</span> `Example: ngw-3tex2x1cwd4c6c0v****`

ID of the NAT gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifyNatGatewayAttributes&Version=2020-04-01&NatGatewayId=ngw-2fedgzyvtzaio59gp675l****&Spec=Small HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyNatGatewayAttributes",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidNatGateway.InvalidBillingType |The specified NAT gateway is not in the correct billing type for the request. |The specified NAT gateway cannot respond this request due to its billing method. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |InvalidNatGatewaySpec.Malformed |The specified NAT spec is malformed. |The specified NAT gateway specification is not supported. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |QuotaExceeded.ExtraLargeNatGateway |You've reached the limit on the number of extra large NAT gateway that you can create. |You have reached the maximum number of super large NAT gateways that you can create. |
|400 |InvalidNatGateway.SmartScheduleNotSupport |The number of EIP types bound by NAT does not support nat smart schedule. |Smart scheduling is not supported because the NAT gateway is associated with EIPs from fewer than two line operators. |
|400 |InvalidNatGateway.SmartScheduleNotSupported |The specified NAT gateway does not support nat smart schedule. |The specified NAT gateway instance does not support smart scheduling. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidNatGateway.QosNotSupport |The specified nat gateway does not support qos. |The specified NAT gateway does not support Quality of Service (QoS). |
|400 |InvalidNatGateway.QosAlreadyEnabled |The specified nat gateway qos is already enabled. |The specified NAT gateway has QoS enabled. |
|400 |InvalidNatGateway.QosQueueExist |The specified NAT gateway has dependent resource of qos queue. |The specified NAT gateway contains remaining QoS queues and cannot be deleted. |
|403 |Forbidden |You are not authorized to create or update an extra large NAT gateway. |No permission to create or modify super large NAT gateways. |
|403 |Forbidden |You are not authorized to use nat qos. |No permission to use NAT QoS. |
|403 |Forbidden.SmartScheduleLimited |You are not authorized to use nat smart schedule. |No permission to use smart scheduling for the NAT gateway. |
|404 |InvalidNatGateway.NotFound |The specified NAT gateway does not exist. |The specified NAT gateway does not exist. |
|412 |InvalidNatGateway.Expired |The specified NAT gateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
