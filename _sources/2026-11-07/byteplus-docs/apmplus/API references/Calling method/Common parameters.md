---
title: "Common parameters"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Public_parameters"
---

Common request parameters are required for every API. You need to include them in each request. Otherwise, the request will fail. Common request parameters start with uppercase letters to distinguish them from other API parameters.

<span id="85fbe1f4"></span>
## Action and Version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Action and Version must be placed in the query.</div>



|**Name** |**Type** |**Required** |**Parameter format** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |This is the API name, which relates to a specific interface and indicates the operation to perform. |
|Version |String |Yes |YYYY\-MM\-DD |This is the API version information. The current version is 2022\-10\-12. |
|X\-Expires |Int |No |300 |The signature validity period is in seconds. The default is 900 if not specified. |
|x\-app\-ids |int |Yes |12345 |Application ID. |


<span id="ddfe9535"></span>
## Header


|**Name** |**Type** |**Required** |**Parameter format** |**Description** |
|---|---|---|---|---|
|x\-app\-ids |int |Yes |12345 |Application ID. |


<span id="719eeaa7"></span>
## Signature parameters

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Signature parameters are required in requests and need to be placed in headers or queries.</div>


<span id="002914e1"></span>
### Signature parameters in headers


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |Time in UTC. It is accurate to the second. Use the format `YYYYMMDD'T'HHMMSS'Z'`. For example, `20201103T104027Z`. |
|Authorization |String |Yes |```json```<br>```HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}```<br> |
|X\-Security\-Token |String |No |This is the SessionToken in temporary security credentials issued by STS. It is not required when using long\-term keys. |


The fields in Authorization are explained as follows:


|**Name** |**Type** |**Note** |
|---|---|---|
|AccessKey |String |This is the AccessKey for the request. |
|ShortDate |String |The short time string for requests in UTC. It is accurate to the day. Use the format `YYYYMMDD`. For example, `20180201`. |
|Region |String |Requested region, for example, `cn-beijing`. |
|ServiceName |String |Requested service.<br><br><br>* apmplus_server: Call the APMPlus API<br><br>* apmplus_openapi: Call other APIs |
|SignedHeaders |String |Headers involved in signature calculation, separated by semicolons. |
|Signature |String |This is a ready\-to\-use signature. See the Signature mechanism for how it is calculated. |
|X\-TT\-Logid |String |Request ID. Ensure the same generation algorithm is used. |


<span id="59bbd63b"></span>
### Signature parameters in Query


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |Time in UTC. It is accurate to the second. For example, `20201103T104027Z`. |
|X\-Algorithm |String |Yes |This value is currently fixed as: `HMAC-SHA256`. |
|X\-Credential |String |Yes |It consists of `{AccessKeyId}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |Headers involved in signature calculation, separated by semicolons. |
|X\-Signature |String |Yes |This is a ready\-to\-use signature. See the [Signature mechanism](https://docs.byteplus.com/en/docs/apmplus/Signature_methods) for how it is calculated. |
