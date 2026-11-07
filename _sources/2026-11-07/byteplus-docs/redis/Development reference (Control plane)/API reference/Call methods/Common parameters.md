---
title: "Common parameters"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/common-parameter"
---

Common request parameters are essential parameters required for every API request. Developers must include these parameters in every request sent via the BytePlus API, otherwise the request will fail.

<span id=".YWN0aW9uLeWSjC12ZXJzaW9u"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be in the Query.</div>



|Name |Type |Required? |Format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface, which is related to the specific interface, indicates the action to be executed. |
|Version |String |Yes |YYYY\-MM\-DD |The interface version information. The current version is 2020\-12\-07. |
|X\-Expires |Integer |No |300 |Effective time of the signature, in seconds. If this parameter is not set, it is 900 seconds by default. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are an essential part of the request and can be in the Header or Query.


* **Signature parameters in Header**

   
   |Name |Type |Required? |Description |
   |---|---|---|---|
   |X\-Date |String |Yes |20201103T104027Z, at UTC time, accurate to the second. |
   |Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |
   

   The following table shows the meaning of the information in Authorization.

   
   |Name |Type |Remarks |
   |---|---|---|
   |AccessKey |String |Access key (AK) of the request. |
   |ShortDate |String |The short date of the request, accurate to the day. At UTC time, for example: 20180201. |
   |Region |String |The requested region, for example, China (Beijing): cn\-beijing. |
   |Service |String |The requested service. The current service is Redis. |
   |SignedHeaders |String |Headers participating in the signature, separated by semicolons. |
   |Signature |String |The calculated signature. For details about signature calculation, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/redis/signature-mechanism). |
   

* **Signature parameters in Query**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The X\-Date and Authorization information can be stored in Query.   </div>
   

   
   |Name |Type |Required? |Description |
   |---|---|---|---|
   |X\-Date |String |Yes |20201103T104027Z, at UTC time, accurate to the second. |
   |X\-Algorithm |String |Yes |Fixed to HMAC\-SHA256. |
   |X\-Credential |String |Yes |Consists of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
   |X\-SignedHeaders |String |Yes |Headers participating in the signature, separated by semicolons. |
   |X\-Signature |String |Yes |The calculated signature. For details about signature calculation, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/redis/signature-mechanism). |
   


For more details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
