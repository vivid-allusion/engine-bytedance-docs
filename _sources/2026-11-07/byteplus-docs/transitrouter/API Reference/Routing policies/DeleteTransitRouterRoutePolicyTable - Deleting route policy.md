---
title: "DeleteTransitRouterRoutePolicyTable - Deleting route policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRoutePolicyTable"
---

Call the DeleteTransitRouterRoutePolicyTable API to delete the specified route policy.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterRoutePolicyTable&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|8cDMPP">必选</span> `Example value: DeleteTransitRouterRoutePolicyTable`

The interface name. The current API name is `DeleteTransitRouterRoutePolicyTable`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|F7vtvE">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRoutePolicyTableId ** <span data-label="purple">String </span><span data-api-tag="require|DRFlJS">必选</span>` Example value: tr-rpt-hy13n2l4c6c0v****`

The ID of the route policy. You can call the [DescribeTransitRouterRoutePolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables) API to obtain the ID of the route policy.



**Force ** <span data-label="purple">Boolean </span><span data-api-tag="require|cAQHnZ">必选</span> `Example value: true`

Specify whether to force delete the route policy. Valid values:


* `true`: Force delete.

* `false`: Not force delete.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterRoutePolicyTable&Version=2020-04-01&TransitRouterRoutePolicyTableId=tr-rpt-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T033444Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250815113447224075072138E42058",
        "Action": "DeleteTransitRouterRoutePolicyTable",
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
|400 |InvalidTransitRouterRoutePolicy.InUse |The specified route policy has been used by Transit Router route tables, and cannot be deleted. |The specified TR route policy cannot be deleted because it is currently associated with a TR route table. |
|400 |InvalidTransitRouterRoutePolicy.InvalidStatus |The specified Transit Router route policy is not in the correct status for the request. |The specified route policy is in a status that cannot respond to this request. |
|400 |InvalidTransitRouterRoutePolicy.WithRoutePolicyEntry |The specified route policy has configured route policy entries, and cannot be deleted. |The specified TR route policy table contains configured policy entries and cannot be deleted. |
|404 |InvalidTransitRouterRoutePolicy.NotFound |The specified Transit Router route policy does not exist. |The specified route policy does not exist. |
