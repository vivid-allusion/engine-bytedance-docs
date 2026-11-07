---
title: "SetSecretValue"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/SetSecretValue"
---

You can call the SetSecretValue API to store a value of a secret.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=SetSecretValue&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |SetSecretValue |The action you want to perform. Set the value to SetSecretValue. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretName |String |Yes |secret\-9527 |The name of the secret. The name must be 2 to 31 characters in length. Valid characters: [a\-zA\-Z0\-9\-_] |
|SecretValue |String |Yes | |The value of the secret. The value can be up to 30,720 bytes in length. You can define a value as you want. We recommend that you use a key/value pair in JSON format. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|VersionID |String |54487470\-102a\-4f35\-bfb1\-b819e78f7579 |The new version ID of the secret value you stored. |
|VersionStage |String |CURRENT |The new version tag of the secret value you stored. |
|CreationDate |Long |1723104729 |The date when the secret version was created. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=SetSecretValue&Version=2021-02-18 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240811T015427Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240811/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "SecretName": "secret-9527",
  "SecretValue": "{\"username\":\"root\",\"password\":\"123456\"}"
}
```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20240811095501069218106058666D53",
    "Action": "SetSecretValue",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "VersionID": "54487470-102a-4f35-bfb1-b819e78f7579",
    "VersionStage": "CURRENT",
    "CreationDate": 1723104729
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidSecretType |The secret type [%s] does not allow to perform this action. | |
|400 |InvalidParameter |The request parameter %s is invalid. | |
|403 |AccessDenied |User is not authorized to do this action | |
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
