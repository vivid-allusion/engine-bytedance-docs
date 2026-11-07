---
title: "ModifyTransitRouterRouteEntryAttributes - Modifying a route"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteEntryAttributes"
---

Call ModifyTransitRouterRouteEntryAttributes to modify the information of the specified route.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterRouteEntryAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|nJidda">必选</span> `Example value: ModifyTransitRouterRouteEntryAttributes`

The interface name. The current API name is `ModifyTransitRouterRouteEntryAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|KVaHG0">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteEntryId ** <span data-label="purple"> String </span> <span data-api-tag="require|_9JHG9">必选</span>`Example: tr-rte-1i5i8khf9m58gae5kcx6****`

The ID of the TR route. You can call [DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries) to get the ID of the TR route.



**TransitRouterRouteEntryName ** <span data-label="purple"> String  </span>`Optional` `Example value: routeentry-01`

The name of the route in the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, it defaults to the TR route ID.



**Description ** <span data-label="purple"> String </span>`Optional` `Example value: This transit router is used for test.`

The description of the route in the TR route table.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterRouteEntryAttributes&Version=2020-04-01&TransitRouterRouteEntryId=tr-rte-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T093309Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2025080417331312820410309491497C",
    "Action": "ModifyTransitRouterRouteEntryAttributes",
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
|400 |InvalidTransitRouterRouteEntry.RouteTypeInvalidToModify |The specified Transit Router route entry is propagated and cannot be modified. |The specified TR route is learned by route learning and does not support modifying. |
|404 |InvalidTransitRouterRouteEntry.NotFound |The specified Transit Router route entry does not exist. |The specified TR route does not exist. |
