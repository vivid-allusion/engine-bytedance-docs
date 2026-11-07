---
title: "Public parameter"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Public_parameter"
---

Public request parameters are required for each interface. The developers need to carry these public request parameters every time they send a request using BytePlus OpenAPI, otherwise the request will fail. Public request parameters are capitalized to distinguish them from other request parameters.

<span id="Action 和 Version"></span>
## Action and Version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be placed in Query. For example: <code>? Action=CreaeFunctiont & Version = 2024-06-06</code>.</div>



|Name |Type |Required or Not |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface is related to the specific interface itself. |
|Version |String |Yes |YYYY\-MM\-DD |The version information of the interface, related to the specific interface itself. Currently only supports `2024-06-06`. |


<span id="签名参数"></span>
## Signature parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The signature parameters are an essential part of the request, and can be placed in the Header or Query.</div>


<span id="在Header中的场景"></span>
### Scene in Header


|Name |Type |Required or Not |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time, accurate to the second. Please use the format: `YYYYMMDD T'HHMMSS'Z '`, for example: `20201103T104027Z`. |
|Authorization |String |Yes |The authentication information used to verify the legitimacy of the request. The format is: `HMAC-SHA256 Credential = {AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders = {SignedHeaders}, Signature = {Signature}`. |


The meanings of information in Authorization:


|Name |Type |Remarks |
|---|---|---|
|AccessKey |String |The Access Key ID of the request. |
|ShortDate |String |The short time of the request, accurate to the day. Use UTC time, for example: `20180201`. |
|Region |String |The requested region (Region), for example: `ap-southeast-1`, represents the China (Beijing) region. For more information about regions, refer to [Server-launching region](https://docs.byteplus.com/en/docs/faas/Regions_and_availability_zones). |
|Service |String |The requested service is `vefaas` when calling the Function Service API. |
|SignedHeaders |String |Headers participating in the signature, separated by semicolons (;). |
|Signature |String |The calculated signature. For the signature calculation method, refer to the [Signature mechanism](https://docs.byteplus.com/en/docs/faas/Signature_mechanism). |


<span id="在 Query 中的场景"></span>
### Scenes in Query

The X\-Date and the information in Authorization can directly be stored in Query.


|Default CPU Request |Type |Required or Not |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time, accurate to the second, for example: `20201103T104027Z`. |
|X\-Algorithm |String |Yes |Fixed value `HMAC-SHA256`; to prepare for future expansion |
|X\-Credential |String |Yes |Consists of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |Headers participating in the signature, separated by semicolons (;). |
|X\-Signature |String |Yes |The calculated signature. For the signature calculation method, refer to the [Signature mechanism](https://docs.byteplus.com/en/docs/faas/Signature_mechanism). |
