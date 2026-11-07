---
title: "ModifyTransitRouterTrafficQosQueuePolicyAttributes - Modifying a traffic queue policy"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosQueuePolicyAttributes"
---

Call the ModifyTransitRouterTrafficQosQueuePolicyAttributes interface to modify the name or description of the traffic queue policy.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyTransitRouterTrafficQosQueuePolicyAttributes&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String ` example: `ModifyTransitRouterTrafficQosQueuePolicyAttributes`

Interface name. The current API name is `ModifyTransitRouterTrafficQosQueuePolicyAttributes`.



**Version ** `String ` example: `2020-04-01`

Interface version. The current API version is `2020-04-01`.



**TransitRouterTrafficQosQueuePolicyId** `String` Sample value: `tr-tqp-hy13n2l4c6c0v****`

ID of the traffic queue policy. You can call the [DescribeTransitRouterTrafficQosQueuePolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueuePolicies) interface to get the ID of the traffic queue policy.



**TransitRouterTrafficQosQueuePolicyName ** `String optional` example: `tmp-02`

Name of the traffic queue policy.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not specify this parameter or leave it empty, it defaults to the traffic queue policy ID.



**Description ** `String optional` Example: `This traffic qos queue policy is used for test.`

Description of the traffic queue policy.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), Chinese commas ( ， ), and Chinese periods ( 。 ).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="EaG5BP6H"></span>
## Request examples

```JSON
GET /?Action=ModifyTransitRouterTrafficQosQueuePolicyAttributes&Version=2020-04-01&TransitRouterTrafficQosQueuePolicyId=tr-tqp-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250731T091117Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250731/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="0h6ssRUP"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "2025073117112119508011019056B023",
    "Action": "ModifyTransitRouterTrafficQosQueuePolicyAttributes",
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


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.TooLong |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of specified name is invalid. Correct the name format and retry. |
|400 |InvalidName.TooLong |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidTransitRouter.InvalidStatus |The specified Transit Router is not in the correct status for the request. |The specified TR is in a status that cannot respond to the request. |
|400 |InvalidTransitRouterTrafficQosQueuePolicy.InvalidStatus |The specified Transit Router traffic qos queue policy is not in the correct status for the request. |The specified traffic queue policy is in a state that cannot respond to this request. |
|404 |InvalidTransitRouterTrafficQosQueuePolicy.NotFound |The specified Transit Router traffic qos queue policy does not exist. |The specified traffic queue policy does not exist. |
