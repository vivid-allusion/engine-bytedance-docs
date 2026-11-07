---
title: "CreateTransitRouterVpcAttachment - Creating a VPC attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment"
---

Call CreateTransitRouterVpcAttachment to create a Virtual Private Cloud (VPC) attachment

<span id=".5L2_55So6K-05piO"></span>
## Instructions

In a request parameter such as Tags.N.a, the "N" represents the sequence number of a tag entry. It must be assigned a value in strict numerical order, starting from 1 up to 50. Separate multiple tags with ampersands (&). Each tag key pairs one tag value.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterVpcAttachment&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|bmOv1F">必选</span> `Example: CreateTransitRouterVpcAttachment`

The interface name. The current API name is `CreateTransitRouterVpcAttachment`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|IzrUY9">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Ipv6Enabled ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable IPv6. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Yes.

* false: No.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IPv6 feature of TR is in the beta stage. To request a trail, please contact your account manager.</div>




**TransitRouterId ** <span data-label="purple">String </span><span data-api-tag="require|Ivyty5">必选</span> `Example: tr-7qthudw0ll6jmc****`

The TR instance ID. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**VpcId ** <span data-label="purple">String </span><span data-api-tag="require|lBVJTx">必选</span> `Example: vpc-2fexiqjlgjif45oxruvso****`

The ID of the VPC instance. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to obtain the VPC instance ID.



**AttachPoints.N.SubnetId ** <span data-label="purple">String </span><span data-api-tag="require|dLG0yC">必选</span> `Example: subnet-2fexiqjlgjif45oxruvso****`

The subnet ID of the attachment point. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) to obtain the subnet ID.


* N represents the sequence number of a subnet ID, ranging from 1 to 100.

* Separate multiple subnet IDs with ampersands (&).



**AttachPoints.N.ZoneId ** <span data-label="purple">String </span><span data-api-tag="require|cEtbaZ">必选</span> `Example: cn-beijing-a`

The ID of the availability zone to which the subnet belongs.


* N represents the sequence number of a availability zone ID, ranging from 1 to 100.

* Separate multiple availability zone IDs with ampersands (&).



**Description ** <span data-label="purple">String </span>`optional` `Example: This attachment is used for test.`

The description of the network instance attachment.


* Must start with a letter, digit, or Chinese character. May include letters, digits, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**TransitRouterAttachmentName ** <span data-label="purple">String </span>`optional` `Example: attachment-01`

The name of the network instance attachment.


* Must start with a letter, digit, or Chinese character. May include letters, digits, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it unset, it defaults to the attachment ID.



**AutoPublishRouteEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to automatically publish TR routes to the route table of the network instance. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Yes. This means the system automatically publishes routes from the TR route table associated with forwarding for this network instance attachment into the route table of that network instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system automatically synchronizes TR routes to the network instance's route table only when this parameter is set to "true" and the TR route table associated with forwarding for this network instance attachment contains routes.   </div>
   

* false (default): No.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

The Client Token that is used to ensure the request idempotency.


* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The custom tag key of the network instance attachment.


* Must be 1 to 128 characters.

* Case\-sensitive. Must not start with `volc:` or `sys:` in any case combination.

* Must not start or end with a space.

* May include letters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>


* <div data-tips="true" data-tips-type="tip">If you do not provide this parameter or leave it unset, it defaults to empty.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: v2`

The custom tag value of the network instance attachment.


* Must be 0 to 255 characters.

* Case\-sensitive. Must not start or end with a space.

* May include letters, digits, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), and at signs (@).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide this parameter, provide Tags.N.Key first.</div>




**ApplianceModeEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable path consistent mode. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Yes. After enabling, TR will use the same availability zone attachment point to forward both the request and response traffic when routing to this VPC attachment.

* false (default): No.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The path consistency feature of TR is in the invite\-only beta stage. To request a trail, please contact your account manager.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-7qthudw0ll6jmc****`

The ID of the network instance attachment.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=CreateTransitRouterVpcAttachment&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc****&VpcId=vpc-2fexiqjlgjif45oxruvso**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250717T063502Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250717/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2025071714350620725405824045B658",
        "Action": "CreateTransitRouterVpcAttachment",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "TransitRouterAttachmentId": "tr-attach-7qthudw0ll6jmc****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |InvalidTransitRouter.ApplianceModeNotSupported |The specified Transit Router does not support the Appliance Mode feature. |The specified TR instance does not support Appliance Mode. |
