---
title: "Common parameters"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Common-parameters"
---

Common request parameters are essential parameters required for every API request. Developers must include these parameters in every request sent via the BytePlus API, otherwise the request will fail.

<span id="84ad3794"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be included in the Query.</div>



|**Name** |**Type** |**Required** |**Format** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the API, relevant to the specific operation to be executed. |
|Version |String |Yes |YYYY\-MM\-DD |The version information of the API, currently set to `2022-01-01`. |
|X\-Expires |Int |No |300 |The validity period of the signature, in seconds. If this parameter is not set, it is 900 seconds by default. |


<span id="9566547e"></span>
## Signature parameters

Signature parameters are required in a request, and can be included in `Header` or `Query`.


* **Signature parameters in Header**



|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |20201103T104027Z, in UTC time, accurate to the second. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |


Where, the Authorization information is explained in the table below:


|**Name** |**Type** |**Note** |
|---|---|---|
|AccessKey |String |Access key (AK) of the request. |
|ShortDate |String |The short date of the request, accurate to the day. In UTC time, for example: 20180201. |
|Region |String |Region of the request, for example: Asia Pacific (Johor), ap\-southeast\-1. |
|Service |String |Requested service, currently set to FileNAS. |
|SignedHeaders |String |Headers involved in the signature, separated by semicolons. |
|Signature |String |Calculated signature. For more information on how the signature is calculated, refer to the [Signature request](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request). |



* **Signature parameters in Query**


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="tip">The X\-Date and Authorization information can be stored in Query.</div>



|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |20201103T104027Z, in UTC time, accurate to the second. |
|X\-Algorithm |String |Yes |Always set to HMAC\-SHA256. |
|X\-Credential |String |Yes |The value is composed of {AccessKey}, {ShortDate}, {Region}, {Service}, and `request`. |
|X\-SignedHeaders |String |Yes |Headers involved in the signature, separated by semicolons. |
|X\-Signature |String |Yes |Calculated signature.For more information on how the signature is calculated, refer to the [Signature request](https://docs.byteplus.com/en/docs/byteplus-platform/reference-signature-request). |


For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
