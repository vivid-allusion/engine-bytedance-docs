---
title: "DescribeSecrets"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/DescribeSecrets"
---

You can call the DescribeSecrets API to query secrets.

<span id="debugging"></span>
## Debugging

[去调试](https://api.volcengine.com/api-explorer/?action=DescribeSecrets&groupName=%E5%87%AD%E6%8D%AE%E7%AE%A1%E7%90%86&serviceCode=kms&version=2021-02-18)


<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Name |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DescribeSecrets |The action you want to perform. Set the value to DescribeSecrets. |
|Version |String |Yes |2021\-02\-18 |The version number of the API. The current version is 2021\-02\-18. |
|Filters |String |No |[{"Key":"SecretName","Values":["hello","world"]}] |The filters you can specify to query all the secrets that meet the criteria. This parameter is composed of key/value pairs.<br><br>Key<br><br>Description: The attribute you need to query.<br><br>Type: String.<br><br>Valid values:<br><br>SecretName: The name of the secret.<br><br>Trn: The tenant resource name (TRN) of the secret.<br><br>SecretType: The type of the secret.<br><br>SecretState: The state of the secret.<br><br>ManagedState: Indicates whether the secret is hosted.<br><br>RotationState: The rotation state of the secret.<br><br>Description: The description of the secret.<br><br>CreationDateRange: The date range in which the secret was created.<br><br>UpdateDateRange: The date range in which the secret was updated.<br><br>Values<br><br>Description: The value of the attribute.<br><br>Type: A list of strings.<br><br>Supported number of values:1 to 10.<br><br>Value description:<br><br>When Key is set to SecretName, fuzzy searches are supported and values are case\-insensitive. Example: ["hello","world"].<br><br>When Key is set to Trn, fuzzy searches are supported and values are case\-insensitive. Example: ["kms","secret"].<br><br>When Key is set to SecretType, values are case\-sensitive and valid values include Generic, IAM, RDS, Redis, and ECS. Example: ["ECS","IAM"].<br><br>When Key is set to SecretState, values are case\-sensitive and valid values include Enable, Disable, and PendingDelete. Example: ["Enable","PendingDelete"].<br><br>When Key is set to ManagedState, values are case\-sensitive and valid values include true and false. Example: ["true"].<br><br>When Key is set to RotationState, values are case\-sensitive and valid values include Enable, Disable, and Rotating. Example: ["Enable","Rotating"].<br><br>When Key is set to Description, fuzzy searches are supported and values are case\-insensitive. Example: ["hello","world"].<br><br>When Key is set to CreationDateRange, the start time and the end time must be entered. Example: ["2024\-08\-13 10:00:00","2024\-08\-14 10:00:00"].<br><br>When Key is set to UpdateDateRange, the start time and the end time must be entered. Example: ["2024\-08\-13 10:00:00","2024\-08\-14 10:00:00"].<br><br>Multiple Values of the same Key in the Filters are in an OR relationship. Different Key parameters are in the AND relationship.<br><br>Example: When you enter [{"Key":"SecretName", "Values":["hello","world"]},{"Key":"SecretType", "Values":["ECS"]}], the equivalent syntax is (SecretName=hello OR SecretName=world) AND (SecretType=ECS). |
|ProjectName |String |No |default |The name of the project to which the secret belongs. |
|CurrentPage |Integer |No |1 |The number of pages to return in the pagination query. The value must be greater than or equal to 1. |
|PageSize |Integer |No |20 |The number of entries to return on each page in the pagination query. Value range: [1, 100] |


<span id="response-parameters"></span>
## Response parameters

This table lists only the response parameters specific to this API. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Name |Type |Example Value |Description |
|---|---|---|---|
|Secrets |Array of Object |{<br><br>"ID": "d24a9f14\-1a8b\-4393\-b66e\-b77b766b6666",<br><br>"CreationDate": 1625818017,<br><br>"UpdateDate": 1625818017591,<br><br>"SecretName": "secret\-9527",<br><br>"UID": "2100000282",<br><br>"Trn": "trn:kms:cn\-beijing:2100000282:secrets/secret\-9527",<br><br>"ProjectName": "default",<br><br>"Description": "test",<br><br>"SecretType": "Generic",<br><br>"Managed": false,<br><br>"ExtendedConfig": "",<br><br>"RotationState": "None",<br><br>"RotationInterval": 0<br><br>} |The information about the secret. |
|PageInfo |Object |"PageInfo": {<br><br>"TotalCount": 1,<br><br>"PageSize": 20,<br><br>"CurrentPage": 1,<br><br>"Count": 1<br><br>} |The information about the returned page. |


<span id="request-example"></span>
## Request example

```text
POST /?Action=DescribeSecrets&Version=2021-02-18 HTTP/1.1
Host: kms.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240814T083317Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240814/cn-beijing/kms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Filters": "[{\"Key\":\"SecretName\",\"Values\":[\"secret\",\"9527\"]}]",
  "ProjectName": "default",
  "CurrentPage": 1,
  "PageSize": 20
}
```


<span id="response-example"></span>
## Response example

```text
{
  "ResponseMetadata": {
    "RequestId": "202408080951551860031671271B4C78",
    "Action": "DescribeSecrets",
    "Version": "2021-02-18",
    "Service": "kms",
    "Region": "cn-beijing"
  },
  "Result": {
    "Secrets": [
      {
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
|403 |Reject.Throttling.Action |The request of Action: %s upper limit is exceeded. | |
|403 |AccessDenied |User is not authorized to do this action | |
|500 |UndefinedError |Undefined Internal Error. Pls Contact With Admin. | |
