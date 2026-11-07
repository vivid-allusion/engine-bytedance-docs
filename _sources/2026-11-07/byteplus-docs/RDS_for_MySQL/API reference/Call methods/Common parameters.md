---
title: "Common parameters"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/common_parameters_1"
---

Common request parameters are the request parameters that each interface needs to use. Each time developers use the BytePlus API to send a request, they need to carry these common request parameters. Otherwise, the request will fail. The first letters of common request parameters are all capitalized to distinguish them from interface request parameters.

<span id=".YWN0aW9uLeWSjC12ZXJzaW9u"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be in the Query.</div>



|Name |Type |Is it required? |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface, which is related to the specific interface, indicates the action to be executed. |
|Version |String |Yes |YYYY\-MM\-DD |The interface version information. The current version is 2022\-01\-01. |
|X\-Expires |Int |No |300 |The valid time of the signature in seconds, default is 900 seconds if not specified. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are an essential part of the request and can be in the Header or Query.


* **Scenarios in Header**

   
   |Name |Type |Is it required? |Description |
   |---|---|---|---|
   |X\-Date |String |Yes |20201103T104027Z, at UTC time, accurate to the second. |
   |Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |
   

   The following table shows the meaning of the information in Authorization.

   
   |Name |Type |Remarks |
   |---|---|---|
   |AccessKey |String |The requested AK. |
   |ShortDate |String |The short time of the request, accurate to the day. Use UTC time, for example: 20180101. |
   |Region |String |The requested region, for example, China (Beijing): cn\-beijing. |
   |ServiceName |String |Requested service, currently rds_mysql. |
   |SignedHeaders |String |Headers participating in the signature, separated by semicolons. |
   |Signature |String |The calculated signature. For details about signature calculation, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/RDS_for_MySQL/signature_mechanism_1). |
   |X\-TT\-Logid |String |The ID of the request. Keep the algorithm generation consistent. |
   

* **Scenarios in Query**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The information of X\-Date and Authorization can directly exist in the Query.   </div>
   

   
   |Name |Type |Is it required? |Description |
   |---|---|---|---|
   |X\-Date |String |Yes |20181103T104027Z. It uses UTC time and is accurate to the second. |
   |X\-Algorithm |String |Yes |Fixed value, HMAC\-SHA256; reserved for future expansion. |
   |X\-Credential |String |Yes |Consists of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
   |X\-SignedHeaders |String |Yes |Headers participating in the signature, separated by semicolons. |
   |X\-Signature |String |Yes |The calculated signature. For details about signature calculation, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/RDS_for_MySQL/signature_mechanism_1). |
   


For more details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
