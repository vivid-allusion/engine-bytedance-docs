---
title: "Common parameters"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/common-parameters"
---

Common request parameters refer to the parameters that are required in all API requests, regardless of the action being called. Whenever you send a request using an API, you must include these common request parameters. Otherwise, your request fails. The first letters of common request parameters are all in upper case to distinguish them from other request parameters.

<span id="b0c357c4"></span>
## Action and Version

Action and Version must be included in the query string when you make an API request.


|**Name** |**Type** |**Required** |**Format** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The action that you want to perform. The value specifies the name of the API action. |
|Version |String |Yes |YYYY\-MM\-DD |The version of the API. Value: **2023\-01\-01**. |
|X\-Expires |Int |No |300 |The validity period of the signature. Unit: seconds. If you do not specify this parameter, it is set to 900 seconds by default. |


<span id="0751f0d4"></span>
## Signature parameters

Signature parameters are required for all requests. They can be placed in the header or query string.


* **Signature parameters in the header**

   
   |**Name** |**Type** |**Required** |**Description** |
   |---|---|---|---|
   |X\-Date |String |Yes |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
   |Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |
   

   The following table describes the parameters in Authorization.

   
   |**Name** |**Type** |**Description** |
   |---|---|---|
   |AccessKey |String |The AccessKey ID used for the request. |
   |ShortDate |String |The time when the request is made. The time must be in the YYYYMMDD format and accurate to the day in UTC time. Example: 20180201. |
   |Region |String |The Region ID for the request, such as ap\-southeast\-1. |
   |ServiceName |String |The service to be requested. Set the value to Cloud Search when you call the Cloud Search API. |
   |SignedHeaders |String |The headers that are used to calculate the signature. Separate multiple headers with semicolons ( ; ). |
   |Signature |String |The calculated signature. For more information on how to calculate the signature, refer to [Signature method](https://docs.byteplus.com/en/docs/cloudsearch/signature-method). |
   

* **Signature parameters in the query string**

   The information from X\-Date and Authorization can be directly stored in the query parameters.

   
   |**Name** |**Type** |**Required** |**Description** |
   |---|---|---|---|
   |X\-Date |String |Yes |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
   |X\-Algorithm |String |Yes |The algorithm for signature calculation. Set the value to HMAC\-SHA256. Other algorithms will be supported in the future. |
   |X\-Credential |String |Yes |The credential value in the format of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
   |X\-SignedHeaders |String |Yes |The headers that are used to calculate the signature. Separate multiple headers with semicolons ( ; ). |
   |X\-Signature |String |Yes |The calculated signature. For more information on how to calculate the signature, refer to [Signature method](https://docs.byteplus.com/en/docs/cloudsearch/signature-method). |
