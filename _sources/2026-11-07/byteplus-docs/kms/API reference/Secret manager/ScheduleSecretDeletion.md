---
title: "ScheduleSecretDeletion"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/ScheduleSecretDeletion"
---

You can call the ScheduleSecretDeletion API to schedule the deletion of a secret.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=ScheduleSecretDeletion&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ScheduleSecretDeletion |The action you want to perform. Set the value to ScheduleSecretDeletion. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretName |String |Yes |secret\-9527 |The name of the secret. The name must be 2 to 31 characters in length. Valid characters: [a\-zA\-Z0\-9\-_] |
|ForceDelete |Boolean |No |false |Specifies whether to force delete the secret immediately. |
|PendingWindowInDays |Integer |No |7 |The number of days after which the secret will be deleted. Within this time period, you can cancel the scheduled deletion of the secret in the PendingDelete state. After this time period, the scheduled deletion cannot be canceled. Value range: 7 to 30. Unit: days. Default value: 7. |


<span id="response-parameters"></span>
## Response parameters

No response parameters are specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="request-example"></span>
## Request example

```text
GET /?Action=ScheduleSecretDeletion&Version=2021-02-18&SecretName=secret-9527&ForceDelete=false&PendingWindowInDays=7 HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240808T080534Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240808/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20240808160557217199219074153C9E",
    "Action": "ScheduleSecretDeletion",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {}
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