|400 |InvalidTransitRouter.IPv6NotSupported |The specified Transit Router does not support the IPv6 feature. |The specified TR instance does not support IPv6. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to arrears. The current action is not supported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterAttachment.InsufficientSubnetIpAddresses |There are subnets that do not have available IP addresses. |The specified subnet does not have available IPs. |
|400 |InvalidTransitRouterAttachment.ServiceRoleNotAuthorized |The service role for Transit Router has not been authorized. |The TR service role has not been authorized to the current account. |
|400 |InvalidTransitRouterAttachment.SubnetIdDuplicate |There are subnets used multiple times in the request. |Subnets are specified repeatedly during the creation of the network instance attachment. |
|400 |InvalidTransitRouterAttachment.SubnetWithoutIPv4Cidr |There are subnets without IPv4 cidr within the specific requirement. |Partial subnets do not have available IPv4 addresses. |
|400 |InvalidTransitRouterAttachment.SubnetWithoutIPv6Cidr |There are subnets without IPv6 cidr within the specific requirement. |Partial subnets do not have available IPv6 addresses. |
|400 |InvalidTransitRouterAttachment.ZoneIdDuplicate |There are available zones used multiple times in the request. |Availability zones are specified repeatedly during the creation of the network instance attachment. |
|400 |InvalidTransitRouterAttachment.ZoneIdMismatch |The specified available zone does not match with the specified subnet. |The specified availability zone does not match the specified subnet. |
|400 |InvalidTransitRouterAttachment.ZoneUnsupported |There are available zones not supported by Transit Router. |Partial specified availability zones do not support creating network instance attachments. |
|400 |InvalidTransitRouterRoutePropagation.TransitRouterMismatch |The specified route table and attachment do not belong to one same Transit Router. |The TR of the specified route table does not match the TR attached to the network instance attachment. |
|400 |InvalidTransitRouterRouteTableAssociation.TransitRouterMismatch |The specified route table and attachment do not belong to one same Transit Router. |The TR of the specified route table does not match the TR attached to the network instance attachment. |
|400 |InvalidTransitRouterRouteTablePropagation.PropagationGranularityInvalid |The specified Transit Router route table propagation granularity is invalid, only VPC and Subnet are supported. |The specified route learning granularity is invalid. |
|400 |LimitExceeded.AutoRoutePublishOfTrEnabledPerVpc |You've reached the maximum number of TRs that one vpc can enable auto route publish with. |You have reached the maximum number of TRs for which you can enable auto publishing in a single VPC. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum of tags that can be processed in a single request. |
|400 |MainAccountNotSupportPaypalErr |You are requested to contact the main account to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Contact your root account to add other payment methods. |
|400 |NotSupportPaypalErr |You are requested to provide an alternative payment method other than Paypal before enabling the pay\-as\-you\-go products in BytePlus. |PayPal is not supported for postpaid products in this order. Add other payment methods. |
|400 |OrderError |Failed to create order and pay in one step. |Failed to create and pay for the order. |
|400 |QuotaExceeded.AttachPointPerTransitRouterAttachment |The specified request reaches the max number of attach points that you can specify. |You have reached the maximum number of attachment points that you can specify for a single network instance attachment. |
|400 |QuotaExceeded.TransitRouterAttachment |You've reached the maximum number of attachments that one Transit Router can have. |You have reached the maximum of network instances that you can create in a single TR. |
|400 |QuotaExceeded.TransitRouterAttachmentPerVpc |You've reached the limit on the number of Transit Routers that one VPC can attach. |You have reached the maximum number of TRs that can be attached to a single VPC. |
|400 |QuotaExceeded.TransitRouterSecurityGroup |You've reached the maximum number of security groups that can be created in one region. |You have reached the maximum number of security groups that can be created per region. |
|400 |QuotaExceeded.VpcAttachment |You've reached the maximum number of vpc attachments that one transit router can have. |You have reached the maximum number of VPC attachments that can be created per TR. |
|400 |UnsupportedOperation |The order is not allowed due to lack of Payment Method in your account, please provide Payment Method. |The action request on this instance is denied due to no payment method in the account. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|403 |Forbidden.PurchaseLimited |The account is not authorized to purchase the resource. |This account has no permission to purchase resources. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. The action is not supported. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified Transit Router (TR) does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterAttachment.SubnetNotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidTransitRouterAttachment.VpcNotFound |The specified VPC does not exist. |The specified VPC does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified TR route table does not exist. |
|409 |InvalidTransitRouterAttachment.Conflict |The specified instance has already been attached to the Transit Router. |The specified network instance has been added to the specified TR. Duplicate action is not supported. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
