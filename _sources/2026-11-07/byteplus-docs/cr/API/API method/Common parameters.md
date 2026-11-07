---
title: "Common parameters"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/common-parameters"
---

The common request parameters are necessary for every successful API action. Developers use these common request parameters every time they call BytePlus API actions to send requests. The first letter of each common request parameter is capitalized, which distinguishes them from API\-specific request parameters.

<span id="action-和-version"></span>
## Action and Version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be included in the query string when you make an API request.</div>



|Name |Type |Required |Format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The API name, which specifies the name of the API action you want to call. |
|Version |String |Yes |YYYY\-MM\-DD |The API version, which specifies the version of the API action you want to call. |
|X\-Expires |Int |No |300 |The validity period for the signature in seconds, which defaults to 900. |


<span id="签名参数"></span>
## Signature

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Signature parameters are an essential part of requests. Signature parameters are included in the Header or Query.</div>


<span id="在-header-中的场景"></span>
### Signature parameters in the Header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |The UTC accurate to seconds. Use the `YYYYMMDD'T'HHMMSS'Z'` format, such as `20201103T104027Z`. |
|Authorization |String |Yes |The authentication information used to validate the validity of the request. Format: `HMAC-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


The description of Authorization is as follows:


|Name |Type |Remarks |
|---|---|---|
|AccessKey |String |The AccessKey ID of the request. |
|ShortDate |String |The short date of the request, accurate to days. Specify the UTC, such as `20180201`. |
|Region |String |The Region in which the request is made, such as `ap-southeast-1`. |
|ServiceName |String |The requested Service. When you call Container Registry (CR) API actions, this parameter is `cr`. |
|SignedHeaders |String |The header involved in signature calculation. Separate headers with semicolons ( ; ). |
|Signature |String |The calculated signature value. For more information on signature calculation methods, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature). |


<span id="在-query-中的场景"></span>
### Signature parameters in the Query

The information from X\-Date and Authorization can be directly stored in the query parameters.


|Default CPU request |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |The UTC accurate to seconds, such as `20201103T104027Z`. |
|X\-Algorithm |String |Yes |Set to the fixed value `HMAC-SHA256`. Other algorithms will be supported in the future. |
|X\-Credential |String |Yes |The credential value in the `{AccessKey}/{ShortDate}/{Region}/{Service}/request` format. |
|X\-SignedHeaders |String |Yes |The header involved in signature calculation. Separate headers with semicolons ( ; ). |
|X\-Signature |String |Yes |The calculated signature value. For more information on signature calculation methods, refer to [Signature method](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature). |
