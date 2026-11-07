---
title: "DisableKeyRotation"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DisableKeyRotation"
---

You can call the DisableKeyRotation API to disable the rotation of a customer master key (CMK).

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DisableKeyRotation&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DisableKeyRotation |The action you want to perform. Set the value to DisableKeyRotation. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |Yes |key\-test |The name of the CMK. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |


<span id="response-parameters"></span>
## Response parameters

No response parameters are specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="request-example"></span>
## Request example

```text
GET /?Action=DisableKeyRotation&Version=2021-02-18&KeyringName=demo&KeyName=demo HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240708T084902Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202407081649110162321720940BC0D6",
    "Action": "DisableKeyRotation",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
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
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|403 |KeyMaterialExpire |Key expire in, %s | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
