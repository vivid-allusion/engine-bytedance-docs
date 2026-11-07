---
title: "CreateKey"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/CreateKey"
---

You can call the CreateKey API to create a customer master key (CMK).

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=CreateKey&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateKey |The action you want to perform. Set the value to CreateKey. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-test |The name of the keyring.<br><br>The name must be 2 to 31 characters in length.<br><br>Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |Yes |key\-test |The name of the CMK.<br><br>The name must be 2 to 31 characters in length.<br><br>Valid characters:[a\-zA\-Z0\-9\-_] |
|KeySpec |String |No |SYMMETRIC_256 |Valid values for symmetric keys:<br><br>SYMMETRIC_256<br><br>SYMMETRIC_128<br><br>Valid values for asymmetric keys:<br><br>RSA_2048<br><br>RSA_3072<br><br>RSA_4096<br><br>EC_P256<br><br>EC_P256K<br><br>EC_P384<br><br>EC_P521<br><br>EC_SM2 |
|Description |String |No |test |The description of the key.<br><br>The description must be 0 to 8,192 characters in length. |
|KeyUsage |String |No |ENCRYPT_DECRYPT |The usage of the key. Valid values:<br><br>ENCRYPT_DECRYPT<br><br>SIGN_VERIFY |
|ProtectionLevel |String |No |SOFTWARE |The protection level of the key. Valid values:<br><br>SOFTWARE<br><br>HSM |
|RotateState |String |No |Enable |The rotation state of the key. Valid values:<br><br>Enable<br><br>Disable |
|Origin |String |No |CloudKMS |The origin of the key. Valid values:<br><br>CloudKMS<br><br>External |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Key |Object |The data in the Key structure |The information about the CMK. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=CreateKey&Version=2021-02-18&KeyringName=demo&KeyName=demo&KeySpec=SYMMETRIC_256&Description=demo&KeyUsage=ENCRYPT_DECRYPT&ProtectionLevel=SOFTWARE&RotateState=Enable&Origin=CloudKMS HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240707T150834Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240707/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240707231112068082115004555B91",
    "Action": "CreateKey",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Key": {
      "ID": "d24a9f14-1a8b-4393-b66e-b77b766b5735",
      "CreationDate": 1625818017,
      "UpdateDate": 1625818017591,
      "KeyName": "demo",
      "KeySpec": "SYMMETRIC_256",
      "Description": "demo",
      "KeyState": "Enable",
      "KeyUsage": "ENCRYPT_DECRYPT",
      "ProtectionLevel": "SOFTWARE",
      "Origin": "CloudKMS"
    }
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
|409 |Conflict |The %s resource %s is conflict. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
