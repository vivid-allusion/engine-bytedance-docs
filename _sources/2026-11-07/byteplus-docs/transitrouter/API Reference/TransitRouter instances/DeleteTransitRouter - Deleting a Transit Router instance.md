---
title: "DeleteTransitRouter - Deleting a Transit Router instance"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouter"
---

Call DeleteTransitRouter to delete the specified Transit Router (TR) instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouter&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|YXyiuf">必选</span> `Example value: DeleteTransitRouter`

The interface name. The current API name is `DeleteTransitRouter`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|qioUGW">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple">String </span><span data-api-tag="require|ymLwVb">必选</span> `Example value: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouter&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033306Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202508041133111770960270689A17D8",
        "Action": "DeleteTransitRouter",
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
|400 |InvalidTransitRouter.DefaultRouteTableWithRouteEntry |The specified Transit Router has route entries in its system route table, and cannot be deleted. |The specified TR system route table contains custom routes and cannot be deleted. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified Transit Router (TR) is in a status that cannot respond to the request. |
|400 |InvalidTransitRouter.WithAttachment |The specified Transit Router has attachments, and cannot be deleted. |The specified TR contains network instances and cannot be deleted. |
|400 |InvalidTransitRouter.WithCustomizedRouteTable |The specified Transit Router has customized route tables, and cannot be deleted. |The specified TR contains custom route tables and cannot be deleted. |
|400 |InvalidTransitRouter.WithForwardPolicyTable |The specified Transit Router has forward policy tables, and cannot be deleted. |The specified TR contains forwarding policies and cannot be deleted. |
|400 |InvalidTransitRouter.WithGrantRule |The specified Transit Router has grant rules and cannot be deleted. |The specified TR contains authorization rules and cannot be deleted. |
|400 |InvalidTransitRouter.WithMulticastDomain |The specified Transit Router has multicast domains, and cannot be deleted. |The specified transit router cannot be deleted because it contains multicast domains. |
|400 |InvalidTransitRouter.WithRoutePolicy |The specified Transit Router has route policies, and cannot be deleted. |The specified TR contains route policies and cannot be deleted. |
|400 |InvalidTransitRouter.WithTrafficQosMarkingPolicy |The specified Transit Router has traffic qos marking policies, and cannot be deleted. |The specified TR contains traffic marking policies and cannot be deleted. |
|400 |InvalidTransitRouter.WithTrafficQosQueuePolicy |The specified Transit Router has traffic qos queue policies, and cannot be deleted. |The specified TR contains traffic queue policies and cannot be deleted. |
|403 |Forbidden.NoPermissionToOperate |You are not authorized to operate the specified resource. |No permission to manage the specified resource. |
|404 |InvalidTransitRouter.NotFound |The specified Transit Router does not exist. |The specified Transit Router (TR) does not exist. |
