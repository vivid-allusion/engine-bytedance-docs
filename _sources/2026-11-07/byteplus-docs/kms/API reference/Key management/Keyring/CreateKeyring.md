---
title: "CreateKeyring"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/CreateKeyring"
---

You can call the CreateKeyring API to create a keyring.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=CreateKeyring&groupName=%E5%AF%86%E9%92%A5%E7%8E%AF%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |CreateKeyring |The action you want to perform. Set the value to CreateKeyring. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyringType |String |No |key\-test |The type of the keyring. Set the value toCustomKeyring |
|Description |String |No |test |The description of the keyring. The description must be 0 to 8,192 characters in length. |
|ProjectName |String |No |default |The name of the project. Default value:default |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Keyring |Object |The data in the Keyring structure |The information about the keyring. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=CreateKeyring&Version=2021-02-18&KeyringName=demo&KeyringType=CustomKeyring&Description=demo&ProjectName=demo HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240707T065739Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240707/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202407071459222300901380488B8EAE",
    "Action": "CreateKeyring",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Keyring": {
      "ID": "758cb40e-3bf2-4cff-88d5-f898e1d9cf27",
      "CreationDate": 1626748349045,
      "UpdateDate": 1626748349045,
      "KeyringName": "demo",
      "KeyringType": "CustomKeyring",
      "Description": "demo",
      "UID": "2100000282",
      "TRN": "trn:kms:cn-beijing:2100000282:keyrings/demo"
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
