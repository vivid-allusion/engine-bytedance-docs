---
title: "Public parameters"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Public_parameters"
---

Public request parameters are required for every API interface. Developers must include these parameters every time they send a request using the BytePlus OpenAPI. Otherwise, the request will fail. The first letters of common request parameters are all capitalized to distinguish them from other request parameters.

<span id=".YWN0aW9uLeWSjC12ZXJzaW9u"></span>
## Action and Version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be placed in the Query.</div>



|Name |Type |Required |Parameter Format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface, specific to the interface being called. |
|Version |String |Yes |YYYY\-MM\-DD |The version information of the interface, specific to the interface being called. |
|X\-Expires |Int |no |300 |The validity period of the signature, in seconds. The default value is 900 seconds if not specified. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The signature parameters are an essential part of the request, which can be placed either in the Header or the Query section of the request.</div>


<span id=".5ZyoaGVhZGVy5Lit55qE5Zy65pmv"></span>
### Scenarios in the header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |The UTC time is used, accurate to the second. Please use the format: `YYYYMMDD'T'HHMMSS'Z'`, e.g., `20201103T104027Z`. |
|Authorization |String |Yes |The credential used to verify the legality of the request. Format: `HMAC-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


The meaning of the information in Authorization


|Name |Type |Description |
|---|---|---|
|AccessKey |String |The Access Key ID of the request. |
|ShortDate |String |The short date of the request, accurate to the day. The UTC time is used, e.g., `20180201`. |
|Region Code |String |The requested Region, such as `cn-beijing`, represents the North China 2 (Beijing) Region.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">CP is a global service and does not differentiate by region. You can enter cn\-beijing, cn\-guangzhou, or cn\-shanghai here.</div><br> |
|Service |String |The requested service when calling the Code Pipeline API is: `cp`. |
|SignedHeaders |String |The headers involved in the signature, separated by semicolons (;). |
|Signature |String |The computed signature. For the signature calculation method, please refer to [Signature mechanism](https://docs.byteplus.com/en/docs/cp/Signature_mechanism). |


<span id=".5ZyoLXF1ZXJ5LeS4reeahOWcuuaZrw=="></span>
### Scenarios in the Query

The information for X\-Date and Authorization can be directly included in the Query.


|Default CPU Request |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |The UTC time is used, accurate to the second, e.g., `20201103T104027Z`. |
|X\-Algorithm |String |Yes |A fixed value of `HMAC-SHA256`; reserved for future expansion |
|X\-Credential |String |Yes |It consists of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |The headers involved in the signature, separated by semicolons (;). |
|X\-Signature |String |Yes |The computed signature. For the signature calculation method, please refer to [Signature mechanism](https://docs.byteplus.com/en/docs/cp/Signature_mechanism). |
