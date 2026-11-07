---
title: "Public parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Common-parameters"
---

Public request parameters are required for every API interface. Developers must include these parameters every time they send a request using the BytePlus OpenAPI. Otherwise, the request will fail. The first letters of common request parameters are all capitalized to distinguish them from other request parameters.

<span id=".YWN0aW9uLeWSjC12ZXJzaW9u"></span>
## Action and Version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be placed in the Query.</div>



|Name |Type |Required |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface, specific to the interface being called. |
|Version |String |Yes |YYYY\-MM\-DD |The version information of the interface, specific to the one being called. |
|X\-Expires |Int |No |300 |The validity period of the signature, in seconds. The default value is 900 seconds if not specified. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The signature parameters are an essential part of the request, which can be placed either in the Header or the Query section of the request.</div>


<span id=".5ZyoaGVhZGVy5Lit55qE5Zy65pmv"></span>
### Scenarios in the Header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |The UTC time is used, accurate to the second. Please use the format: `YYYYMMDD'T'HHMMSS'Z'`, e.g., `20201103T104027Z`. |
|Authorization |String |Yes |The credential used to verify the legality of the request. Format: `HMAC-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |
Meanings of Authorization information


|Name |Type |Description |
|---|---|---|
|AccessKey |String |The Access Key ID of the request. |
|ShortDate |String |The short date of the request, accurate to the day. The UTC time is used, e.g., `20180201`. |
|Region |String |The region of the request, such as `cn-beijing`, which indicates the China (Beijing) region. For more information about regions, see [Regions and availability zones](https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones). |
|Service |String |The requested service. When an API of VKE is called,  the value is set to `vke`. |
|SignedHeaders |String |The headers involved in the signature, separated by semicolons (;). |
|Signature |String |The computed signature. For the signature calculation method, please refer to [Signature mechanism](https://docs.byteplus.com/en/docs/vke/Signature-method). |


<span id=".5ZyoLXF1ZXJ5LeS4reeahOWcuuaZrw=="></span>
### Scenarios in the Query

<span id="b0jEPqOp"></span>
### The information for X\-Date and Authorization can be directly included in the Query.


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Uses UTC time, accurate to the second, e.g., `20201103T104027Z`. |
|X\-Algorithm |String |Yes |The fixed value is `HMAC-SHA256`, which is prepared for future expansion. |
|X\-Credential |String |Yes |It consists of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |The headers involved in the signature, separated by semicolons (;). |
|X\-Signature |String |Yes |The computed signature. For the signature calculation method, please refer to [Signature mechanism](https://docs.byteplus.com/en/docs/vke/Signature-method). |
