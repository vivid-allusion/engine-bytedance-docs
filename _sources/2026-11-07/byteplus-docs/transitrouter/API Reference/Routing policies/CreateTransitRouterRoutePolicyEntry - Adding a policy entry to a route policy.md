---
title: "CreateTransitRouterRoutePolicyEntry - Adding a policy entry to a route policy."
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry"
---

Call the CreateTransitRouterRoutePolicyEntry API to add a route policy entry to a specified route policy.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* You can add up to 20 route policy entries for a single route policy.

* If a route policy is associated with a Transit Router (TR) route table, service traffic forwarding may be affected by adding route policy entry. Proceed with caution.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterRoutePolicyEntry&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|O49xJ9">必选</span> `Example: CreateTransitRouterRoutePolicyEntry`

The interface name. The current API name is `CreateTransitRouterRoutePolicyEntry`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|IrKpUv">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**IpPrefixMatchMode ** <span data-label="purple">String </span>`optional` `Example: Include`

The match mode of the route prefix.


* Include: Fuzzy match. When the route prefix in the match condition contains the route prefix of the matched route, it is considered a successful match. For example: A policy entry with a Route Prefix of 10.10.0.0/16 can fuzzily match a route with a Destination CIDR of 10.10.1.0/24.

* Complete (default): Exact match. A match is only considered successful if the route prefix specified in the condition is identical to the prefix of the target route.​ For example: A policy entry with a Route Prefix of 10.10.0.0/16 can only exactly match a route with a Destination CIDR of 10.10.0.0/16.



**TransitRouterRoutePolicyTableId ** <span data-label="purple">String </span><span data-api-tag="require|alTsZS">必选</span> `Example: tr-rpt-1i5i8khf9m58gae5kcx6****`

ID of the route policy. You can call the [DescribeTransitRouterRoutePolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables) API to obtain the ID of the route policy.



**Priority ** <span data-label="purple">Integer </span><span data-api-tag="require|IkRhUl">必选</span> `Example: 100`

The priority of the route policy entry. Default: Empty. Valid range: 1 to 10000. A lower priority value indicates higher precedence.

Priority values must be unique within the same routing policy.



**IpPrefixes.N ** <span data-label="purple">String </span>`optional` `Example: 192.168.XX.XX/24`

The route prefix of the route policy entry. Allow IPv4 and IPv6 CIDR blocks.


* N represents the sequence number of a route prefix, with a valid range of 1 to 200. Separate multiple route prefixes with ampersands ( & ).

* If you omit this parameter or set it to an empty value, it defaults to an empty string.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The IPv6 feature of TR is in the beta stage. If you need a trail, please contact your account manager.</div>




**SourceResourceTypes.N ** <span data-label="purple">String </span>`optional` `Example: VPC`

The source instance type of the route policy entry. Values:


* VPC: Virtual Private Cloud.

* DirectConnectGateway: Direct Connect Gateway.

* TransitRouter: Inter\-region Transit Router.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">N represents the sequence number of a source instance type, with a maximum of 10 per call. Separate multiple source instance types with ampersands (&).</div>


* <div data-tips="true" data-tips-type="tip">If you omit this parameter or set it to an empty value, it defaults to an empty string.</div>




**SourceResourceIds.N ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1aevy8sofi8mh1****`

The source instance ID of the route policy entry.


* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC instance ID.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to obtain the instance ID of the DC Gateway.

* You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the instance ID of the inter\-region TR.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">N represents the sequence number of a source instance ID, with a valid range of 1 to 10. Separate multiple source instance IDs with ampersands (&).</div>


* <div data-tips="true" data-tips-type="tip">This parameter is required when <code>SourceResourceTypes.N</code> is set.</div>




**DestinationResourceTypes.N ** <span data-label="purple">String </span>`optional` `Example: VPC`

The destination instance type of the route policy entry. Values:


* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC instance ID.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to obtain the instance ID of the DC Gateway.

* You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the instance ID of the inter\-region TR.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">N represents the sequence number of a source instance ID, with a valid range of 1 to 10. Separate multiple source instance IDs with ampersands (&).</div>


* <div data-tips="true" data-tips-type="tip">This parameter is required when <code>SourceResourceTypes.N</code> is set.</div>




**DestinationResourceIds.N ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1aevy8sofi8mh1****`

