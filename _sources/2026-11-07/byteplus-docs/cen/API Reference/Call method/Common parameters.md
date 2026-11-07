---
title: "Common parameters"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Public-parameters"
---

Common request parameters are the set of parameters required for every API call. This means that each time you send a request using the platform's OpenAPI, you must include these common parameters; otherwise, the request will fail.

The first letter of each common request parameter is capitalized to distinguish it from other request parameters.

<span id="Action&Version"></span>
## Action&Version

> Action and Version must be included in the Query.



|Name |Topic |Required |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |API name that is related to the specific interface, indicating the action you want to perform. |
|Version |String |Yes |YYYY\-MM\-DD |Current API version is 2020\-04\-01. |
|X\-Expires |Int |No |300 |Signature validity period. Unit: seconds. If left blank, it defaults to 900. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

> Signature parameters are essential parts of the request and can be included in either the Header or the Query.


<span id=".5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Scenario in Header


|Name |Topic |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time with second\-level precision. For example, 20201103T104027Z. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |


The meaning of parts in Authorization is as follows:


|Name |Topic |Remark |
|---|---|---|
|AccessKey |String |The AccessKey information for the request. |
|ShortDate |String |Requested short time, accurate to day. Use UTC time. For example, 20180201. |
|Region |String |The region of the request. Fixed as China (Beijing): cn\-beijing. |
|Service |String |The target service of the request. For Cloud Enterprise Network (CEN) API calls, this is cen. |
|SignedHeaders |String |Headers involved in the signature, separated with semicolons. |
|Signature |String |Calculated signature. For more information on the signature calculation method, see [Signature method](https://docs.byteplus.com/en/docs/cen/Signature-method). |


<span id=".5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
### Scenario in Query

The information of X\-Date and Authorization can be directly included in the Query.


|Name |Topic |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time with second\-level precision. For example, 20201103T104027Z. |
|X\-Algorithm |String |Yes |Fixed: HMAC\-SHA256. Prepared for future expansion. |
|X\-Credential |String |Yes |Consist of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Headers involved in the signature, separated with semicolons. |
|X\-Signature |String |Yes |Calculated signature. For more information on the signature calculation method, see [Signature method](https://docs.byteplus.com/en/docs/cen/Signature-method). |
