---
title: "DescribeKeyrings"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeKeyrings"
---

You can call the DescribeKeyrings API to query keyrings.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeKeyrings&groupName=%E5%AF%86%E9%92%A5%E7%8E%AF%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeKeyrings |The action you want to perform. Set the value to DescribeKeyrings. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|CurrentPage |Integer |No |1 |The number of pages to return in the pagination query. The value must be greater than or equal to 1. |
|PageSize |Integer |No |20 |The number of entries to return on each page in the pagination query. Value range:[1, 100] |
|ProjectName |String |No |default |The name of the project. |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Keyrings |Array of Object |The data in the Keyring structure |The information about the keyring. |
|PageInfo |Object |The data in the PageInfo structure |The information about the returned page. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=DescribeKeyrings&Version=2021-02-18&CurrentPage=1&PageSize=5&ProjectName=demo HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240707T071800Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240707/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240707151839135245227171238D54",
    "Action": "DescribeKeyrings",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageInfo": {
      "TotalCount": 2,
      "PageSize": 5,
      "CurrentPage": 1,
      "Count": 2
    },
    "Keyrings": [
      {
        "ID": "758cb40e-3bf2-4cff-88d5-f898e1d9cf27",
        "CreationDate": 1626748349,
        "UpdateDate": 1626748349045,
        "KeyringName": "demo",
        "KeyringType": "CustomKeyring",
        "Description": "demo keyring for test",
        "UID": "2100000282",
        "TRN": "trn:kms:cn-beijing:2100000282:keyrings/demo"
      },
      {
        "ID": "6859f1b4-9fe0-4237-84a4-e11c6ff4d85a",
        "CreationDate": 1626604238,
        "UpdateDate": 1626604238868,
        "KeyringName": "demo_keyringaaa",
        "KeyringType": "CustomKeyring",
        "Description": "demo keyring for test",
        "UID": "2100000282",
        "TRN": "trn:kms:cn-beijing:2100000282:keyrings/demo_keyringaaa"
      }
    ]
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
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
