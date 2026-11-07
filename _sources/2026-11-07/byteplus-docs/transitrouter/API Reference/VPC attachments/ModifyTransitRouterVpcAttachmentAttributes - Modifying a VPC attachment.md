---
title: "ModifyTransitRouterVpcAttachmentAttributes - Modifying a VPC attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes"
---

Call ModifyTransitRouterVpcAttachmentAttributes to modify the information of the specified Virtual Private Cloud (VPC) attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterVpcAttachmentAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|h-YQm5">必选</span> `Example: ModifyTransitRouterVpcAttachmentAttributes`

The interface name. The current API name is `ModifyTransitRouterVpcAttachmentAttributes`.



**Version** <span data-label="purple">String</span> <span data-api-tag="require|8UiVQG">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**Ipv6Enabled ** <span data-label="purple"> Boolean  </span>`optional` `Example: false`

Describe whether to enable IPv6. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Yes.

* false: No.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The IPv6 feature of TR is in the beta stage. If you need a trial, please contact your account manager.</div>




**TransitRouterAttachmentId ** <span data-label="purple"> String </span><span data-api-tag="require|Do0gDI">必选</span> `Example: tr-attach-a*******`

The ID of the network instance attachment. You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.



**AttachPoints.N.SubnetId ** <span data-label="purple"> String </span>`optional` `Example: subnet-2fexiqjlgjif45oxruvso****`

The subnet ID of the attachment point. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) to obtain the subnet ID.


* N represents the serial number of the subnet ID, ranging from 1 to 100.

* Separate multiple subnet IDs with ampersands (&).



**AttachPoints.N.ZoneId ** <span data-label="purple"> String  </span>`optional` `Example: cn-guangzhou-a`

ID of the availability zone to which the subnet belongs.


* N represents the serial number of the availability zone ID, ranging from 1 to 100.

* Separate multiple availability zone IDs with ampersands (&).



**AutoPublishRouteEnabled ** <span data-label="purple"> Boolean </span>`optional` `Example: false`

Describe whether to automatically publish TR routes to the route table of the network instance. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Yes. This means the system automatically publishes routes from the TR route table associated with forwarding for this network instance attachment into the route table of that network instance.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Explanation   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The system automatically synchronizes TR routes to the network instance's route table only when this parameter is set to "true" and the TR route table associated with forwarding for this network instance attachment contains routes.   </div>
   

* false (default): No.



**Description ** <span data-label="purple"> String </span>`optional` `Example: This attachment is used for test.`

The description of the network instance attachment.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not modify this parameter value, its original configuration remains.



**TransitRouterAttachmentName ** <span data-label="purple"> String </span>`optional` `Example: attachment-02`

The name of the network instance attachment.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not modify this parameter value, its original configuration remains.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterVpcAttachmentAttributes&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-a******* HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033836Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2025080411384025302903309369C618",
    "Action": "ModifyTransitRouterVpcAttachmentAttributes",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of the specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of the specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTransitRouter.IPv6NotSupported |The specified Transit Router does not support the IPv6 feature. |The specified TR instance does not support IPv6. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified Transit Router (TR) is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.InsufficientSubnetIpAddresses |There are subnets that do not have available IP addresses. |The specified subnet does not have available IPs. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.SubnetIdDuplicate |There are subnets used multiple times in the request. |Subnets are specified repeatedly during the creation of the network instance attachment. |
|400 |InvalidTransitRouterAttachment.SubnetWithoutIPv4Cidr |There are subnets without IPv4 cidr within the specific requirement. |Partial subnets do not have available IPv4 addresses. |
|400 |InvalidTransitRouterAttachment.SubnetWithoutIPv6Cidr |There are subnets without IPv6 cidr within the specific requirement. |Partial subnets do not have available IPv6 addresses. |
|400 |InvalidTransitRouterAttachment.VpcWithIPv4RouteEntryToTransitRouter |The specified TR attachment can not be modified as IPv6 only, since there are IPv4 static routes in VPC route tables depending on the attachment. |The specified VPC contains an IPv4 static route pointing to this TR. Therefore, disabling IPv4 for this attachment is not permitted. |
|400 |InvalidTransitRouterAttachment.VpcWithIPv6RouteEntryToTransitRouter |The specified TR attachment can not be modified as IPv4 only, since there are IPv6 static routes in VPC route tables depending on the attachment. |The specified VPC contains an IPv6 static route pointing to this TR. Therefore, disabling IPv6 for this attachment is not permitted. |
|400 |InvalidTransitRouterAttachment.VpcWithRouteEntryToTransitRouter |The VPC of the specified attachment has customized route entries to the Transit Router. |The route table of the VPC associated with the specified attachment contains route entries pointing to the TR. |
|400 |InvalidTransitRouterAttachment.WithIPv4StaticRouteEntry |The specified TR attachment can not be modified as IPv6 only, since there are IPv4 static routes in TR route tables depending on the attachment. |The TR route table contains an IPv4 static route pointing to this network instance. Therefore, disabling IPv4 for this attachment is not permitted. |
|400 |InvalidTransitRouterAttachment.WithIPv6StaticRouteEntry |The specified TR attachment can not be modified as IPv4 only, since there are IPv6 static routes in TR route tables depending on the attachment. |The TR route table contains an IPv6 static route pointing to this network instance. Therefore, disabling IPv6 for this attachment is not permitted. |
|400 |InvalidTransitRouterAttachment.WithStaticRouteEntry |The specified Transit Router has static route entries depending on the attachment. |The specified network instance attachment has static routes configured and cannot be deleted. |
|400 |InvalidTransitRouterAttachment.ZoneIdDuplicate |There are available zones used multiple times in the request. |Availability zones are specified repeatedly during the creation of the network instance attachment. |
|400 |InvalidTransitRouterAttachment.ZoneIdMismatch |The specified available zone does not match with the specified subnet. |The specified availability zone does not match the specified subnet. |
|400 |InvalidTransitRouterAttachment.ZoneUnsupported |There are available zones not supported by Transit Router. |Part of the specified availability zones do not support creating network instance attachments. |
|400 |LimitExceeded.AutoRoutePublishOfTrEnabledPerVpc |You've reached the maximum number of TRs that one vpc can enable auto route publish with. |You have reached the maximum number of TRs for which you can enable auto publishing in a single VPC. |
|400 |QuotaExceeded.AttachPointPerTransitRouterAttachment |The specified request reaches the max number of attach points that you can specify. |You have reached the maximum number of attachment points that you can specify for a single network instance attachment. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. This action is unsupported. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified Transit Router (TR) does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterAttachment.SubnetNotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
