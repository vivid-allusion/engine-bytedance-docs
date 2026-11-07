---
title: "Common Parameters"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Public-parameters"
---

Common request parameters are required each time you call a BytePlus API to send a request. If any of the common request parameters are not included, the request fails.

The initial letter of every common request parameter is capitalized to distinguish them from API request parameters.

## Action&Version

> Action and Version must be included in the query string when you make an API request.

|name |Type |Required |Format |Description |
|---|---|---|---|---|
|Action |String |Yes   |[a\-zA\-Z]+ |Name of an API, indicating the operation to be performed. |
|Version |String |Yes   |YYYY\-MM\-DD |The version number of the API. The current version is 2020\-04\-01. |
|X\-Expires |Int |No  |Integer |The validity period of the signature. Unit: seconds. If you do not enter any value, 900 is used by default. |

## Signature parameters

Signature parameters are required in a request and can be included in Header or Query.

### Signature parameters in Header

|name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes   |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
|Authorization |String |Yes   |HMAC\-SHA256 Credential={AccessKey}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}. |

Parameters in Authorization:

|name |Type |Remark |
|---|---|---|
|AccessKey |String |AccessKey of the request. |
|ShortDate |String |The short time requested, accurate to the day. UTC time is used. Example: 20180201. |
|Region |String |The Region ID for the request, such as cn\-beijing.<br><br>For details about region information, refer to [Regions and availability zones](https://docs.byteplus.com/en/docs/privatelink/Regions-and-Availability-Zones). |
|Service |String |The requested service, when calling the PrivateLink OpenAPI, is privatelink. |
|SignedHeaders |String |Signed headers. Multiple values are separated by semicolons ( ; ). |
|Signature |String |The signature after the calculation is completed. For more information on how the signature is calculated, refer to Signature mechanism. |

### Signature parameters in Query

The parameters X\-Date and Authorization can be directly stored in Query.

|name |Type |Required |Description |
|---|---|---|---|
|X\-Date |String |Yes   |The request timestamp, accurate to the second in UTC time. Example: 20201103T104027Z. |
|X\-Algorithm |String |Yes   |Set the value to HMAC\-SHA256. |
|X\-Credential |String |Yes   |The credential value in the format of {AccessKey}/{ShortDate}/{Region}/{Service}/request. |
|X\-SignedHeaders |String |Yes |Signed headers. Multiple values are separated by semicolons ( ; ). |
|X\-Signature |String |Yes   |The signature after the calculation is completed. For more information on how the signature is calculated, refer to Signature mechanism. |
