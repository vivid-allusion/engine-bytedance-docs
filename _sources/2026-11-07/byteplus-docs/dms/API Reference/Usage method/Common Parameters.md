---
title: "Common Parameters"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/Common_Parameters"
---

Public request parameters must be included in every interface request. Developers need to provide these parameters when using BytePlus API; otherwise, the request will fail. All public request parameters start with a capital letter to distinguish API request parameters.

<span id="5a3a2cdc"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be included in the Query.</div>



|**Name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateDataMigrateTask |Interface name, indicates the operation to perform. List of supported operations for file storage; see [API Overview](https://docs.byteplus.com/docs/dms/API_Overview). |
|Version |String |Yes |2018\-01\-01 |API version information. The current version is `2018-01-01`. |
|X\-Expires |Int |No |300 |Signature validity period in seconds. Default is 900 if not specified. |


<span id="8865b525"></span>
## Signature parameters

Signature parameters are required in requests and can be included in the Header or Query.

<span id="9342668a"></span>
### Scenario for including in the Header


|**Name** |**Type** |**Required** |**Description** |**Example value** |
|---|---|---|---|---|
|X\-Date |String |Yes |Use UTC time, accurate to seconds, and formatted using the ISO 8601 standard: `YYYYMMDD'T'HHMMSS'Z'`. |20201103T104027Z |
|Authorization |String |Yes |HTTP standard authentication header field. The format is `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. |HMAC\-SHA256 Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZkYzE/20201230/cn\-north\-1/iam/request, SignedHeaders=content\-type;host;x\-content\-sha256;x\-date, Signature=28eeabbbd726b87002e0fe58ad8c1c768e619b06e2646f35b6ad7ed029a6d8a7 |


The meaning of information in Authorization is detailed in the table below.


|**Name** |**Type** |**Remarks** |
|---|---|---|
|AccessKey |String |Requested AccessKey information. For instructions on how to view the AK and SK, see [Viewing the Access Key ID and Secret Access Key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-keys). |
|ShortDate |String |Short request date, accurate to day. Use UTC time, for example: 20180201. |
|Region |String |Requested region, for example: North China 2 (Beijing): cn\-beijing. |
|ServiceName |String |The requested service is currently `dms`. |
|SignedHeaders |String |Headers involved in signing, separated by semicolons if there are multiple headers. |
|Signature |String |Signature after calculation. For details about signature calculation, see [Signature Mechanism](https://docs.byteplus.com/docs/dms/Signature_Mechanism). |


<span id="0c891a40"></span>
### Scenario in Query


|**Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Date |String |Yes |20201103T104027Z, use UTC time, accurate to the second. |
|X\-Algorithm |String |Yes |Fixed value: HMAC\-SHA256; reserved for future extensions. |
|X\-Credential |String |Yes |Composed of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
|X\-SignedHeaders |String |Yes |Headers participating in the signature are separated by semicolons. |
|X\-Signature |String |Yes |Calculated signature. For details on how the signature is calculated, see [Signature Mechanism](https://docs.byteplus.com/docs/dms/Signature_Mechanism). |
