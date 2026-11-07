---
title: "Common Parameters"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Public-parameters"
---

Common request parameters are those parameters that are required to call any open API. That is, whenever you use an open API of BytePlus to send a request, the request must contain common request parameters. Otherwise, your request fails. The initial letter of every common request parameter is capitalized to distinguish them from Request parameters.

<span id="Action&Version"></span>
## Action&Version

> Action and Version must be included in the query string when you make an API request.



|Name |Type  |Required |Format |Description |
|---|---|---|---|---|
|Action |String |Yes  |[a\-zA\-Z]+ |Name of an API, indicating the operation to be performed. |
|Version |String |Yes  |YYYY\-MM\-DD |The version of the API. The current version is 2020\-04\-01. |
|X\-Expires |Integer |No |300 |The validity period of the signature. Unit: seconds. Default value: 900. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters 

Signature parameters are an essential part of requests. Signature parameters can be put in the header or query.

<span id=".562-5ZCN5Y-C5pWw5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Signature parameters in `Header`


|Name |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes  |GMT time that is accurate to the second, such as 20201103T104027Z. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature} |


The Authorization part contains the following parameters.


|Name |Type  |Remark |
|---|---|---|
|AccessKey |String |AccessKey of the request. |
|ShortDate |String |The short time requested, accurate to the day. UTC time, e.g., 20180201. |
|Region |String |The Region of the request, such as cn\-beijing for China (Beijing). For more information on regions, refer to [Regions](https://docs.byteplus.com/en/docs/6407/74604). |
|Service |String |The requested service. For Direct Connect, it is: directconnect. |
|SignedHeaders |String |The headers that are used for the signature. Multiple parameter values are separated with semicolons ( ; ). |
|Signature |String |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/directconnect/Signature-method). |


<span id=".562-5ZCN5Y-C5pWw5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
### Scenarios of signature parameters in Query 

X\-Date and Authorization information can directly exist in the Query.


|Name |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes  |UTC time is used, accurate to seconds. Example: 20201103T104027Z. |
|X\-Algorithm |String |Yes  |Set the value to HMAC\-SHA256. Multiple options will be available in the future. |
|X\-Credential |String |Yes  |composed of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes  |The Header involved in the signature. Separate multiple Headers with semicolons ( ; ). |
|X\-Signature |String |Yes  |Calculated signature. For more information on the signature calculation method, refer to [Signature method](https://docs.byteplus.com/en/docs/directconnect/Signature-method). |
