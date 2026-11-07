---
title: "DeleteTransitRouterTrafficQosMarkingPolicy - Deleting a traffic marking policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingPolicy"
---

Call the DeleteTransitRouterTrafficQosMarkingPolicy API to delete a traffic marking policy.

<span id=".5L2_55So6K-05piO"></span>
## Notes


* The traffic marking policy is not used by an inter\-region attachment. If in use, disable the traffic marking policy for the inter\-region attachment first.

* No marking entries exist in the traffic marking policy. If present, delete the marking entries first.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Traffic marking may be impacted by deleting a traffic marking policy. If the bandwidth allocated to the scheduling queue matched by the traffic marking is insufficient for actual business requirements, normal service forwarding may be impacted.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteTransitRouterTrafficQosMarkingPolicy&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|joEu6B">必选</span> `Example: DeleteTransitRouterTrafficQosMarkingPolicy`

The interface name. The current API name is `DeleteTransitRouterTrafficQosMarkingPolicy`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|expxrG">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|eGbpBo">必选</span> `Example: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy. You can call the [DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) API to obtain the ID of the traffic marking policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteTransitRouterTrafficQosMarkingPolicy&Version=2020-04-01&TransitRouterTrafficQosMarkingPolicyId=tr-tmp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T083020Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250731163024175200203024897C98",
        "Action": "DeleteTransitRouterTrafficQosMarkingPolicy",
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
|400 |InvalidTransitRouterTrafficQosMarkingPolicy.InvalidStatus |The specified Transit Router traffic qos marking policy is not in the correct status for the request. |The specified traffic marking policy cannot respond to this request due to its status. |
|400 |InvalidTransitRouterTrafficQosMarkingPolicy.WithAssociation |The specified traffic qos marking policy has been associated to Transit Router attachments, and cannot be deleted. |The specified traffic marking policy is in use by a network instance attachment and cannot be deleted. |
|400 |InvalidTransitRouterTrafficQosMarkingPolicy.WithTrafficQosMarkingEntry |There are marking entries within the specified traffic qos marking policy, which cannot be deleted. |The specified traffic marking policy has entries configured and cannot be deleted. |
|404 |InvalidTransitRouterTrafficQosMarkingPolicy.NotFound |The specified Transit Router traffic qos marking policy does not exist. |The specified traffic marking policy does not exist. |
