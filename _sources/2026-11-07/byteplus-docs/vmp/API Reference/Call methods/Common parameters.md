---
title: "Common parameters"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Common-parameters"
---

Common request parameters are required for each API. Each time you send a request to a BytePlus OpenAPI, you must include these common request parameters. Otherwise, the request fails. The first letter of each common request parameter must be capitalized to distinguish these parameters from other request parameters.

<span id=".QWN0aW9uIOWSjCBWZXJzaW9u"></span>
## Actions and Versions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be placed in the query.</div>



|Name |Type |Is it required? |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |Name of the API. |
|Version |String |Yes |YYYY\-MM\-DD |Version of the API. |
|X\-Expires |Int |No |300 |The signature lifetime in seconds. Leaving it empty indicates a default lifetime of 900 seconds. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Signature parameters are required in requests and need to be placed in headers or queries.</div>


<span id=".5ZyoSGVhZGVy5Lit55qE5Zy65pmv"></span>
### Signature parameters in headers


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |It is time in UTC precise to the second. It follows ISO 8601 standard: `YYYYMMDD'T'HHMMSS'Z'`, e.g., `20201103T104027Z`. |
|Authorization |String |Yes |It is used to verify the validity of requests. The format is: `HMAC-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |


Details in Authorization:


|Name |Type |Note |
|---|---|---|
|AccessKey |String |Access key ID. |
|ShortDate |String |Date of the request, which is precise to the day. It is time in UTC, e.g., `20180201`. |
|Region |String |The region to which requests are sent, e.g., `cn-beijing` is used to represent the region North China 2 (Beijing).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about regions, see <a href="https://docs.byteplus.com/en/docs/vmp/Regions-and-availability-zones">Server\-launching region</a>.</div><br> |
|Service |String |The service to be requested, e.g., `vmp` represents VMP service. |
|SignedHeaders |String |Headers involved in signing with semicolons (;) as separators. |
|Signature |String |Calculated signature. A signature that is ready to use. See [Signature Method](https://docs.byteplus.com/en/docs/vmp/Signature-mechanism) for details. |


<span id=".5ZyoIFF1ZXJ5IOS4reeahOWcuuaZrw=="></span>
### X\-Date and Authorization can be placed directly in the query.


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |It is time in UTC precise to the second, e.g., `20201103T104027Z`. |
|X\-Algorithm |String |Yes |The value is always HMAC\-SHA256, which is reserved for future extensions. |
|X\-Credential |String |Yes |It is composed of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. You can find the details about the fields in the previous table. |
|X\-SignedHeaders |String |Yes |Headers involved in signing with semicolons (;) as separators. |
|X\-Signature |String |Yes |A signature that is ready to use. See [Signature Method](https://docs.byteplus.com/en/docs/vmp/Signature-mechanism) for details. |
