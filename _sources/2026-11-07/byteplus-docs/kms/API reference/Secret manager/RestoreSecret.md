---
title: "RestoreSecret"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/RestoreSecret"
---

You can call the RestoreSecret API to restore a secret.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=RestoreSecret&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |RestoreSecret |The action you want to perform. Set the value to RestoreSecret. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretDataKey |String |Yes |C3UuDNBwR8eGeh4MpKp0bQAAY/IF0N+VFVlzDdbuKAaWYN8KxwbN9cqKB9d34lbeKFKPRGia9Egv/6PASfbgua7IG+ilsUOGkCTsqmvYcwGo/9prXDEutiThS6GOo/eenGpCzHYLV/p5TgeuzNc= |The Base64\-encoded data key ciphertext returned when the secret was backed up. |
|BackupData |String |Yes |{} |The full data of the secret in JSON format returned when the secret was backed up. |
|Signature |String |Yes |GHblfcSOT2aewMP5ZslQnSk6aM1R1WA4HpK8K+N/wGM= |The Base64\-encoded signature of the data you backed up. This value is also the same as that returned when the secret was backed up. |


<span id="response-parameters"></span>
## Response parameters

No response parameters are specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="request-example"></span>
## Request example

```text
POST /?Action=RestoreSecret&Version=2021-02-18 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240811T065828Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240811/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "SecretDataKey": "C3UuDNBwR8eGeh4MpKp0bQAAY/IF0N+VFVlzDdbuKAaWYN8KxwbN9cqKB9d34lbeKFKPRGia9Egv/6PASfbgua7IG+ilsUOGkCTsqmvYcwGo/9prXDEutiThS6GOo/eenGpCzHYLV/p5TgeuzNc=",
  "BackupData": "{}",
  "Signature": "GHblfcSOT2aewMP5ZslQnSk6aM1R1WA4HpK8K+N/wGM="
}
```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "202408111458350352532021348F6125",
    "Action": "RestoreSecret",
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
|409 |ProjectConflict |The secret [%s] already exists in one project. | |
|409 |Conflict |The %s resource %s is conflict. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
