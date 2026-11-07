---
title: "Common parameters"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Common_parameters"
---

Common request parameters are the request parameters that each interface needs to use. Each time developers use the BytePlus API to send a request, they need to carry these common request parameters. Otherwise, the request will fail. Common request parameters start with uppercase letters to distinguish them from interface request parameters.

<span id=".YWN0aW9uLeWSjC12ZXJzaW9u"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be in the Query.</div>



|Parameter name |Type |Is it required? |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The API name relates to the specific interface, indicating the action to execute. |
|Version |String |Yes |YYYY\-MM\-DD |The API version information. The current version is 2025\-10\-01. |
|X\-Expires |Int |No |300 |The valid time of the signature in seconds, default is 900 seconds if not specified. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are an essential part of the request and can be in the Header or Query:


* **Scenario in the Header**

   
   |Parameter name |Type |Is it required? |Description |
   |---|---|---|---|
   |X\-Date |String |Yes |20201103T104027Z, using UTC time, accurate to the second. |
   |Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |
   

   The following table shows the meaning of the information in Authorization.

   
   |Parameter name |Type |Remarks |
   |---|---|---|
   |AccessKey |String |The requested AK. |
   |ShortDate |String |Requested short time, accurate to day. Use UTC time, for example: 20250101. |
   |Region |String |The requested region, for example, China (Beijing): cn\-beijing. |
   |ServiceName |String |Requested service, currently aidap. |
   |SignedHeaders |String |Headers participating in the signature, separated by semicolons. |
   |Signature |String |Calculated signature. For details on the signature calculation method, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/330/Signature_mechanism). |
   |X\-TT\-Logid |String |The ID of the request. Keep the algorithm generation consistent. |
   

* **Scenarios in the Query**

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">X\-Date and Authorization information can be directly in the Query.   </div>
   

   
   |Parameter name |Type |Is it required? |Description |
   |---|---|---|---|
   |X\-Date |String |Yes |20181103T104027Z. It uses UTC time and is accurate to the second. |
   |X\-Algorithm |String |Yes |Fixed value, HMAC\-SHA256; reserved for future expansion. |
   |X\-Credential |String |Yes |composed of `{AccessKey}/{ShortDate}/{Region}/{Service}/request`. |
   |X\-SignedHeaders |String |Yes |Headers participating in the signature, separated by semicolons. |
   |X\-Signature |String |Yes |Calculated signature. For details on the signature calculation method, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/330/Signature_mechanism). |
   


For more details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
