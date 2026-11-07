---
title: "Common parameters"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Public_parameters"
---

Common request parameters are required for every API operation. Developers must include these common request parameters each time they send a request using BytePlus platform APIs. Otherwise, the request will fail. The initial letter of each common request parameter is capitalized to distinguish them from request parameters specific to each API operation.

<span id="Action&Version"></span>
### Action&Version

> Action and Version must be included in the query string.



|Name |Type |Required |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the operation, which specifies the operation you want to perform. |
|Version |String |Yes |YYYY\-MM\-DD |The version information of the API. The current version is 2020\-04\-01. |
|X\-Expires |Int |No |300 |The validity period of the signature measured in seconds. Default value: 900. |


<span id=".562-5ZCN5Y-C5pWw"></span>
### Signature parameters

> Signature parameters are an essential part of the request and can be placed in either the request header or the query string.


<span id=".5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
#### Scenarios where signature parameters are placed in the request header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |20201103T104027Z. Use UTC time, accurate to seconds. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |


The following table describes the fields included in Authorization.


|Name |Type |Remarks |
|---|---|---|
|AccessKey |String |The AK of the request. |
|ShortDate |String |The short date of the request, accurate to days. Use UTC time. Example: 20180201. |
|Region |String |The region of the requested resource. Example: Asia Pacific (Johor):ap\-southeast\-1.<br><br>For more information about regions, see [Region and availability zone](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones). |
|Service |String |The requested service. To call the SMC API, set this parameter to `smc`. |
|SignedHeaders |String |The headers involved in the signature. Separate multiple headers with semicolons. |
|Signature |String |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/smc/Signature_method). |


<span id=".5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
#### Scenarios where signature parameters are placed in the query string

X\-Date and Authorization information can be directly included in the query string.


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |20201103T104027Z. Use UTC time, accurate to seconds. |
|X\-Algorithm |String |Yes |Fixed value: HMAC\-SHA256. This field is used to prepare for future expansion. |
|X\-Credential |String |Yes |The format is {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Request headers included in the signature calculation, separated with semicolons. |
|X\-Signature |String |Yes |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/smc/Signature_method). |
