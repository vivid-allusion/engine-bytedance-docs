---
title: "GetSecretValue"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/GetSecretValue"
---

You can call the GetSecretValue API to obtain a value of a secret.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=GetSecretValue&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetSecretValue |The action you want to perform. Set the value to GetSecretValue. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretName |String |Yes |secret\-9527 |The name of the secret. The name must be 2 to 31 characters in length. Valid characters: [a\-zA\-Z0\-9\-_] |
|VersionID |String |No |b58a7e97\-3000\-4e6e\-90c4\-c01958333717 |The version ID of the secret value you need to obtain. If you do not specify this parameter, the version with the CURRENT tag is returned by default. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|VersionID |String |b58a7e97\-3000\-4e6e\-90c4\-c01958333717 |The version ID of the secret value you obtained. |
|VersionStage |String |CURRENT |The version tag of the secret value you obtained. |
|CreationDate |Long |1723284049 |The date when the secret version was created. |
|SecretValue |String | |The obtained secret value. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=GetSecretValue&Version=2021-02-18&SecretName=secret-9527 HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240810T113459Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240810/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20240810193520028008060086B0B947",
    "Action": "GetSecretValue",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "VersionID": "b58a7e97-3000-4e6e-90c4-c01958333717",
    "VersionStage": "CURRENT",
    "CreationDate": 1723284049,
    "SecretValue": "{\"username\":\"root\",\"password\":\"123456\"}"
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |The request parameter %s is invalid. | |
|403 |AccessDenied |User is not authorized to do this action | |
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
