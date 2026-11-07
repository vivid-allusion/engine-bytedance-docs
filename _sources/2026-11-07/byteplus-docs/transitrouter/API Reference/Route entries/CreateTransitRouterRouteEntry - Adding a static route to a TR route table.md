---
title: "CreateTransitRouterRouteEntry - Adding a static route to a TR route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry"
---

Call CreateTransitRouterRouteEntry to add a static route to a specified Transit Router (TR) route table.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterRouteEntry&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ZR0D0C">必选</span> `Example: CreateTransitRouterRouteEntry`

The interface name. The current API name is `CreateTransitRouterRouteEntry`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|RO4jlx">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|lIh0KK">必选</span> `Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the TR instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



**TransitRouterRouteEntryNextHopType ** <span data-label="purple">String </span><span data-api-tag="require|PSaxA8">必选</span> `Example: Attachment`

The next hop type of the route. Values:


* Attachment: A network instance, indicating that traffic matching the route is forwarded to the specified network instance.

* BlackHole: A blackhole, indicating that traffic matching the route is discarded.



**TransitRouterRouteEntryNextHopId ** <span data-label="purple">String </span>`optional` `Example: tr-attach-1ffn6gjk****`

The Next Hop ID of the route.


* You can call the [DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) API to obtain the ID of the Virtual Private Cloud (VPC) attachment.

* You can call the [DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) API to obtain the ID of the Virtual Private Network (VPN) attachment.

* You can call the [DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) API to obtain the ID of the Direct Connect (DC) Gateway attachment.

* You can call the [DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) API to obtain the ID of the inter\-region attachment.



**DestinationCidrBlock ** <span data-label="purple">String </span>`optional` `Example: 192.168.XX.XX/24`

The destination CIDR block of the route.

This parameter and `DestinationPrefixListId` cannot be passed simultaneously.



**Description ** <span data-label="purple">String </span>`optional` `Example: This transit router is used for test.`

The description of the route in the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**TransitRouterRouteEntryName ** <span data-label="purple">String </span>`optional` `Example: routeentry-01`

The name of the route in the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If you do not provide this parameter or leave it unset, it defaults to the TR route ID.



**DestinationPrefixListId ** <span data-label="purple">String </span>`optional` `Example: pl-1234567890abcdef0`

The ID of the target prefix list for the route entry. It specifies the destination address range of the route entry.

This parameter and `DestinationCidrBlock` cannot be passed simultaneously.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature that TR supports VPC prefix lists is currently in the beta stage. To request a trial, please contact your account manager.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterRouteEntryId ** <span data-label="purple">String </span>`Example: tr-rte-1i5i8khf9m58gae5kcx6****`

The route ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateTransitRouterRouteEntry&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v****&TransitRouterRouteEntryNextHopType=Attachment&DestinationCidrBlock=192.168.XX.XX/24 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T035640Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250804115643130207110174097CF7",
        "Action": "CreateTransitRouterRouteEntry",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "TransitRouterRouteEntryId": "tr-rte-1i5i8khf9m58gae5kcx6****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format specified for CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for Description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for Description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for Name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for Name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidTransitRouter.IPv6NotSupported |The specified Transit Router does not support the IPv6 feature. |The specified TR instance does not support IPv6. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to arrears. The current action is unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterRouteEntry.DestinationInvalid |Cannot specify destination CIDR and prefix list simultaneously. |You cannot specify both a destination CIDR block and a destination prefix list when creating a route entry. |
|400 |InvalidTransitRouterRouteEntry.IPv4OnlyAttachment |The specified Transit Router attachment supports IPv4 only, and cannot configure IPv6 route with it. |The specified attachment is IPv4 single\-stack and does not support configuring IPv6 routes. |
|400 |InvalidTransitRouterRouteEntry.IPv6OnlyAttachment |The specified Transit Router attachment supports IPv6 only, and cannot configure IPv4 route with it. |The specified attachment is IPv6 single\-stack and does not support configuring IPv4 routes. |
|400 |InvalidTransitRouterRouteEntry.MulticastCidrNotSupported |The specified cidr is a multicast cidr, and can not be configured as route entry. |Not supported configuring routes with destination CIDR blocks as multicast CIDR blocks. |
|400 |InvalidTransitRouterRouteEntry.NextHopMissing |The specified Transit Router route entry next hop is missing. |The next hop of the specified TR route cannot be empty. |
|400 |InvalidTransitRouterRouteEntry.NextHopTypeMalformed |The specified Transit Router route entry next hop type is malformed, only BlackHole and Attachment are supported. |The next hop type of the specified TR route is not supported, which supports only BlackHole and Attachment. |
|400 |InvalidTransitRouterRouteEntry.NextHopUnsupported |The specified Transit Router route type is black hole, and does not support configuring next hop. |Blackhole routing does not support specifying a next hop. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|400 |QuotaExceeded.TransitRouterEcmpRouteEntry |You've reached the maximum number of next hop attachment that one ECMP route entry can have. |You have reached the maximum number of ECMP routes that can be configured. |
|400 |QuotaExceeded.TransitRouterRouteEntry |You've reached the maximum number of route entries that one Transit Router route table can have. |You have reached the maximum number of routes per TR route table. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. Action unsupported. |
|403 |Forbidden.VpcPrefixList |You are not authorized to use prefix list. |No permission to use the prefix list. Enable the prefix list allowlist. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified TR does not exist. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
|404 |InvalidTransitRouterRouteEntry.NextHopNotFound |The specified Transit Router route entry next hop attachment does not exist. |The specified next hop instance for the TR route does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified TR route table does not exist. |
|409 |InvalidTransitRouterRouteEntry.DestinationCidrBlockConflict |The specified Transit Router route entry destination already exists. |The specified destination CIDR block already exists in the TR route table. |
|409 |InvalidTransitRouterRouteEntry.DestinationPrefixListCidrConflict |The CIDRs in the specified destination prefix list conflict with existing routes in the Transit Router route table. |A CIDR block in the specified prefix list conflicts with an existing route in the TR route table. |
|409 |InvalidTransitRouterRouteEntry.DestinationPrefixListConflict |Cannot configure multiple routes with an empty prefix list. |The specified prefix list is empty. Creating multiple routes using an empty prefix list is not supported. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
