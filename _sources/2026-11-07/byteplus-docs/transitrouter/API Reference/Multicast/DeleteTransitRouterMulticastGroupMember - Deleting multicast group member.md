---
title: "DeleteTransitRouterMulticastGroupMember - Deleting multicast group member"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastGroupMember"
---

Call the DeleteTransitRouterMulticastGroupMember API to delete multicast members.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterMulticastGroupMember&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|JKWe0q">必选</span> `Example value: DeleteTransitRouterMulticastGroupMember`

The interface name. The current API name is `DeleteTransitRouterMulticastGroupMember`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|vOV41s">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterMulticastDomainId ** <span data-label="purple">String </span><span data-api-tag="require|u5j0JF">必选</span> `Example value: tr-md-hy13n2l4c6c0v****`

The ID of the multicast domain. You can call [DescribeTransitRouterMulticastDomains](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains) to obtain the ID of the multicast domain.



**GroupIpAddress ** <span data-label="purple">String </span><span data-api-tag="require|Ow1cjs">必选</span> `Example value: 224.0.1.0`

IP address of the multicast group.



**NetworkInterfaceId ** <span data-label="purple">String </span><span data-api-tag="require|y9J7zz">必选</span> `Example value: eni-123456`

Network Interface ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterMulticastGroupMember&Version=2020-04-01&TransitRouterMulticastDomainId=tr-md-hy13n2l4c6c0v****&GroupIpAddress=224.0.1.0&NetworkInterfaceId=eni-123456 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T122356Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202505091745180630512401165F****",
        "Action": "DeleteTransitRouterMulticastGroupMember",
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
|404 |InvalidTransitRouterMulticastGroupMember.NotFound |The specified Transit Router multicast group member does not exist. |The specified multicast member does not exist. |
