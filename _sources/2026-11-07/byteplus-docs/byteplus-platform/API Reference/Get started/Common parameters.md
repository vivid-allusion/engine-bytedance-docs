---
title: "Common parameters"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters"
---

The common parameters in BytePlus API requests are as follows:

<span id="2367680f"></span>
## `Action` and `Version`

`Action` and `Version` must be included in the query of an API request.


|**Name** |**Data type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. Format: `[a-zA-Z]+`. For example, `ListActivityAPI`. |
|Version |String |Yes |API version. Format: `YYYY-MM-DD`. For example, `2020-06-01`. |
|X\-Expires |Integer |No |The validity period of the signature (unit: second). The default value is `900`. |


<span id="89a4cb5c"></span>
## Authentication Parameters

The authentication parameters can be included in the header or query of an API request.

**In header:** 


|**Name** |**Data type** |**Required** |**Description** |
|---|---|---|---|
|Host |String |Yes |Service address for HTTP requests, which varies by product. Refer to the API reference of the product you use for details. |
|Content\-Type |String |Yes |The MIME type of the request body. |
|X\-Date |String |Yes |The timestamp of the API request in UTC format (unit: second). For example, `20201103T104027Z`. |
|Authorization |String |Yes |Format: `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |
|X\-Security\-Token |String |No |The temporary session token issued by the [Security Token Service (STS) API](https://docs.byteplus.com/byteplus-platform/reference/assumerole). Not required when using a long\-term access key. |


Parameters for generating `Authorization` are as follows:


|**Name** |**Data type** |**Description** |
|---|---|---|
|AccessKeyId |String |The access key of the BytePlus user account. Go to **BytePlus Console** \> **User Profile** \> **IAM** \> **Key Management** to obtain it. |
|ShortDate |String |The date of the API request. Format: `YYYYMMDD`. For example, `20180201`. |
|Region |String |The region of the API service. For example, `ap-singapore-1`. |
|Service |String |The name of the API service. For example, `livesaas`. |
|SignedHeaders |String |The headers that are included in generating the signature. Separate them by semicolon. |
|Signature |String |The calculated signature. |


**In query:** 


|**Name** |**Data type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |The timestamp of the API request in UTC format (unit: second). For example, `20201103T104027Z`. |
|X\-Algorithm |String |Yes |The value of this parameter is fixed as `HMAC-SHA256`. |
|X\-Credential |String |Yes |Composed by `{AccessKeyId}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |The headers that are included in generating the signature. Separate them by semicolon. |
|X\-Signature |String |Yes |The calculated signature. |
