---
title: "UntagResources - Disassociating custom tags"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/UntagResources"
---

Call the UntagResources API to disassociate custom tags from resources.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=UntagResources&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|6fsrTT">必选</span> `Example: UntagResources`

The interface name. The current API name is `UntagResources`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Mxi9SU">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**ResourceType ** <span data-label="purple"> String  </span><span data-api-tag="require|6Oxc4I">必选</span> `Example: directconnectconnection`

The type of the resource to be untagged. Values:


* directconnectconnection: Direct Connect Connection

* directconnectgateway: Direct Connect Gateway

* directconnectvirtualinterface: Direct Connect Virtual Interface



**ResourceIds.N ** <span data-label="purple"> String </span><span data-api-tag="require|7_FrGj">必选</span> `Example: dcc-lhn2cx0an18****`

The ID of the resource to be untagged.


* N represents the sequence number of a resource ID. You can specify a maximum of 50 IDs per call.

* Separate multiple resource IDs with ampersands (&).



**TagKeys.N ** <span data-label="purple"> String  </span><span data-api-tag="require|eHNbi0">必选</span> `Example: k1`

The key of the custom tag to be disassociated.


* N represents the sequence number of a tag key. You can specify a maximum of 20 keys per call.

* Separate multiple tag keys with ampersands (&).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=UntagResources&Version=2020-04-01&ResourceType=directconnectconnection&ResourceIds.1=dcc-lhn2cx0an18****&TagKeys.1=k1 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UntagResources",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
 "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
