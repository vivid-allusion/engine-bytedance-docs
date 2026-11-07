---
title: "AsymmetricDecrypt"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/AsymmetricDecrypt"
---

You can call the AsymmetricDecrypt API to decrypt small\-volume data with an asymmetric key.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=AsymmetricDecrypt&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |AsymmetricDecrypt |The action you want to perform. Set the value to AsymmetricDecrypt. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |No |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |No |key\-test |The name of the customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyID |String |No |39a0e7c6\-b7dd\-4c83\-b400\-3449bb95403a |The ID of the CMK. Specify either<br><br>KeyringName or KeyName.<br><br>KeyID |
|CiphertextBlob |String |Yes |43y7grE9TjamX4P7ZOHFbwAAqoNHFtMZ6RNyblKlEhIhrfP6zy034cwJN6MSqFGiDm8oiGqu2Rahs1aKPIcMjaOuodVCE1zYpDFg1QvgOHtVQxkQWhfpE8i8NibiJ1pL8ILgAE+TogQZuIglAoo= |The Base64\-encoded ciphertext that you need to decrypt. Value range:[1, 4096] |
|Algorithm |String |Yes |RSAES_OAEP_SHA_256 |Note: The algorithm must be the same as the encryption algorithm used in the AsymmetricEncrypt API.<br><br>The algorithm used for the decryption. Valid enumerated values:<br><br>RSAES_OAEP_SHA_256<br><br>SM2PKE |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|KeyID |String |39a0e7c6\-b7dd\-4c83\-b400\-3449bb95403a |The unique ID of the CMK. The value is in the UUID format. |
|Plaintext |String |encryptPlaintext= |The Base64\-encoded plaintext obtained after the ciphertext is decrypted. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=AsymmetricDecrypt&Version=2021-02-18&KeyringName=demo&KeyName=demo&Algorithm= RSAES_OAEP_SHA_256 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240708T144018Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "CiphertextBlob": "43y7grE9TjamX4P7ZOHFbwAAqoNHFtMZ6RNyblKlEhIhrfP6zy034cwJN6MSqFGiDm8oiGqu2Rahs1aKPIcMjaOuodVCE1zYpDFg1QvgOHtVQxkQWhfpE8i8NibiJ1pL8ILgAE+TogQZuIglAoo="
}
```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "2024070822411815919311418488C93F",
    "Action": "AsymmetricDecrypt",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "KeyID": "39a0e7c6-b7dd-4c83-b400-3449bb95403a",
    "Plaintext": "encryptPlaintext="
  }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes of the current API related to business logic. For common error codes, refer to [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|HttpCode |Error Code |Error Message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing %s parameter. | |
|400 |InvalidParameter |The request parameter %s is invalid. | |
|400 |InvalidKeyStatus |Current key status: %s does not allow to perform this action | |
|400 |InvalidKeyUsage |Current key usage only allows: %s. Please use different keys for encryption/decryption and signing/verification. | |
|403 |AccessDenied |User is not authorized to do this action | |
|403 |Reject.Throttling.CMK |The request of CMK: %s upper limit is exceeded. | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
