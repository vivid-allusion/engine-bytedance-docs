---
title: "Common request parameters"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Common_request_parameters"
---

This document describes the common request parameters, such as API version and authentication details, that are mandatory for all API calls. Correctly including these parameters is crucial, as their omission will cause requests to fail validation. You should consult this guide when constructing any API request.

This guide explains the structure of common parameters and where to place them, including Action, Version, and signature information. Signature parameters can be included in either the query string or the request header, but Action and Version must be included in the query string.

<span id="667515b6"></span>
## Action and Version


|**Parameter** |**Type** |**Required** |**Description** |**Example value** |
|---|---|---|---|---|
|Action<br><br> |String |Yes |The name of the API. |`Moderate`<br><br>`Generate` |
|Version<br><br> |String |Yes |The OpenAPI versions provided by the LLM Application Firewall are `2025-08-31` and `2023-12-25` (a legacy version). For more information, see the documentation for the specific interface. |`2025-08-31`<br><br> |


<span id="6b1245c0"></span>
## **Header signature parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Expires |Integer |No |The signature's validity period in seconds. If not specified, the default value is 900. |
|X\-Date<br><br> |String |Yes |The UTC time, with second precision. The format is `YYYYMMDD'T'HHMMSS'Z'`, for example: `20201103T104027Z`. |
|Authorization |String |Yes |`HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`<br><br> <br>&nbsp;<br><br>* AccessKeyId (String): The Access Key ID of the account initiating the request. For example: `AKLTNGU0OGEyMT***`.<br><br>* ShortDate (String): The request date in UTC, formatted to the day. Please use the format: YYYYMMDD, for example: `20230201`.<br><br>* Region (String): The requested region, for example: `cn-beijing`. This region must match the region of the purchased instance. <br><br>* Service (String): The name of the requested service. For the LLM Application Firewall OpenAPI, this value is 'llmshield'.<br><br>* SignedHeaders (String): Headers involved in signing, separated by semicolons.<br><br>* Signature (String): The computed signature. For example: `da4fac562d00f41ad8***`. |
|X\-Security\-Token |String |No |The SessionToken from temporary security credentials issued by the Security Token Service (STS). Omit this parameter when using long\-term keys. |


<span id="356179b6"></span>
## **Query signature parameters**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|X\-Expires |Integer |No |The signature's validity period in seconds. If not specified, the default value is 900. |
|X\-Date |String |Yes |Use UTC time, accurate to the second. The format is YYYYMMDD'T'HHMMSS'Z', for example: 20201103T104027Z. |
|X\-Algorithm |String |Yes |The value must be 'HMAC\-SHA256'. |
|X\-Credential |String |Yes |The credential string, formatted as: {AccessKeyId}/{ShortDate}/{Region}/{Service}/request.<br><br> <br>&nbsp;<br><br>* AccessKeyId (String): The Access Key ID of the account initiating the request.<br><br>* ShortDate (String): The request date in UTC, formatted as YYYYMMDD. For example: 20250201.<br><br>* Region (String): The requested region, for example: cn\-beijing.<br><br>* Service (String): The requested service. |
|X\-SignedHeaders |String |Yes |Headers involved in signing, separated by semicolons. |
|X\-Signature |String |Yes |The computed signature. |
