---
title: "ModifyTransitRouterVpnAttachmentAttributes - Modifying a VPN attachment"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpnAttachmentAttributes"
---

Call ModifyTransitRouterVpnAttachmentAttributes to modify the information of the specified Virtual Private Network (VPN) attachment.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterVpnAttachmentAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|xpejHX">必选</span> `Example value: ModifyTransitRouterVpnAttachmentAttributes`

The interface name. The current API name is `ModifyTransitRouterVpnAttachmentAttributes`.



**Version ** <span data-label="purple"> string </span><span data-api-tag="require|1qZBE4">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterAttachmentId ** <span data-label="purple"> String  </span><span data-api-tag="require|2G4Aml">必选</span> `Example value: tr-attach-a*******`

The ID of the network instance attachment. You can call the [DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) API to obtain the ID of the Virtual Private Network (VPN) attachment.



**Description ** <span data-label="purple"> String </span>`optional` `Example value: This attachment is used for test.`

The description of the network instance attachment.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not modify this parameter value, its original configuration remains.



**TransitRouterAttachmentName ** <span data-label="purple"> String  </span>`Optional` `Example value: attachment-02`

The name of the network instance attachment.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not modify this parameter value, its original configuration remains.



**HealthCheckRevokeRouteEnabled ** <span data-label="purple"> Boolean  </span>`optional` `example value: true`

Describe whether to enable health check convergence routing.


* true: Yes. The health check convergence routing feature only takes effect when health check is enabled on the IPsec\-VPN connection. It only supports converging static routes, not BGP routes.

* false: No.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterVpnAttachmentAttributes&Version=2020-04-01&TransitRouterAttachmentId=tr-attach-a******* HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T034335Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250804114338220223058010133478",
    "Action": "ModifyTransitRouterVpnAttachmentAttributes",
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


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of the specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterAttachment.InvalidStatus |The specified Transit Router Attachment is not in the correct status for the request. |The specified network instance attachment is in a status that cannot respond to the request. |
|403 |Forbidden.EnableVpnAttachmentHealthCheckerRevokeRoute |You are not authorized to enable health checker revoke route on vpn attachment. |No permission to enable health check convergence routing for VPN. Enable the allowlist. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterAttachment.NotFound |The specified Transit Router attachment does not exist. |The specified network instance attachment does not exist. |
