---
title: "Default parameters"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/Common-parameters"
---

Public request parameters are mandatory for every API call to BytePlus. You must include them in each request. Otherwise, the request will fail.

These parameters are distinguished by capitalized initial letters to differentiate them from other request parameters.

<span id="action-version"></span>
## Action and Version

The `Action` and `Version` differ for each `OpenAPI`. For details, see the public parameter section of `OpenAPI`.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be placed in the Query.</div>



|**Name** |**Type** |**Required** |**Parameter format** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |API name. It varies by the target API. |
|Version |String |Yes |YYYY\-MM\-DD |Version of the API. |
|X\-Expires |Int |No |300 |The validity period of the signature in seconds. The default validity period is 900 seconds. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are an essential part of a request and can be included in the Header or Query.

<span id=".5ZyoLWhlYWRlci3kuK3nmoTlnLrmma8="></span>
### Signature parameters in Header


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |UTC time accurate down to the second in the format `YYYYMMDD'T'HHMMSS'Z'`, for example,`20201103T104027Z`. |
|Authorization |String |Yes |It is used to verify the validity of requests. The format is: `HMAC-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


The meaning of each field in Authorization is as follows:


|**Name** |**Type** |**Note** |
|---|---|---|
|AccessKey |String |Access key ID. |
|ShortDate |String |Date of the request, which is precise to the day. It uses the UTC time standard, for example, `20180201`. |
|Region |String |The target region of the request. For example, `cn-beijing` represents the China (Beijing) region. For more information about regions, see [Region restrictions](https://docs.byteplus.com/docs/cloudmonitor/Limits). |
|ServiceName |String |The service to be requested. When calling a Cloud Monitor API, set it to `cloudmonitor`. |
|SignedHeaders |String |Headers involved in signing with semicolons (`;`) as their separator. |
|Signature |String |The calculated signature. For information about signature calculation, see [Signature mechanism](https://docs.byteplus.com/en/docs/cloudmonitor/Signature-method). |


<span id=".5ZyocXVlcnnkuK3nmoTlnLrmma8="></span>
### Signature parameters in Query

X\-Date and Authorization can be included directly in the Query.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |It uses the UTC time standard with accuracy down to the second, for example, `20201103T104027Z`. |
|X\-Algorithm |String |Yes |The value is fixed as `HMAC-SHA256`, which is reserved for future extensions. |
|X\-Credential |String |Yes |It is composed of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |Headers involved in signing with semicolons (`;`) as their separator. |
|X\-Signature |String |Yes |The calculated signature. For information about signature calculation, see [Signature mechanism](https://docs.byteplus.com/en/docs/cloudmonitor/Signature-method). |


&nbsp;
