---
title: "Public parameters"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Public-parameters"
---

Public request parameters are used during all API calls. Each time you use a BytePlus API to send a request, the request must contain these public parameters. Otherwise, the request fails.

The first letter of each public request parameter must be in uppercase to distinguish it from other request parameters.

<span id="action-version"></span>
## Action&Version

> The parameters Action and Version must be included in Query.



|**Name** |**Type** |**Required** |**Format** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |Name of an API operation, indicating the action to be performed. |
|Version |String |Yes |YYYY\-MM\-DD |API version number. Current version: 2020\-04\-01. |
|X\-Expires |Int |No |300 |Validity period of the signature, in seconds. If this parameter is not specified, the default value 900 is used. |


<span id="signature-parameters"></span>
## Signature parameters

Signature parameters are required in a request and can be included in Header or Query.

<span id="signature-parameters-in-header"></span>
### Signature parameters in Header


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |UTC time, accurate to seconds. Example: 20201103T104027Z. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |


Parameters in Authorization:


|**Name** |**Type** |**Description** |
|---|---|---|
|AccessKey |String |Access Key information in a request. |
|ShortDate |String |Short date requested, accurate to the day. UTC time is used. Example: 20180201 |
|Region |String |Region of the request. Example: Asia Pacific (Johor): ap\-southeast\-1<br><br>For details about region information, refer to [Regions and availability zones](https://docs.byteplus.com/en/docs/clb/Product-Overview-08). |
|Service |String |Requested service. The value is clb when a CLB API is called. |
|SignedHeaders |String |Signed headers. Multiple values are separated by semicolons ( ; ). |
|Signature |String |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/clb/Signature-method). |


<span id="signature-parameters-in-query"></span>
### Signature parameters in Query

The parameters X\-Date and Authorization can be directly stored in Query.


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |UTC time, accurate to seconds. Example: 20201103T104027Z |
|X\-Algorithm |String |Yes |The value is always HMAC\-SHA256. This is a preparation for future expansion. |
|X\-Credential |String |Yes |The value is composed of {AccessKey}, {ShortDate}, {Region}, {Service}, and request. |
|X\-SignedHeaders |String |Yes |Signed headers. Multiple values are separated by semicolons ( ; ). |
|X\-Signature |String |Yes |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/clb/Signature-method). |
