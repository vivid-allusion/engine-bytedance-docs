---
title: "DescribeKey"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeKey"
---

You can call the DescribeKey API to query a customer master key (CMK).

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeKey&groupName=%E5%AF%86%E9%92%A5%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeKey |The action you want to perform. Set the value to DescribeKey. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|KeyringName |String |Yes |keyring\-test |The name of the keyring. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |
|KeyName |String |Yes |key\-test |The name of the CMK. The name must be 2 to 31 characters in length. Valid characters:[a\-zA\-Z0\-9\-_] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Key |Object |The data in the Key structure |The information about the CMK. |


<span id="request-example"></span>
## Request example

```text
GET /?Action=DescribeKey&Version=2021-02-18&KeyringName=demo&KeyName=demo HTTP/1.1
Host: kms.volcengineapi.com
X-Date: 20240708T021200Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240708/cn-beijing/kms/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f


```


<span id="response-example"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240708101218071139091045786C7A",
    "Action": "DescribeKey",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Key": {
      "ID": "0324d9b3-c5d9-4b6f-94e7-884010a16fee",
      "CreationDate": 1642732307,
      "UpdateDate": 1642732307264,
      "KeyName": "demo",
      "KeySpec": "SYMMETRIC_256",
      "Description": "demo",
      "KeyState": "Enable",
      "KeyUsage": "ENCRYPT_DECRYPT",
      "ProtectionLevel": "SOFTWARE",
      "RotationState": "Enable",
      "LastRotationTime": "2022-01-21T10:31:47.264+08:00",
      "ScheduleRotationTime": "2023-01-21T10:31:47.264+08:00",
      "Trn": "trn:kms:cn-beijing:2100056381:keyrings/demo/keys/demo"
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
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
