---
title: "Common Parameters"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Public-parameters"
---

Common request parameters are required each time you call an API to send a request. If any of the common request parameters are not included, the request fails.

The initial letter of every common request parameter is capitalized to distinguish them from API\-specific request parameters.

<span id="Action&Version"></span>
## Action&Version

> Action and Version must be included in the query string when you make an API request.



|Name |Type  |Required |Format |Description |
|---|---|---|---|---|
|Action |String |Yes  |[a\-zA\-Z]+ |Name of an API, indicating the operation to be performed. |
|Version |String |Yes  |YYYY\-MM\-DD |The version number of the API. The current version is 2020\-04\-01. |
|X\-Expires |Int |No |300 |Validity period of the signature. Unit: seconds. If you do not enter any value, 900 is used by default. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are required in a request, and can be included in 'Header' or 'Query'.

<span id=".5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Signature parameters in Header


|Name |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes  |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
|Authorization |String |Yes  |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |


Parameters in Authorization:


|Name |Type  |Remark |
|---|---|---|
|AccessKey |String |AccessKey of the request. |
|ShortDate |String |Short date of the request, accurate to the day. UTC time, e.g., 20180201. |
|Region |String |The Region ID for the request, such as cn\-guangzhou.<br><br>For more information on Regions, refer to [Region sets and Regions](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-05). |
|Service |String |The service to be requested. Set the value to transitrouter when you call the Transit Router (TR) API. |
|SignedHeaders |String |The headers that are used for the signature. Multiple parameter values are separated with semicolons ( ; ). |
|Signature |String |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/transitrouter/Signature-method). |


<span id=".5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
### Signature parameters in Query

The X\-Date parameter and the Authorization parameter can be stored in `Query`.


|Name |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
|X\-Algorithm |String |Yes  |Set the value to HMAC\-SHA256. |
|X\-Credential |String |Yes  |composed of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |The Header involved in the signature. Separate multiple Headers with semicolons ( ; ). |
|X\-Signature |String |Yes  |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/transitrouter/Signature-method). |
