---
title: "DeleteTransitRouterRouteEntry - Deleting a static route entry"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteEntry"
---

Call the DeleteTransitRouterRouteEntry API to delete the specified static route.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterRouteEntry&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|ntFl6b">必选</span>`Example value: DeleteTransitRouterRouteEntry`

The interface name. The current API name is `DeleteTransitRouterRouteEntry`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|HTudUz">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteEntryId ** <span data-label="purple">String </span><span data-api-tag="require|cg66Xy">必选</span> `Example value: tr-rte-1i5i8khf9m58gae5kcx6****`

The route ID. You can call [DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries) to get the ID of the TR route.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterRouteEntry&Version=2020-04-01&TransitRouterRouteEntryId=tr-rte-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T035736Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250804115739146170176252EE3A48",
        "Action": "DeleteTransitRouterRouteEntry",
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


|Status code |Error codes |Error message |Explanation |
|---|---|---|---|
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterRouteEntry.RouteTypeInvalidToDelete |The specified Transit Router route entry is propagated and cannot be deleted. |The specified Transit Router (TR) route is automatically learned through route learning and cannot be deleted. |
|404 |InvalidTransitRouterRouteEntry.NotFound |The specified Transit Router route entry does not exist. |The specified TR route does not exist. |
