---
title: "Common parameters"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Common_parameters"
---

Common request parameters are the request parameters that each interface needs to use. Each time developers use the BytePlus API to send a request, they need to carry these common request parameters. Otherwise, the request will fail. Common request parameters start with a capital letter to distinguish them from interface request parameters.

<span id=".YWN0aW9uLeWSjC12ZXJzaW9u"></span>
## Action and Version

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Action and Version must be in the Query.</div>



|Name |Type |Required |Parameter format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the interface, which is related to the specific interface, indicates the action to be executed. |
|Version |String |Yes |YYYY\-MM\-DD |The interface version information. The current version is 2022\-01\-01. |
|X\-Expires |Int |No |300 |Effective time of the signature, in seconds. The default value is 900 seconds if this parameter is not set. |


<span id=".562-5ZCN5Y-C5pWw"></span>
## Signature parameters

Signature parameters are an essential part of the request and can be in the Header or Query.

<span id=".5ZyoLWhlYWRlci3kuK3nmoTlnLrmma8="></span>
### Scenarios in Header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |202201013T104027Z, using UTC time, accurate to the second. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |


The following table shows the meaning of the information in Authorization.


|Name |Type |Remarks |
|---|---|---|
|AccessKey |String |Request AK. |
|ShortDate |String |The short time of the request, accurate to the day. Use UTC time, for example, 20220101. |
|Region |String |The requested region, for example, cn\-beijing. |
|Service |String |The requested service. The current service is vedbm. |
|SignedHeaders |String |Headers participating in the signature, separated by semicolons. |
|Signature |String |The calculated signature. For details about signature calculation, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Signature_mechanism). |
|X\-TT\-Logid |String |The ID of the request. Keep the algorithm generation consistent. |


<span id=".5ZyoLXF1ZXJ5LeS4reeahOWcuuaZrw=="></span>
### Scenarios in Query

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The information of X\-Date and Authorization can directly exist in the Query.</div>



|Parameter name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |20220101T104027Z, using UTC time, accurate to the second. |
|X\-Algorithm |String |Yes |Fixed value, HMAC\-SHA256. Prepare for future expansion. |
|X\-Credential |String |Yes |Consists of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Headers participating in the signature, separated by semicolons. |
|X\-Signature |String |Yes |The calculated signature. For more information about the signature calculation method, refer to [Signature mechanism](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Signature_mechanism). |


For more details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).