The destination instance ID of the route policy entry.


* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the VPC instance ID.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to obtain the instance ID of the DC Gateway.

* You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the instance ID of the inter\-region TR.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">N represents the sequence number of a target instance ID, with a valid range of 1 to 10. Separate multiple destination instance IDs with ampersands (&).</div>


* <div data-tips="true" data-tips-type="tip">This parameter is required when <code>DestinationResourceIds.N</code> is provided.</div>


* <div data-tips="true" data-tips-type="tip">This field must not be provided when the direction of the specified route policy is "In".</div>




**ActionResult ** <span data-label="purple">String </span><span data-api-tag="require|uYAZ9j">必选</span> `Example: Permit`

The policy action of the route policy entry. Values:


* Permit. It means allowing the routes that match the route policy to pass.

* Deny. It means rejecting the routes that match the route policy entry from passing.



**AsPathOperateMode ** <span data-label="purple">String </span>`optional` `Example: Additive`

The AsPath setting method for the route policy entry. Values:


* Additive: Append As Path. This means adding the specified AsPath to the front of the AsPath of routes allowed to pass.

* Replace: Replace As Path. This means replacing the AsPath of routes allowed to pass with the specified AsPath.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>ActionResult</code> is set to “Permit”.</div>




**ApplyAsPathValues.N ** <span data-label="purple">String </span>`optional` `Example: 1234`

The AsPath of the route policy entry. Value range: 1 to 4294967295.


* N represents the sequence number of a route attribute, with a valid range of 1 to 10.

* Separate multiple route attributes with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>ActionResult</code> is set to “Permit”.</div>




**Description ** <span data-label="purple">String </span>`optional` `Example: This transit router is used for test.`

The description of the route policy entry.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

The Client Token is used to ensure the request idempotency.


* This parameter value is auto\-generated by the client. Ensure uniqueness across requests, preventing duplicate actions caused by multiple client retries during API timeouts or server internal errors.

* Must not exceed 64 ASCII characters.

* If you do not set this parameter, idempotency check is not performed.



**PrefixListId ** <span data-label="purple">String </span>`optional` `Example: pl-1234567890abcdef0`

The prefix list ID associated with the route policy entry.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The feature that TR supports VPC prefix lists is currently in the beta stage. To request a trial, please contact your account manager.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterRoutePolicyEntryId ** <span data-label="purple">String </span>`Example: tr-rpe-13f1fdx5l****`

The ID of the route policy entry.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateTransitRouterRoutePolicyEntry&Version=2020-04-01&TransitRouterRoutePolicyTableId=tr-rpt-1i5i8khf9m58gae5kcx6****&Priority=100&ActionResult=Permit HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250722T113907Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250722/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2025072219401622106011418461E668",
        "Action": "CreateTransitRouterRoutePolicyEntry",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "TransitRouterRoutePolicyEntryId": "tr-rpe-13f1fdx5l****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for the CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTransitRouter.IPv6NotSupported |The specified Transit Router does not support the IPv6 feature. |The specified TR instance does not support IPv6. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to arrears. The current action is unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR cannot respond to the request due to its status. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterRoutePolicyEntry.ActionResultInvalid |The specified Transit Router route policy entry action result is invalid. A route policy action result must be Permit or Deny. |The specified policy action is not supported. Only Permit and Deny are supported. |
