---
title: "DescribeKeys"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeKeys"
---

You can call the DescribeKeys API to query customer master keys (CMKs).

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeKeys&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeKeys |The action you want to perform. Set the value to DescribeKeys. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|CurrentPage |Integer |No |1 |The number of pages to return in the pagination query. The value must be greater than or equal to 1. |
|PageSize |Integer |No |20 |The number of entries to return on each page in the pagination query. Value range:[1, 100] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|PageInfo |Object |The data in the PageInfo structure |The information about the returned page. |
|Keys |Array of Object |The data in all the Key structures |The information about the CMKs. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=DescribeKeys&Version=2021-02-18&KeyringName=demo&CurrentPage=1&PageSize=5 HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240707T153816Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240707/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202407072338460550250711642E5896",
    "Action": "DescribeKeys",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageInfo": {
      "TotalCount": 1,
      "PageSize": 5,
      "CurrentPage": 1,
      "Count": 1
    },
    "Keys": [
      {
        "ID": "d24a9f14-1a8b-4393-b66e-b77b766b5735",
        "CreationDate": 1625818017,
        "UpdateDate": 1625818017591,
        "KeyName": "demo",
        "KeySpec": "SYMMETRIC_256",
        "Description": "demo",
        "KeyState": "Enable",
        "KeyUsage": "ENCRYPT_DECRYPT",
        "ProtectionLevel": "SOFTWARE"
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
