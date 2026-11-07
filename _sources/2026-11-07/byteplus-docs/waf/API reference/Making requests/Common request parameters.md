---
title: "Common request parameters"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/common_request_parameters"
---

This article describes the common parameters that must be passed when calling an API. Common parameters generally include OpenAPI version and authentication information. These parameters will not be repeatedly described in the specific API interface documentation, please carry these parameters when requesting the API, otherwise, the request will not pass the legitimacy verification.

Signature parameters can be in the Query or in the Header, but Action and Version must be in the Query.

<span id="667515b6"></span>
## Action and Version


|**Parameter** |**Data type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CreateBlockRule` |The name of the interface. Consistent with the actual business interface name. |
|Version |String |is |`2023-12-25` |The version of the interface. Web Application Firewall provides OpenAPI versions `2022-12-09` and `2023-12-2`5. For details, please refer to the specific documentation. |


<span id="6b1245c0"></span>
## **Header Signature Parameters**


|**Parameter** |**Data type** |**Required** |**Description** |
|---|---|---|---|
|X\-Expires |Integer |No |The duration of the signature's validity in seconds, defaults to 900 if not specified. |
|X\-Date |String |Yes |Use UTC time, accurate to the second. The format is YYYYMMDD'T'HHMMSS'Z', for example: `20231103T104027Z`. |
|Authorization |String |Is |`HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`<br><br>Where:<br><br><br>* AccessKeyId (String): The Access Key ID of the account initiating the request. For example: `AKLTNGU0OGEyMT***`.<br><br>* ShortDate (String): The short date of the request, using UTC time, accurate to the day. Please use the format: YYYYMMDD, for example: `20230201`.<br><br>* Region (String): The region of the request, for example: `byteplus-global`. The requested region should be consistent with the region where the purchased instance is located. Its corresponding relationship can be referred to [Region information](https://docs.byteplus.com/docs/waf/45507#8d79aaa3).<br><br>* Service (String): The service that is requested. The OpenAPI provided by the Web Application Firewall belongs to the product `waf`.<br><br>* SignedHeaders (String): The headers involved in the signature, separated by semicolons.<br><br>* Signature (String): The computed signature. For example: `da4fac562d00f41ad8***`. |
|X\-Security\-Token |String |No |Refers to the SessionToken in the temporary security credentials issued by the Security Token Service (STS), not required when using long\-term keys. |


<span id="356179b6"></span>
## **Query Signature Parameters**


|**Parameter** |**Data type** |**Required** |**Description** |
|---|---|---|---|
|X\-Expires |Integer |No |The valid time of the signature, in seconds. If not specified, the default value is 900. |
|X\-Date |String |Yes |Using UTC time, accurate to the second. The format is YYYYMMDD'T'HHMMSS'Z', for example: 20201103T104027Z. |
|X\-Algorithm |String |Yes |Fixed value: HMAC\-SHA256. |
|X\-Credential |String |Yes |The authentication information is composed of {AccessKeyId}/{ShortDate}/{Region}/{Service}/request.<br><br>Where:<br><br><br>* AccessKeyId (String): The Access Key ID of the account initiating the request.<br><br>* ShortDate (String): The short date of the request, using UTC time, accurate to the day. Please use the format: YYYYMMDD, for example: 20180201.<br><br>* Region (String): The region of the request, for example: cn\-beijing.<br><br>* Service (String): The service of the request. |
|X\-SignedHeaders |String |Yes |Headers that participate in the signing, separated by semicolons. |
|X\-Signature |String |Yes |The calculated signature. |