|400 |InvalidTransitRouterRoutePolicyEntry.AsPathInvalid |The specified AsPath is invalid. |The specified AsPath value is invalid. |
|400 |InvalidTransitRouterRoutePolicyEntry.AsPathOperateModeInvalid |The specified AsPath operate mode of the route policy entry is invalid, only Additive and Replace are supported. |The AsPath action for the specified policy entry is not supported. Only Append and Replace are supported. |
|400 |InvalidTransitRouterRoutePolicyEntry.IpPrefixMatchModeInvalid |The specified ip prefix match mode of the Transit Router route policy entry is invalid. |The specified route prefix match type is invalid for the route policy match condition. |
|400 |InvalidTransitRouterRoutePolicyEntry.IpPrefixMatchModeMismatch |The specified ip prefix match mode does not match with the specified ip prefix. |The specified route prefix match type mismatches the route prefix. |
|400 |InvalidTransitRouterRoutePolicyEntry.IpPrefixMatchModeNotSupported |The Transit Router route policy entry does not support configuring ip prefix match mode. |The specified route policy entry does not support configuring route prefix fuzzy match. |
|400 |InvalidTransitRouterRoutePolicyEntry.MatchConditionMissing |The specified Transit Router route policy entry must have at least one match condition. |The specified route policy entry must contain at least one match condition. |
|400 |InvalidTransitRouterRoutePolicyEntry.PriorityInvalid |The specified priority of the Transit Router route policy entry is invalid. |The priority of the specified route policy entry is invalid. |
|400 |InvalidTransitRouterRoutePolicyEntry.ResourceTypeInvalid |The specified resource type of the Transit Router route policy entry is invalid. |The instance type specified for the route policy match condition is invalid. |
|400 |LimitExceeded.RoutePolicyEntryApplyAsPath |You've reached the limit on the number of AsPath that can be applied. |You have reached the maximum length of AsPath that you can configure to a route policy entry. |
|400 |LimitExceeded.RoutePolicyEntryMatchCondition |You've reached the limit on the number of match conditions that one route policy entry can have. |You have reached the maximum match conditions for a single route policy entry. |
|400 |MissingParameter |The request is missing a required parameter. |This request is missing a required parameter. |
|400 |QuotaExceeded.TransitRouterRoutePolicyEntry |You've reached the limit on the number of route policy entries that one Transit Router route policy can have. |You have reached the maximum number of entries for a single route policy. |
|403 |Forbidden.CreateRoutePolicyEntryWithVpnAttachment |You are not authorized to create route policy entry with vpn attachment on Transit Router. |No permission to create route policy entries for attaching VPN attachments. Enable the allowlist for VPN attachments with a routing type of BGP on the TR. |
|403 |Forbidden.CreateTransitRouterBgpVpnAttachment |You are not authorized to create BGP vpn attachment on Transit Router. |No permission to create VPN attachments using BGP. Enable the associated allowlist in the TR. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. Action unsupported. |
|403 |Forbidden.VpcPrefixList |You are not authorized to use prefix list. |No permission to use the prefix list. Enable the prefix list allowlist. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidTransitRouterRoutePolicy.NotFound |The specified Transit Router route policy does not exist. |The specified route policy does not exist. |
|404 |InvalidTransitRouterRoutePolicyEntry.ResourceIdNotFound |The specified Resource does not exist or is not attached to this Transit Router. |The specified network instance does not exist or is not attached to this TR. |
|409 |InvalidTransitRouterRoutePolicyEntry.ActionResultConflict |The specified route attributes operation conflicts with the action result of route policy entry. |The specified action to configure route attributes conflicts with the policy action of the route policy. Only "Permit" policies allow attribute configuration. |
|409 |InvalidTransitRouterRoutePolicyEntry.DirectionConflict |The route policy direction is In, destination resource types and ids are not supported. |An inbound route policy. It does not support configuring the destination instance type or destination instance list as the match condition. |
|409 |InvalidTransitRouterRoutePolicyEntry.IpPrefixesInvalid |Cannot specify destination CIDR and prefix list simultaneously. |Destination CIDR block and destination prefix list cannot be specified at the same time. |
|409 |InvalidTransitRouterRoutePolicyEntry.PriorityConflict |The specified priority of the Transit Router route policy entry is conflict with another entry. |The priority of the specified route policy entry conflicts with that of another entry. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
