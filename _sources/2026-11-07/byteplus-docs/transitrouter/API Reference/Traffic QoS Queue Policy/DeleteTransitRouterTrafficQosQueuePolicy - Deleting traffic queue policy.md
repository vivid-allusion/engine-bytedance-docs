---
title: "DeleteTransitRouterTrafficQosQueuePolicy - Deleting traffic queue policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosQueuePolicy"
---

Call the DeleteTransitRouterTrafficQosQueuePolicy API to delete the specified traffic queue policy.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* The traffic queue policy is not used by an inter\-region attachment. If in use, disable the traffic queue policy for the inter\-region attachment first.

* No custom queues exist in the traffic queue policy. If present, delete the custom queues first.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterTrafficQosQueuePolicy&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|p524qZ">必选</span> `Example: DeleteTransitRouterTrafficQosQueuePolicy`

The interface name. The current API name is `DeleteTransitRouterTrafficQosQueuePolicy`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|9xjyx6">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosQueuePolicyId ** <span data-label="purple">String </span><span data-api-tag="require|8JbQpx">必选</span> `Example value: tr-tqp-hy13n2l4c6c0v****`

ID of the traffic queue policy. You can call the [DescribeTransitRouterTrafficQosQueuePolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueuePolicies) API to obtain the traffic queue policy ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterTrafficQosQueuePolicy&Version=2020-04-01&TransitRouterTrafficQosQueuePolicyId=tr-tqp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T091001Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202507311710042190301681138F2308",
        "Action": "DeleteTransitRouterTrafficQosQueuePolicy",
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
|400 |InvalidTransitRouterTrafficQosQueuePolicy.InvalidStatus |The specified Transit Router traffic qos queue policy is not in the correct status for the request. |The specified traffic queue policy cannot respond to this request due to its status. |
|400 |InvalidTransitRouterTrafficQosQueuePolicy.WithAssociation |The specified traffic qos queue policy has been associated to Transit Router attachments, and cannot be deleted. |The specified traffic queue policy is currently used by a network instance attachment and cannot be deleted. |
|400 |InvalidTransitRouterTrafficQosQueuePolicy.WithTrafficQosQueueEntry |There are queue entries within the specified traffic qos queue policy, which cannot be deleted. |The specified traffic queue policy has custom queues configured and cannot be deleted. |
|404 |InvalidTransitRouterTrafficQosQueuePolicy.NotFound |The specified Transit Router traffic qos queue policy does not exist. |The specified traffic queue policy does not exist. |
