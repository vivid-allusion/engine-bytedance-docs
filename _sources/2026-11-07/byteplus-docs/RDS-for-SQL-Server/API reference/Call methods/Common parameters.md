---
title: "Common parameters"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/common-parameters"
---

Public request parameters are required for each interface. Developers need to carry these public request parameters every time they send a request using the Byteplus API, otherwise the request will fail. Common request parameters are capitalized to distinguish interface request parameters.

<span id="actions-and-versions"></span>
## **Actions and Versions**

Action and Version must be in the Query.


|name |type |Is it required? |parameter format |describe |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface, associated with the specific interface, indicates the operation to be performed. |
|Version |String |Yes |YYYY\-MM\-DD |Interface version information, the current version is 2022\-01\-01. |
|X\-Expires |Int |No |300 |The valid time of the signature, in seconds, is 900 seconds by default. |


<span id="signature-parameter"></span>
## **signature parameter**

Signature parameters are an essential part of a request and can be found in a header or query.


* **Scene in Header**



|name |type |Is it required? |describe |
|---|---|---|---|
|X\-Date |String |Yes |20201103T104027Z, using UTC time, accurate to the second. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |


The meaning of the information in Authorization is shown in the following table.


|name |type |Remarks |
|---|---|---|
|AccessKey |String |The requested AK. |
|ShortDate |String |The short time of the request, accurate to the day. Use UTC time, for example: 20220101. |
|Region |String |The requested region, for example: North China 2 (Beijing): cn\-Beijing. |
|ServiceName |String |The requested service, currently rds_mssql. |
|SignedHeaders |String |Headers participating in the signature, separated by semicolons. |
|Signature |String |The calculated signature. For details on how signatures are calculated, see [Signature Mechanisms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/signature-mechanism). |
|X\-TT\-Logid |String |The requested ID and the generation algorithm should be consistent. |



* **Scenes in Query**


X\-Date and Authorization information can be stored directly in Query.


|name |type |Is it required? |describe |
|---|---|---|---|
|X\-Date |String |Yes |20221103T104027Z, using UTC time, accurate to the second. |
|X\-Algorithm |String |Yes |Fixed value, HMAC\-SHA256; for future expansion. |
|X\-Credential |String |Yes |Consists of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Headers participating in the signature, separated by semicolons. |
|X\-Signature |String |Yes |The calculated signature. For details on how signatures are calculated, see [Signature Mechanisms](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/signature-mechanism). |


For more details, see [Public Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
