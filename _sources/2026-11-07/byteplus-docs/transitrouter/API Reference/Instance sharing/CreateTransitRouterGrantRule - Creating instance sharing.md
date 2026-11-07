---
title: "CreateTransitRouterGrantRule - Creating instance sharing"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterGrantRule"
---

Call the CreateTransitRouterGrantRule API to create instance sharing and authorize the specified Transit Router (TR) instance to other accounts.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateTransitRouterGrantRule&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|2PaRs-">必选</span> `Example: CreateTransitRouterGrantRule`

The interface name. The current API name is `CreateTransitRouterGrantRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|ufXkKL">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple"> String  </span><span data-api-tag="require|J-kzTO">必选</span> `Example: tr-7qthudw0ll6jmc****`

The TR instance ID. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**Description ** <span data-label="purple"> String  </span>`optional` `Example: rule01`

Description information of the shared rule.


* Must start with a letter or Chinese character and may include numbers, commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas (，), and Chinese periods (。).

* Must be 1 to 255 characters.

* If you omit this parameter or set it to an empty value, it defaults to an empty string.



**GrantAccountId ** <span data-label="purple"> String  </span><span data-api-tag="require|Y87Lef">必选</span> `Example: 210001****`

ID of the account to which the TR instance to be authorized belongs. You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to get the account ID for authorization.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateTransitRouterGrantRule&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc****&GrantAccountId=210001**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250804113541206111202004393748",
    "Action": "CreateTransitRouterGrantRule",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidResourceShare.InvalidGrantRuleSourceType |The specified grant rule source type is invalid. |The specified TR authorization rule source is incorrect. The current action is unsupported. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified TR is suspended due to arrears. The current action is unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterGrantRule.InvalidAccount |The specified granted account is equal to the login account, please change the account to grant. |The specified account for authorization is the same as the current account. Change another account to authorize. |
|400 |QuotaExceeded.GrantRule |You've reached the maximum number of grant rules that one transit router can have. |You have reached the maximum of authorization rules that you can create for a single TR. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|403 |Forbidden.SelfShareNotSupported |You are not authorized to enable self share. |No permission to create a legacy version shared TR. Enable the allowlist. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified TR does not exist. |
|409 |InvalidTransitRouterGrantRule.AccountTypeConflict |The request is denied because the specified account and the login account belong to different cloud types, or the specified account has no permission for the region of this TransitRouter instance. |The recipient account differs from the sharer account type, or the recipient lacks permission to use this region, so this operation is not supported. |
|409 |InvalidTransitRouterGrantRule.Conflict |The specified grant rule has already been existed in the Transit Router. |This authorization rule already exists on the specified TR. Duplicate action is not allowed. |
