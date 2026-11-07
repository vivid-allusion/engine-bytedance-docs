---
title: "DeleteTransitRouterMulticastDomain - Deleting Multicast Domain"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastDomain"
---

Call the DeleteTransitRouterMulticastDomain API to delete the specified multicast domain.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterMulticastDomain&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|2RYJQo">必选</span>`Example value: DeleteTransitRouterMulticastDomain`

The interface name. The current API name is `DeleteTransitRouterMulticastDomain`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|hYL7iY">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterMulticastDomainId ** <span data-label="purple">String </span><span data-api-tag="require|7jMLCy">必选</span> `Example value: tr-md-hy13n2l4c6c0v****`

The ID of the multicast domain. You can call the [DescribeTransitRouterMulticastDomains](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains) API to obtain the multicast domain ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterMulticastDomain&Version=2020-04-01&TransitRouterMulticastDomainId=tr-md-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T121906Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250721201910233175070238E85E58",
        "Action": "DeleteTransitRouterMulticastDomain",
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
|400 |InvalidTransitRouterMulticastDomain.InvalidStatus |The specified Transit Router multicast domain is not in the correct status for the request. |The specified multicast domain cannot respond to this request due to its status. |
|400 |InvalidTransitRouterMulticastDomain.WithAssociation |The specified multicast domain has been associated with subnets, and cannot be deleted. |The specified multicast domain cannot be deleted because it is associated with subnets. |
|400 |InvalidTransitRouterMulticastDomain.WithMulticastGroup |There are multicast groups within the specified multicast domain, which cannot be deleted. |The specified multicast domain contains multicast groups and cannot be deleted. |
|404 |InvalidTransitRouterMulticastDomain.NotFound |The specified Transit Router multicast domain does not exist. |The specified multicast domain does not exist. |
