---
title: "UntagResources - Disassociating custom tags"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/UntagResources"
---

Call the UntagResources API to disassociate custom tags from resources.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=UntagResources&groupName=%E6%A0%87%E7%AD%BE&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|CH01Py">必选</span> `Example: UntagResources`

The action that you want to perform. Value: UntagResources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|IazleI">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**ResourceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|EhFT79">必选</span> `Example: ngw-273w3e33y2y9s7fap8u2j***`

ID of the NAT gateway.


* Parameter \- N: Represents the serial number of a resource ID. A maximum of 50 IDs can be specified per single API call.

* Separate multiple resource IDs with ampersands (&).



**ResourceType ** <span data-label="purple">string </span><span data-api-tag="require|9uzOBc">必选</span> `Example: ngw`

The type of the tagged resource. Currently only "ngw" (NAT gateway instance) is supported.



**TagKeys.N ** <span data-label="purple">string[] </span><span data-api-tag="require|QZKAjp">必选</span> `Example: k1`

The key of the custom tag to be deleted.


* N represents the sequence number of a tag key. You can specify a maximum of 20 keys per call.

* Separate multiple tag keys with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=UntagResources&Version=2020-04-01&ResourceIds.1=ngw-273w3e33y2y9s7fap8u2j***&ResourceType=ngw&TagKeys.1=k1 HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
X-Date: 20251113T124810Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251113/cn-beijing/natgateway/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "UntagResources",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
   "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}

```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidResource.NotFound |The specified resource does not exist. |The specified resource does not exist. |
|400 |LimitExceeded.Resource |You've reached the limit on the number of resources that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidResourceType.Malformed |The specified parameter resource type is invalid. |The resource type is invalid. |
