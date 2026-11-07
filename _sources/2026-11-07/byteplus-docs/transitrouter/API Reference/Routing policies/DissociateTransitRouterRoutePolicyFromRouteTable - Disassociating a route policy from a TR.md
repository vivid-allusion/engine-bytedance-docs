---
title: "DissociateTransitRouterRoutePolicyFromRouteTable - Disassociating a route policy from a TR route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterRoutePolicyFromRouteTable"
---

Call the DissociateTransitRouterRoutePolicyFromRouteTable API to disassociate the specified route policy from the specified Transit Router (TR) route table.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DissociateTransitRouterRoutePolicyFromRouteTable&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|PIeOAc">必选</span> `Example value: DissociateTransitRouterRoutePolicyFromRouteTable`

The interface name. The current API name is `DissociateTransitRouterRoutePolicyFromRouteTable`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|JoQzpb">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRoutePolicyTableId** <span data-label="purple">String</span> <span data-api-tag="require|9ohvFX">必选</span> `Example value: tr-rpt-1i5i8khf9m58gae5kcx6****`

The ID of the route policy. You can call the [DescribeTransitRouterRoutePolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables) API to obtain the ID of the route policy.



**TransitRouterRouteTableId** <span data-label="purple">String</span> <span data-api-tag="require|Tf4hAr">必选</span>`Example value: tr-rtb-13n2l4c****`

ID of the TR route table. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DissociateTransitRouterRoutePolicyFromRouteTable&Version=2020-04-01&TransitRouterRoutePolicyTableId=tr-rpt-1i5i8khf9m58gae5kcx6****&TransitRouterRouteTableId=tr-rtb-13n2l4c**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T033957Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250815114000202101180148F414A8",
        "Action": "DissociateTransitRouterRoutePolicyFromRouteTable",
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
|400 |InvalidTransitRouterRouteTable.RoutePolicyTableNotAssociated |The route policy has not been associated with the Transit Router route table. |This route policy is not configured for the specified route table. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterRoutePolicy.NotFound |The specified Transit Router route policy does not exist. |The specified route policy does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
