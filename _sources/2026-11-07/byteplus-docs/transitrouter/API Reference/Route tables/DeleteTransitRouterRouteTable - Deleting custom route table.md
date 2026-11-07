---
title: "DeleteTransitRouterRouteTable - Deleting custom route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteTable"
---

Call the DeleteTransitRouterRouteTable API to delete the specified custom route table.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterRouteTable&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DPlt9n">必选</span> `Example value: DeleteTransitRouterRouteTable`

The interface name. The current API name is `DeleteTransitRouterRouteTable`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Q8Ya5h">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|3k6sj9">必选</span> `Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the Transit Router (TR) instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterRouteTable&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033105Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202508041131081261822251826EF74D",
        "Action": "DeleteTransitRouterRouteTable",
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
|400 |InvalidTransitRouterRouteTable.DeleteSystemRouteTable |The specified route table is system route table, and can not be deleted. |The specified TR route table is a system route table and cannot be deleted. |
|400 |InvalidTransitRouterRouteTable.WithAssociation |The specified route table has dependent route table associations. |The specified Transit Router (TR) route table has association forwarding configured and cannot be deleted. |
|400 |InvalidTransitRouterRouteTable.WithForwardPolicyEntry |The specified route table has dependent forward policy entry, and cannot be deleted. |The specified TR route table is referenced by forward policy entries and cannot be deleted. |
|400 |InvalidTransitRouterRouteTable.WithRouteEntry |The specified route table has configured static route entries, and cannot be deleted. |The specified TR route table contains custom static route entries and cannot be deleted. |
|400 |InvalidTransitRouterRouteTable.WithRouteTablePropagation |The specified route table has configured propagations, and cannot be deleted. |The specified TR route table has route learning configured and cannot be deleted. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
