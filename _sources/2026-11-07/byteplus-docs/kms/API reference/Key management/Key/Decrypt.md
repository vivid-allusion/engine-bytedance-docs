---
title: "Decrypt"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Decrypt"
---

You can call the Decrypt API to decrypt data using a symmetric key.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=Decrypt&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |Decrypt |The action you want to perform. Set the value to Decrypt. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|EncryptionContext |String |No | |The JSON string of the key/value. If this parameter is specified during the encryption, send an identical parameter when you call the Decrypt API. |
|CiphertextBlob |String |Yes |aaSgNwtCRlebbNLMueEN2gAA/Ijt5mhv0QfCLLKxpiF/QfSsTr2Yh8j7X/BWJ6JzhqmTGGXSRBf8RIzZiqZpuZ3ilC389YOnHoLahR5PjcEroYCEcbVxf7k+y8wVBE/O1XDdGK+5iBTzqy9k0y8= |The data you want to decrypt. The value must be greater than 18. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Plaintext |String |tWB54tTvEu47YjRjuuj+fAt5PskpUaqwsjLeEy4YMNg= |The Base64\-encoded plaintext obtained after the data is decrypted. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=Decrypt&Version=2021-02-18 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240708T073658Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "CiphertextBlob":"aaSgNwtCRlebbNLMueEN2gAA/Ijt5mhv0QfCLLKxpiF/QfSsTr2Yh8j7X/BWJ6JzhqmTGGXSRBf8RIzZiqZpuZ3ilC389YOnHoLahR5PjcEroYCEcbVxf7k+y8wVBE/O1XDdGK+5iBTzqy9k0y8="
}
```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202407081537241800271190259E510F",
    "Action": "Decrypt",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "KeyringName": "demo",
    "KeyName": "demo",
    "Plaintext": "tWB54tTvEu47YjRjuuj+fAt5PskpUaqwsjLeEy4YMNg="
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter |The request parameter %s is invalid. | |
|400 |InvalidKeyStatus |Current key status: %s does not allow to perform this action | |
|403 |Reject.Throttling.CMK |The request of CMK: %s upper limit is exceeded. | |
|403 |AccessDenied |User is not authorized to do this action | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
