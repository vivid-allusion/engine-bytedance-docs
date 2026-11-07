---
title: "Common Parameters"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Common-Parameters"
---

Common request parameters are required each time you call a  API to send a request. If any of the common request parameters are not included, the request fails.

The initial letter of every common request parameter is capitalized to distinguish them from API request parameters.

<span id="Action&Version"></span>
## Action&Version

> Action and Version must be included in the query string when you make an API request.



|Parameter Nmae |Type  |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes   |[a\-zA\-Z]+ |Name of an API, indicating the operation to be performed. |
|Version |String |Yes   |YYYY\-MM\-DD |The version number of the API. The current version is 2020\-04\-01. |
|X\-Expires |Int |No  |300 |The validity period of the signature. Unit: seconds. If you do not enter any value, 900 is used by default. |


<span id="签名参数"></span>
## Signature parameters

Signature parameters are required in a request and can be included in Header or Query.

<span id="在Header中的场景"></span>
### Signature parameters in Header


|Parameter Nmae |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes   |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
|Authorization |String |Yes   |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |


Parameters in Authorization:


|Parameter Nmae |Type  |Remark |
|---|---|---|
|AccessKey |String |AccessKey of the request. |
|ShortDate |String |Short date of the request, accurate to the day. UTC time is used. Example: 20180201. |
|Region |String |The Region ID for the request, such as cn\-guangzhou.<br><br>For more information on regions, refer to [Regions and Availability Zones](https://docs.byteplus.com/en/docs/clb/NLB-Regions-and-availability-zones). |
|Service |String |The requested service, when calling the NLB OpenAPI, is: clb. |
|SignedHeaders |String |The Header involved in the signature. Separate multiple Headers with semicolons ( ; ). |
|Signature |String |Calculated signature. For more information on the signature calculation method, refer to [Signature Method](https://docs.byteplus.com/en/docs/clb/NLB-Signature-Method). |


<span id="在Query中的场景"></span>
### Signature parameters in Query

The parameters X\-Date and Authorization can be directly stored in Query.


|Parameter Nmae |Type  |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes   |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
|X\-Algorithm |String |Yes   |Set the value to HMAC\-SHA256. |
|X\-Credential |String |Yes |The credential value in the format of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes   |The headers that are used for the signature. Separate multiple headers semicolons ( ; ). |
|X\-Signature |String |Yes   |Calculated signature. For more information on the signature calculation method, refer to [Signature Method](https://docs.byteplus.com/en/docs/clb/NLB-Signature-Method). |
