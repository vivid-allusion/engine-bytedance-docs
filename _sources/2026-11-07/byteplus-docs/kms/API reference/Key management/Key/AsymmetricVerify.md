---
title: "AsymmetricVerify"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/AsymmetricVerify"
---

You can call the AsymmetricVerify API to verify a signature created using an asymmetric key.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=AsymmetricVerify&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |AsymmetricVerify |The action you want to perform. Set the value to AsymmetricVerify. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |No |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |No |key\-test |The name of the customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyID |String |No |39a0e7c6\-b7dd\-4c83\-b400\-3449bb95403a |The ID of the CMK. Specify either<br><br>KeyringName or KeyName.<br><br>KeyID |
|Message |String |Yes |MessageToBeSigned= |The Base64\-encoded message whose signature you need to verify.<br><br>When MessageType is set to RAW, if the original data you need to sign is specified, the hash algorithm specified by the Algorithm parameter will be used to generate a digest of the original message. Then, the system creates a digital signature for the message digest. Value range:[1, 4096]<br><br>When MessageType is set to DIGEST, the signature can be up to 32 bytes in length. |
|MessageType |String |No |RAW |The type of the message. Valid values:<br><br>RAW (Default): The raw data.<br><br>DIGEST: The message digest of the raw data. Key Management Service (KMS) does not process the data in the message digest of the raw data, but directly creates a digital signature for the message digest using a private key. |
|Algorithm |String |Yes |RSA_PSS_SHA_256 |The algorithm used for creating the signature. Valid enumerated values:<br><br>RSA_PSS_SHA_256<br><br>RSA_PKCS1_SHA_256<br><br>RSA_PSS_SHA_384<br><br>RSA_PKCS1_SHA_384<br><br>RSA_PSS_SHA_512<br><br>RSA_PKCS1_SHA_512<br><br>ECDSA_SHA_256<br><br>ECDSA_SHA_384<br><br>ECDSA_SHA_512<br><br>SM2_DSA<br><br>Note: The signing algorithm must be the same as that used in the AsymmetricSign API.<br><br>The signing algorithm varies depending on the key type. |
|Signature |String |Yes |OuodVCE1zYpDFg1QvgOHtVQxkQWhfpE8i8NibiJ1pL8ILgAE+TogQZuIglAoo= |The Base64\-encoded signature you need to verify. Value range:[1, 6144] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|KeyID |String |39a0e7c6\-b7dd\-4c83\-b400\-3449bb95403a |The unique ID of the CMK. The value is in the UUID format. |
|SignatureValid |Boolean |true |Indicates whether the signature passes verification. Valid values:<br><br>true: The signature passes verification.<br><br>false: The signature fails to pass verification. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=AsymmetricVerify&Version=2021-02-18&KeyringName=demo&KeyName=demo&MessageType=RAW&Algorithm=RSA_PSS_SHA_256 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240708T151941Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Message": "MessageToBeSigned=",
  "Signature": "OuodVCE1zYpDFg1QvgOHtVQxkQWhfpE8i8NibiJ1pL8ILgAE+TogQZuIglAoo="
}
```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202407082320461811522081854EB0A8",
    "Action": "AsymmetricVerify",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "KeyID": "39a0e7c6-b7dd-4c83-b400-3449bb95403a",
    "SignatureValid": "true"
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
