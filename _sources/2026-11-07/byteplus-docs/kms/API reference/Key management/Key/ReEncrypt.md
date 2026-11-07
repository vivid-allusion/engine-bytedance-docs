---
title: "ReEncrypt"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/ReEncrypt"
---

You can call the ReEncrypt API to re\-encrypt data using an asymmetric key.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=ReEncrypt&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ReEncrypt |The action you want to perform. Set the value to ReEncrypt. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|NewKeyringName |String |Yes |keyring\-test1 |The name of the new keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|NewKeyName |String |Yes |key\-test1 |The name of the new customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|OldEncryptionContext |String |No | |The encryption context of the old ciphertext data. |
|NewEncryptionContext |String |No | |The encryption context of the new ciphertext data. |
|CiphertextBlob |String |Yes |858AeEPZQpCdjfXwvXFWeAAAXN1exNPCoOnjug2Lvd1kKX+QTETi3ZkJdwvDMcC7HPFzlRHGrrhzPTeiIz9gumyuP10myXqyUoI3bh+GMW4t |The ciphertext data you need to re\-encrypt. The value must be greater than 18. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|CiphertextBlob |String |3v097jlrRhy9W+ssK8F3EgAAQcr9UmlnESCTDWt5h9Sc63pqck0Vg+xuLp4TNSzsAFVAROVCe2djOVTRyPMmevZ/SbI2VqjSznApk352COmh |The Base64\-encoded ciphertext obtained after the data is re\-encrypted. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=ReEncrypt&Version=2021-02-18&NewKeyringName=demo1&NewKeyName=demo1 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240708T100424Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "CiphertextBlob": "858AeEPZQpCdjfXwvXFWeAAAXN1exNPCoOnjug2Lvd1kKX+QTETi3ZkJdwvDMcC7HPFzlRHGrrhzPTeiIz9gumyuP10myXqyUoI3bh+GMW4t"
}
```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202407081805351152540521739F8055",
    "Action": "ReEncrypt",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "OldKeyringName": "demo",
    "OldKeyName": "demo",
    "CiphertextBlob": "3v097jlrRhy9W+ssK8F3EgAAQcr9UmlnESCTDWt5h9Sc63pqck0Vg+xuLp4TNSzsAFVAROVCe2djOVTRyPMmevZ/SbI2VqjSznApk352COmh"
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
|403 |AccessDenied |User is not authorized to do this action | |
|403 |Reject.Throttling.CMK |The request of CMK: %s upper limit is exceeded. | |
|403 |KeyMaterialExpire |Key expire in, %s | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
