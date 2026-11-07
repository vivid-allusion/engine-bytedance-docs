---
title: "BatchGetSecretValue"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/BatchGetSecretValue"
---

You can call the BatchGetSecretValue API to batch obtain secret values.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=BatchGetSecretValue&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |BatchGetSecretValue |The action you want to perform. Set the value to BatchGetSecretValue. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretNames |Array of String |Yes |["secret\-9527"] |A list of secret names. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|SecretValues |Array of Object |[<br><br>{<br><br>"SecretName": "secret\-9527",<br><br>"VersionID": "b58a7e97\-3000\-4e6e\-90c4\-c01958333717",<br><br>"VersionStage": "CURRENT",<br><br>"CreationDate": 1723284049,<br><br>"SecretValue": "{"username":"root","password":"123456"}"<br><br>}<br><br>] |A list of obtained secret values. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=BatchGetSecretValue&Version=2021-02-18 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240810T122536Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240810/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "SecretNames": [
    "secret-9527"
  ]
}
```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "202408102026552280000251394C743F",
    "Action": "BatchGetSecretValue",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "SecretValues": [
      {
        "SecretName": "secret-9527",
        "VersionID": "b58a7e97-3000-4e6e-90c4-c01958333717",
        "VersionStage": "CURRENT",
        "CreationDate": 1723284049,
        "SecretValue": "{\"username\":\"root\",\"password\":\"123456\"}"
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |The request parameter %s is invalid. | |
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|403 |AccessDenied |User is not authorized to do this action | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
