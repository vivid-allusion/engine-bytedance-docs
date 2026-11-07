---
title: "DescribeSecret"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeSecret"
---

You can call the DescribeSecret API to query a secret.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeSecret&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeSecret |The action you want to perform. Set the value to DescribeSecret. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretName |String |Yes |secret\-9527 |The name of the secret. The name must be 2 to 31 characters in length. Valid characters: [a\-zA\-Z0\-9\-_] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Secret |Object |{<br><br>"ID": "d24a9f14\-1a8b\-4393\-b66e\-b77b766b6666",<br><br>"CreationDate": 1625818017,<br><br>"UpdateDate": 1625818017591,<br><br>"SecretName": "secret\-9527",<br><br>"UID": "2100000282",<br><br>"Trn": "trn:kms:cn\-beijing:2100000282:secrets/secret\-9527",<br><br>"ProjectName": "default",<br><br>"Description": "test",<br><br>"SecretType": "Generic",<br><br>"Managed": false,<br><br>"ExtendedConfig": "",<br><br>"RotationState": "None",<br><br>"RotationInterval": 0<br><br>} |The information about the queried secret. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=DescribeSecret&Version=2021-02-18&SecretName=secret-9527 HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240808T020044Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240808/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "20240808100105207033003140DB67B3",
    "Action": "DescribeSecret",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Secret": {
      "ID": "d24a9f14-1a8b-4393-b66e-b77b766b6666",
      "CreationDate": 1625818017,
      "UpdateDate": 1625818017591,
      "SecretName": "secret-9527",
      "UID": "2100000282",
      "Trn": "trn:kms:cn-beijing:2100000282:secrets/secret-9527",
      "ProjectName": "default",
      "Description": "test",
      "SecretType": "Generic",
      "Managed": false,
      "ExtendedConfig": "",
      "RotationState": "None",
      "RotationInterval": 0
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
|403 |AccessDenied |User is not authorized to do this action | |
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|404 |Not Found |Not found %s [%s]. | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
