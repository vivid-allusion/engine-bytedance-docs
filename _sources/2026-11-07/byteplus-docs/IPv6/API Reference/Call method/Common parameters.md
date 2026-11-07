---
title: "Common parameters"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Public_parameters"
---

Common request parameters refer to the request parameters required for calling any API. That is, you must include these parameters each time you send a request using BytePlus OpenAPI. Otherwise, the request may fail.

The first letter of each common request parameter is capitalized to distinguish it from other request parameters.

<span id="Action&Version"></span>
## Action & Version

> Action and Version must be included in the Query.



|Name |Topic |Required |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |API name that is related to the specific interface, indicating the action you want to perform. |
|Version |String |Yes |YYYY\-MM\-DD |Version information of OpenAPI. |
|X\-Expires |Integer |No |300 |Signature validity period. Unit: seconds. If left blank, it defaults to 900. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are essential parts of the request and can be included in either the Header or the Query.

<span id=".562-5ZCN5Y-C5pWw5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Signature parameters in the Header


|Name |Topic |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time with second\-level precision. For example, 20201103T104027Z. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |


The meaning of parts in Authorization is as follows:


|Name |Topic |Remark |
|---|---|---|
|AccessKey |String |The AccessKey information for the request. |
|ShortDate |String |The short\-formatted time of the request with day\-level precision.​ Use UTC time. For example, 20180201. |
|Region |String |Region of the request. For example, China (Beijing): cn\-beijing. For region details, see [Regions](https://docs.byteplus.com/en/docs/IPv6/Regions). |
|Service |String |The requested service, called vpc when invoking the OpenAPI of the IPv6 Gateway. |
|SignedHeaders |String |Headers involved in the signature, separated with semicolons. |
|Signature |String |Calculated signature. For more about the signature calculation method, see [Signature method](https://docs.byteplus.com/en/docs/IPv6/Signature_method). |


<span id=".562-5ZCN5Y-C5pWw5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
### Signature parameters in the Query

The information of X\-Date and Authorization can be directly included in the Query.


|Name |Topic |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time with second\-level precision. For example, 20201103T104027Z. |
|X\-Algorithm |String |Yes |Fixed: HMAC\-SHA256. Prepared for future expansion. |
|X\-Credential |String |Yes |Consist of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Headers involved in the signature, separated with semicolons. |
|X\-Signature |String |Yes |Calculated signature. For more about the signature calculation method, see [Signature method](https://docs.byteplus.com/en/docs/IPv6/Signature_method). |
