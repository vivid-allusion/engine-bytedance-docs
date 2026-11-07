---
title: "ModifyTransitRouterRoutePolicyAssociation - Modifying the TR route table attached to the route policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyAssociation"
---

Call the ModifyTransitRouterRoutePolicyTableAssociation API to modify the Transit Router (TR) route table associated with the specified route policy.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterRoutePolicyAssociation&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|FUOvW9">必选</span> `Example value: ModifyTransitRouterRoutePolicyAssociation`

The interface name. The current API name is `ModifyTransitRouterRoutePolicyAssociation`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|tsCzoX">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRoutePolicyTableId ** <span data-label="purple">String </span><span data-api-tag="require|UjtiOv">必选</span> `Example value: tr-rpt-1i5i8khf9m58gae5kcx6****`

The ID of the route policy. You can call the [DescribeTransitRouterRoutePolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables) API to obtain the ID of the route policy.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|wwM7Ub">必选</span> `Example: tr-rtb-13n2l4c****`

ID of the TR route table. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



**Direction ** <span data-label="purple">String </span><span data-api-tag="require|6LdvDJ">必选</span> `Example value: In`

The direction of the route policy. Values:


* In: Inbound. The direction that TR receives routes from a network instance only if they meet the route policy.

* Out: Outbound. The direction that TR synchronizes routes to a network instance only if they meet the route policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyTransitRouterRoutePolicyAssociation&Version=2020-04-01&TransitRouterRoutePolicyTableId=tr-rpt-1i5i8khf9m58gae5kcx6****&TransitRouterRouteTableId=tr-rtb-13n2l4c****&Direction=In HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T033902Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202508151139061161220101608776B8",
        "Action": "ModifyTransitRouterRoutePolicyAssociation",
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
|400 |InvalidRoutePolicy.DirectionInvalid |The specified Transit Router route policy direction is invalid, only In and Out are supported. |The specified route policy direction is invalid. Only In and Out are supported. |
|400 |InvalidTransitRouter.InvalidBusinessStatus |The request is denied because the specified Transit Router is shut down due to arrears. |The specified Transit Router (TR) is suspended due to overdue payments. Action unsupported. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterRoutePolicyAssociation.TransitRouterMismatch |The specified route table and route policy do not belong to one same Transit Router. |The specified route table does not belong to the TR associated with the route policy. |
|400 |InvalidTransitRouterRouteTable.RoutePolicyTableNotAssociated |The route policy has not been associated with the Transit Router route table. |This route policy is not configured for the specified route table. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouterRoutePolicy.NotFound |The specified Transit Router route policy does not exist. |The specified route policy does not exist. |
|404 |InvalidTransitRouterRouteTable.NotFound |The specified route table does not exist. |The specified Transit Router (TR) route table does not exist. |
|409 |InvalidTransitRouterRoutePolicyAssociation.DirectionConflict |The specified direction conflicts with the direction of the Transit Router route policy. |The specified direction conflicts with the direction of the route policy. |
