---
title: "GetPublicKey"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/GetPublicKey"
---

You can call the GetPublicKey API to obtain the public key of a specified asymmetric key.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=GetPublicKey&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetPublicKey |The action you want to perform. Set the value to GetPublicKey. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |No |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |No |key\-test |The name of the customer master key (CMK). The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyID |String |No |39a0e7c6\-b7dd\-4c83\-b400\-3449bb95403a |The ID of the CMK. Specify either<br><br>KeyringName or KeyName.<br><br>KeyID |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|KeyID |String |39a0e7c6\-b7dd\-4c83\-b400\-3449bb95403a |The unique ID of the CMK. The value is in the UUID format. |
|PublicKey |String |MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEy1ywbEU17uqak8PNqv54BDdtE7+n CGXuj8nKmhPNl3AmN8z2roAowQYORs4JTTfmmLq0jvIU0hBCsSS3aY== |The public key in the PEM format.<br><br>\-\-\-\-\-BEGIN PUBLIC KEY\-\-\-\-\- MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEy1ywbEU17uqak8PNqv54BDdtE7+n CGXuj8nKmhPNl3AmN8z2roAowQYORs4JTTfmmLq0jvIU0hBCsSS3aY\*\*\*\*== \-\-\-\-\-END PUBLIC KEY\-\-\-\-\- |


<span id="request-example"></span>
## Request example

```text
GET /?Action=GetPublicKey&Version=2021-02-18&KeyringName=demo&KeyName=demo HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240709T013058Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240709/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240709093134130030112119297E09",
    "Action": "GetPublicKey",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "KeyID": "39a0e7c6-b7dd-4c83-b400-3449bb95403a",
    "PublicKey": "MFkwEwYHKoZIzj0CAQYIKoEcz1UBgi0DQgAEy1ywbEU17uqak8PNqv54BDdtE7+n CGXuj8nKmhPNl3AmN8z2roAowQYORs4JTTfmmLq0jvIU0hBCsSS3aY==",
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
|403 |AccessDenied |User is not authorized to do this action | |
|403 |Reject.Throttling.CMK |The request of CMK: %s upper limit is exceeded. | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
