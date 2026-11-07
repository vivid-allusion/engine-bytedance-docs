---
title: "Common parameters"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-parameters"
---

To simplify your integration with BytePlus Live APIs, this document provides a centralized reference for all shared request and response parameters. You can refer to this guide to understand the common parameters required for every API call.

<span id="common-request-parameters"></span>
## Common request parameters

The following are the common request parameters.


|Parameter Name |Data Type |Required |Location |Description |Example |
|---|---|---|---|---|---|
|Host |String |Yes |Header |Endpoint. Set the value to `livesaas.byteplusapi.com`. |livesaas.byteplusapi.com |
|Content\-Type |String |Yes |Header |A Multipurpose Internet Mail Extensions (MIME) resource type. Set the value to `application/x-www-form-urlencoded; charset=utf-8`. |application/x\-www\-form\-urlencoded; charset=utf\-8 |
|X\-Content\-Sha256 |String |Yes |Header |A string created using the payload in the body of the HTTP or HTTPS request as the input to a hash function. This string uses lowercase hexadecimal characters. If the payload is empty, use an empty string as the input to the hash function. This parameter is used for signature purposes. For more information, see [API authentication](https://docs.byteplus.com/docs/byteplus-livesaas/docs-API-authentication). |e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855 |
|X\-Date |String |Yes |Header |UTC time when the API request is sent.<br><br>Unit: seconds.<br><br>Format: `YYYYMMDD'T'HHMMSS'Z'` |20201230T081805Z |
|X\-Security\-Token |String |No |Header |Temporary session token issued by the Security Token Service (STS). Not required when using a long\-term access key. |STSeyJBY2NvdW50SW\*\*klkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MzAyMTcsIkNoYW5uZWwiOiJyZXNvdXJjZSIsIkFjY2Vzc0tleUlkIjoiQUtUUE9EZzBNelZrWlRNMVlqQXlOR05sWkdGbU0yVTNaVEl6T0RnMlpEY3hNRGciLCJTaWduZWRTZWNyZXRBY2Nlc3NLZXkiOiJHSHRuc2Q1b3BOOThUeUNrckVuMVAxTDd1ZzBXczZFMytzTktDMDJQT01lNzFMOUloNzhYaDB5VXE4Ni9JMW8reEZxTmtkK01tVUR0cjRHR0NodXJQdz09IiwiRXhwaXJlZFRpbWUiOjE2MTgxOTk4MjksIlBvbGljeVN0cmluZyI6IiIsIlNpZ25hdHVyZSI6IjdiZTEzNTU1MDM5NzcyM2VkMDQxYmVkNTIyNzU4YmMyNjQ3YzRmNzZiNmRjYTViNzVhZDUyOTMwYTg1NjE5ZGEiLCJTZXNzaW9uTmFtZSI6ImNlc2hpYXNzdW1lIn0= |
|[Authorization](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters) |String |Yes |Header |Format: `HMAC-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature={Signature}`. For more information, see [API authentication](https://docs.byteplus.com/docs/byteplus-livesaas/docs-API-authentication). |HMAC\-SHA256 Credential=AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA\*\*\*\*/20201230/ap\-singapore\-1/livesaas/request, SignedHeaders=content\-type;host;x\-content\-sha256;x\-date, Signature=11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a |
|Action |String |Yes |Query string |API operation. |CreateActivityAPIV2 |
|Version |String |Yes |Query string |Version of the API operation. Current version: `2020-06-01`. |2020\-06\-01 |
|X\-Expires |Integer |No |Header |The validity period of the signature. Unit: seconds. Default value: `900`. |900 |


<span id="authorization"></span>
### Authorization


|Parameter Name |Data Type |Description |Example |
|---|---|---|---|
|AccessKeyId |String |Your AccessKey ID for API request authentication. |AKAPY2RhYmQzODhhYTg4NGZmNTk3ZGUxODk3ODgzYTA\*\*\*\* |
|ShortDate |String |UTC time when the API request is sent. Unit: days. Format: `YYYYMMDD`.<br><br>The value must be the same as that of `YYYYMMDD` in `X-Date`. |20201230 |
|Region |String |Region of the API request. The value must be `ap-singapore-1`. |ap\-singapore\-1 |
|Service |String |Service name of the API request. For BytePlus Live, the value must be `livesaas`. |livesaas |
|SignedHeaders |String |A semicolon\-separated list of request headers to include in the signature. This process ensures that any extra headers added by a proxy are ignored during verification. If the `host` and `x-date` headers are present in the request, they must be included in this list. |content\-type;host;x\-content\-sha256;x\-date |
|Signature |String |The calculated signature. |11a2e7bb9db7ee7ea2e4d7f3d6989a65dc3bb5feedf3aae50ba1b3313fe0093a |


<span id="common-response-parameters"></span>
## Common response parameters

The following are the common response parameters.


|Parameter Name |Data Type |Description |Example |
|---|---|---|---|
|RequestId |String |Unique ID of the API request. |202201201826170101501312091D1C09D2 |
|Action |String |Name of the requested API operation. |CreateActivityAPIV2 |
|Version |String |Version of the requested API operation. Current version: `2020-06-01`. |2020\-06\-01 |
|Service |String |Name of the requested API service. For BytePlus Live, this value is `livesaas`. |livesaas |
|Region |String |Region of the requested API service. This value is `ap-singapore-1`. |ap\-singapore\-1 |
|SystemTime |Integer |The system time when the API operation was called in Unix timestamp format. Unit: seconds. |1656067132 |
