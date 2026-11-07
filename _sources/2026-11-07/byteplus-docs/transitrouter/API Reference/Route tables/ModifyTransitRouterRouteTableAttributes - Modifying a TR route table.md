---
title: "ModifyTransitRouterRouteTableAttributes - Modifying a TR route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteTableAttributes"
---

Call the ModifyTransitRouterRouteTableAttributes API to modify the name and description of the specified Transit Router (TR) route table.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterRouteTableAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|u_L2PL">必选</span> `Example value: ModifyTransitRouterRouteTableAttributes`

The interface name. The current API name is `ModifyTransitRouterRouteTableAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|pw7ZnS">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteTableId ** <span data-label="purple"> String  </span><span data-api-tag="require|TRJnbN">必选</span> `Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the Transit Router (TR) instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



**Description ** <span data-label="purple"> String </span>`optional` `Example value: This transit router is used for test.`

Description of the route in the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, the original configuration is retained.



**TransitRouterRouteTableName ** <span data-label="purple"> String </span>`optional` `example: routetable-02`

Name of the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, the original configuration is retained.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterRouteTableAttributes&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T035457Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250804115500113148157013BC2934",
    "Action": "ModifyTransitRouterRouteTableAttributes",
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
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
