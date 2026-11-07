---
title: "Common parameters"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/common_parameters"
---

Common request parameters are essential parameters required for every API request. Developers must include these parameters in every request sent via the BytePlus API, otherwise the request will fail. The initial letter of each common request parameter is capitalized to distinguish them from API\-specific request parameters.

<span id="action-and-version"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be included in the Query.</div>



|**Name** |**Type** |**Required** |**Format** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the API, relevant to the specific operation to be executed. |
|Version |String |Yes |YYYY\-MM\-DD |API version information. The version value is 2022\-01\-01 or 2018\-01\-01 depending on the API version in use. |
|X\-Expires |Int |No |300 |Signature validity period, which is accurate to seconds and defaults to 900 seconds if the parameter is left empty. |


<span id="signature-parameters"></span>
## Signature parameters

Signature parameters are required in a request, and can be included in 'Header' or 'Query'.


* **Signature parameters in Header**

   
   |**Name** |**Type** |**Required** |**Description** |
   |---|---|---|---|
   |X\-Date |String |Yes |20201103T104027Z, in UTC time, accurate to seconds. |
   |Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |
   

   Where, the Authorization information is explained in the table below:

   
   |**Name** |**Type** |**Note** |
   |---|---|---|
   |AccessKey |String |Access key (AK) of the request. |
   |ShortDate |String |The short date of the request, accurate to the day. In UTC time, for example: 20220101. |
   |Region |String |Region of the request, for example: Asia Pacific (Johor): ap\-southeast\-1. |
   |ServiceName |String |Requested service, which is rds_postgresql in the current example. |
   |SignedHeaders |String |Headers involved in the signature, separated by semicolons. |
   |Signature |String |Calculated signature. For details on how the signature is calculated, refer to the [Signature mechanism](https://docs.byteplus.com/en/docs/RDS_for_PG/signature_mechanism). |
   |X\-TT\-Logid |String |Request ID. Please use a consistent algorithm. |
   

* **Signature parameters in Query**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The X\-Date and Authorization information can be stored in Query.   </div>
   

   
   |**Name** |**Type** |**Required** |**Description** |
   |---|---|---|---|
   |X\-Date |String |Yes |20221103T104027Z, in UTC time, accurate to seconds. |
   |X\-Algorithm |String |Yes |Value is always set to HMAC\-SHA256. This parameter is reserved for future extensions. |
   |X\-Credential |String |Yes |The value is composed of {AccessKey}, {ShortDate}, {Region}, {Service}, and request. |
   |X\-SignedHeaders |String |Yes |Headers involved in the signature, separated by semicolons. |
   |X\-Signature |String |Yes |Calculated signature.For details on how the signature is calculated, refer to the [Signature mechanism](https://docs.byteplus.com/en/docs/RDS_for_PG/signature_mechanism). |
   


For more details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
