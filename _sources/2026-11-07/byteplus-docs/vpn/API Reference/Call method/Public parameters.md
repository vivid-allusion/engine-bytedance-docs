---
title: "Public parameters"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Public-parameters"
---

Common request parameters are those parameters that are required to call any open API. That is, whenever you use an open API of BytePlus to send a request, the request must contain common request parameters. Otherwise, your request fails.

To differentiate between common request parameters and other request parameters. the first letters of common request parameters are capitalized.

<span id="action-version"></span>
## Action&Version

> Action and Version must be placed in Query.



|Name |Type |Required |Format |Description |
|---|---|---|---|---|
|Action |String |Yes |[a\-zA\-Z]+ |The name of the API. It specifies the action that you want to perform, and its value depends on the API. |
|Version |String |Yes |YYYY\-MM\-DD |The version of the API. The current version is 2020\-04\-01. |
|X\-Expires |Integer |No |300 |The validity period of the signature. Unit: seconds. If you do not enter any value, 900 is used by default. |


<span id="signature-parameters"></span>
## Signature parameters

Signature parameters are integral to a request, and can be placed in Header or Query.

<span id="scenarios-of-signature-parameters-in-header"></span>
### Scenarios of signature parameters in Header


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Uses the GMT time that is accurate to the second, such as 20201103T104027Z. |
|Authorization |String |Yes |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |


The following table describes the information contained in Authorization:


|Name |Type |Description |
|---|---|---|
|AccessKey |String |The requested AccessKey. |
|ShortDate |String |The requested short time that is accurate to the day. It uses the GMT time, such as 20180201. |
|Region |String |The requested Region, such as **ap\-southeast\-1**. For more information on Regions, refer to Introduction to [Regions](https://docs.byteplus.com/en/docs/vpn/Regions). |
|Service |String |The requested service. When you call a VPN connection, set its value to vpn. |
|SignedHeaders |String |The header involved in the signature. Separate multiple headers with semicolons ( ; ). |
|Signature |String |The signature after the calculation is completed. For more information on signature calculation methods, refer to [Signature methods](https://docs.byteplus.com/en/docs/vpn/Signature-method). |


<span id="scenarios-of-signature-parameters-in-query"></span>
### Scenarios of signature parameters in Query

The information of X\-Date and Authorization can be directly placed in Query.


|Name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes |Uses the GMT time that is accurate to the second, such as 20201103T104027Z. |
|X\-Algorithm |String |Yes |Uses a fixed value: HMAC\-SHA256 to accommodate future expansions. |
|X\-Credential |String |Yes |Consists of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |The header involved in the signature. Separate multiple headers with semicolons ( ; ). |
|X\-Signature |String |Yes |The signature after the calculation is completed. For more information on signature calculation methods, refer to [Signature methods](https://docs.byteplus.com/en/docs/vpn/Signature-method). |
