---
title: "Request structure"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Request_structure"
---

**Service endpoint**


|**Region** |**Domain Name** |
|---|---|
|Asia Pacific(Johor) |kms.ap\-southeast\-1.byteplusapi.com |


**Communication protocols**

All Key Management Service (KMS) APIs communicate through HTTPs, which ensures high security.

**Request methods**


* GET (Recommended)

* POST


Note:


* The common parameters **Action** and **Version** must be placed in the Query String.

* The two request methods cannot be used together. If the GET method is used, all parameters are placed in the Query String. If the POST method is used, the parameters are placed in the Request Body.

* In most cases, the GET method is recommended. When the parameter string is longer than 1,024 bytes, the POST method is recommended.

* When the GET method is used, all request parameters need to be URL\-encoded. When the POST method is used, parameters do not need to be encoded.
