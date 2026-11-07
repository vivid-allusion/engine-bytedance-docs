---
title: "Common Parameters"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Public-parameters"
---

Common request parameters are those parameters that are required to call any open API. That is, whenever you use an open API of BytePlus to send a request, the request must contain common request parameters. Otherwise, your request fails.

The initial letter of every common request parameter is capitalized to distinguish them from API request parameters.

<span id="Action&Version"></span>
## Action&Version

> Action and Version must be included in the query string when you make an API request.



|Term |Type  |Required |Format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |Name of an API, indicating the operation to be performed. |
|Version |String |Yes   |YYYY\-MM\-DD |API version information, value is: 2020\-04\-01. |
|X\-Expires |Integer |No  |300 |The validity period of the signature. Unit: seconds. Default value: 900. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are required in a request and can be included in Header or Query.

<span id=".562-5ZCN5Y-C5pWw5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Signature parameters in `Header`


|Term |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes   |GMT time that is accurate to the second, such as 20201103T104027Z. |
|Authorization |String |Yes   |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |


Parameters in Authorization:


|Term |Type  |Remark |
|---|---|---|
|AccessKey |String |AccessKey of the request. |
|ShortDate |String |The short time requested, accurate to the day. UTC time, e.g., 20180201. |
|Region |String |The Region of the request, such as cn\-beijing for China (Beijing). For more information on Regions and Availability Zones, [refer to Regions and Availability Zones](https://docs.byteplus.com/en/docs/vpc/Regions-and-Availability-Zones). |
|Service |String |The requested Service, when calling the Virtual Private Cloud (VPC) API, is: vpc. |
|SignedHeaders |String |The Header involved in the signature. Separate multiple Headers with semicolons ( ; ). |
|Signature |String |The signature that is calculated. For more information on the signature calculation method, refer to [Signature Method](https://docs.byteplus.com/en/docs/vpc/Signature-method). |


<span id=".562-5ZCN5Y-C5pWw5ZyoUXVlcnnkuK3nmoTlnLrmma8="></span>
### Signature parameters in `Query`

The parameters X\-Date and Authorization can be directly stored in Query.


|Term |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes   |UTC time is used, accurate to seconds. Example: 20201103T104027Z. |
|X\-Algorithm |String |Yes   |Set the value to HMAC\-SHA256. Multiple options will be available in the future. |
|X\-Credential |String |Yes   |composed of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes   |The headers that are used for the signature. Separate multiple headers semicolons ( ; ). |
|X\-Signature |String |Yes   |The signature that is calculated. For more information on the signature calculation method, refer to [Signature Method](https://docs.byteplus.com/en/docs/vpc/Signature-method). |
