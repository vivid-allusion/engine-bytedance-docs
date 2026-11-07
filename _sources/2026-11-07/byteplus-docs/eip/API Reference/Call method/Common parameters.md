---
title: "Common parameters"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Public-parameters"
---

Common request parameters refer to the request parameters required for calling any API. That is, you must include these parameters each time you send a request using BytePlus OpenAPI; otherwise, the request will fail.

The first letter of each common request parameter is capitalized to distinguish it from other request parameters.

<span id="Action&Version"></span>
## Action&Version

> Action and Version must be included in the Query.



|Name |Type |Required |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |API name that is related to the specific interface, indicating the action you want to perform. |
|Version |String |Yes |YYYY\-MM\-DD |API version number. |
|X\-Expires |Integer |No |300 |Signature validity period. Unit: seconds. If left blank, it defaults to 900. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are essential parts of the request and can be included in either the Header or the Query.

<span id=".562-5ZCN5Y-C5pWw5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Signature parameters in the Header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time with second\-level precision. For example, 20201103T104027Z. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}。 |


The meaning of parts in Authorization is as follows:


|Name |Type |Remark |
|---|---|---|
|AccessKey |String |The AccessKey information for the request. |
|ShortDate |String |Requested short time, accurate to day. Use UTC time. For example, 20180201. |
|Region |String |Region of the request. For example, Asia Pacific (Johor): cn\-beijing. For region details, see [Regions](https://docs.byteplus.com/en/docs/eip/Regions). |
|Service |String |Requested service. When calling an EIP API: vpc. |
|SignedHeaders |String |Headers involved in the signature, separated with semicolons. |
|Signature |String |Calculated signature. For more about the signature calculation method, see [Signature method](https://docs.byteplus.com/en/docs/eip/Signature-method). |


<span id=".562-5ZCN5Y-C5pWw5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
### Signature parameters in the Query

The information of X\-Date and Authorization can be directly included in the Query.


|Name |Instance type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Use UTC time with second\-level precision. For example, 20201103T104027Z. |
|X\-Algorithm |String |Yes |Fixed: HMAC\-SHA256. Prepared for future expansion. |
|X\-Credential |String |Yes |Consist of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Headers involved in the signature, separated with semicolons. |
|X\-Signature |String |Yes |Calculated signature. For more about the signature calculation method, see [Signature method](https://docs.byteplus.com/en/docs/eip/Signature-method). |
