---
title: "DescribeSecretVersions"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeSecretVersions"
---

You can call the DescribeSecretVersions API to query secret versions.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeSecretVersions&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeSecretVersions |The action you want to perform. Set the value to DescribeSecretVersions. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|SecretName |String |Yes |secret\-9527 |The name of the secret. The name must be 2 to 31 characters in length. Valid characters: [a\-zA\-Z0\-9\-_] |
|CurrentPage |Integer |No |1 |The number of pages to return in the pagination query. The value must be greater than or equal to 1. |
|PageSize |Integer |No |20 |The number of entries to return on each page in the pagination query. Value range: [1, 100] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|SecretVersions |Array of Object |[<br><br>{<br><br>"VersionID": "54487470\-102a\-4f35\-bfb1\-b819e78f7579",<br><br>"VersionStage": "CURRENT",<br><br>"CreationDate": 1723104729<br><br>}<br><br>] |The information about the secret versions. |
|PageInfo |Object |{<br><br>"TotalCount": 1,<br><br>"PageSize": 20,<br><br>"CurrentPage": 1,<br><br>"Count": 1<br><br>} |The information about the returned page. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=DescribeSecretVersions&Version=2021-02-18&SecretName=secret-9527&CurrentPage=1&PageSize=20 HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240811T024400Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240811/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "2024081110441815424409905636A85B",
    "Action": "DescribeSecretVersions",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "SecretVersions": [
      {
        "VersionID": "54487470-102a-4f35-bfb1-b819e78f7579",
        "VersionStage": "CURRENT",
        "CreationDate": 1723104729
      }
    ],
    "PageInfo": {
      "TotalCount": 1,
      "PageSize": 20,
      "CurrentPage": 1,
      "Count": 1
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
