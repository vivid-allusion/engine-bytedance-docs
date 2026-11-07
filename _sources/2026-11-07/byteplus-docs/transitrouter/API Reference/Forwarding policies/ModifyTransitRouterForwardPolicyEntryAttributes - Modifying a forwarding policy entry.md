---
title: "ModifyTransitRouterForwardPolicyEntryAttributes - Modifying a forwarding policy entry"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterForwardPolicyEntryAttributes"
---

Call the ModifyTransitRouterForwardPolicyEntryAttributes API to modify the information of the specified forwarding policy entry.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterForwardPolicyEntryAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple"> String </span> <span data-api-tag="require|xYrXSM">必选</span> `Example: ModifyTransitRouterForwardPolicyEntryAttributes`

The interface name. The current API name is `ModifyTransitRouterForwardPolicyEntryAttributes`.



**Version** <span data-label="purple"> String </span> <span data-api-tag="require|cyPtjj">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterForwardPolicyEntryId** <span data-label="purple"> String </span> <span data-api-tag="require|3CaYZx">必选</span> `Example: tr-fpe-hy13n2l4c6c0v****`

The ID of the forwarding policy entry. You can call the [DescribeTransitRouterForwardPolicyEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyEntries) API to obtain the ID of the forwarding policy entry.



**SourceCidrBlock** <span data-label="purple"> String </span> `optional` `Example: 192.168.XX.XX/24`

The source CIDR block of the forwarding policy entry. Allow IPv4 and IPv6 CIDR blocks.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The IPv6 feature of TR is in the beta stage. If you need a trial, please contact your account manager.</div>




**DestinationCidrBlock** <span data-label="purple"> String </span> `optional` `Example: 192.168.XX.XX/24`

The destination CIDR block of the forwarding policy entry. Allow IPv4 and IPv6 CIDR blocks.

Leaving this parameter unset means matching all destination addresses.



**Priority** <span data-label="purple"> Integer </span> `optional` `Example: 100`

Priority of the forwarding policy entry. Value range: 1\-10000.



**TransitRouterRouteTableId** <span data-label="purple"> String </span> `optional` `Example: tr-rtb-hy13n2l4c6c0v****`

ID of the forward route table. You can call [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) to obtain the TR route table ID.



**Description** <span data-label="purple"> String </span> `optional` `Example: This forward policy entry is used for tests.`

The description of forwarding policy entry.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="aWrwzthU"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterForwardPolicyEntryAttributes&Version=2020-04-01&TransitRouterForwardPolicyEntryId=tr-fpe-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T034453Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="ueYBXQ10"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250815114457093189045080E048EB",
    "Action": "ModifyTransitRouterForwardPolicyEntryAttributes",
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
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidTransitRouter.IPv6NotSupported |The specified Transit Router does not support the IPv6 feature. |The specified TR instance does not support IPv6. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to overdue payments. The action is unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterForwardPolicyEntry.CidrVersionMismatch |The specified cidr of the Transit Router forward policy entry is invalid. The source and destination cidr must both IPv4 or IPv6. |The CIDR block of the specified forwarding policy entry is invalid. The source and destination CIDR blocks must both be IPv4 or both be IPv6. |
|400 |InvalidTransitRouterForwardPolicyEntry.InvalidStatus |The specified Transit Router forward policy entry is not in the correct status for the request. |The specified forwarding policy entry cannot respond to this request due to its status. |
|400 |InvalidTransitRouterForwardPolicyEntry.PriorityInvalid |The specified priority of the Transit Router forward policy entry is invalid. |The priority of the specified forwarding policy entry is invalid. |
|400 |InvalidTransitRouterForwardPolicyEntry.TransitRouterMismatch |The specified route table and forward policy table do not belong to the same Transit Router. |The specified route table and the forwarding policy are associated with different TRs.​​ |
|400 |InvalidTransitRouterForwardPolicyEntry.TransitRouterNotSupported |The specified cidr of the Transit Router does not support configuring the forwarding policy entries for the destination cidr. |The specified TR instance does not support configuring destination CIDR forwarding policy entries. |
|403 |Forbidden.TransitRouterIPv6 |You are not authorized to use ipv6 on Transit Router. |The IPv6 feature is not enabled for the TR. The action is unsupported. |
|404 |InvalidTransitRouterForwardPolicyEntry.NotFound |The specified Transit Router forward policy entry does not exist. |The specified forwarding policy entry does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
|409 |InvalidTransitRouterForwardPolicyEntry.PriorityConflict |The specified priority of the Transit Router forward policy entry is conflict with another entry. |The priority of the specified forwarding policy entry conflicts with that of another entry. |
