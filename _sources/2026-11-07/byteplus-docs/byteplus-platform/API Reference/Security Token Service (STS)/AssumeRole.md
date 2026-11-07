---
title: "AssumeRole"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-assumerole"
---

Use `AssumeRole` to get a set of temporary security credentials of the account that a role belongs to, then access cloud resources through assuming the role.

When using temporary security credentials to request an API, the `SessionToken` parameter is required as a common parameter for the Header. Click [here](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) for more information about BytePlus common parameters.

The service for this API is `sts` and the service address is **open.byteplusapi.com**.

<span id="1ea0975a"></span>
## Request method

HTTP GET

<span id="fa0e3e84"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |AssumeRole |
|Version |String |Yes |The version of this API, which is `2018-01-01` currently. |
|RoleTrn |String |Yes |The TRN of the to\-be\-assumed role. |
|RoleSessionName |String |Yes |The temporary session name. |
|DurationSeconds |Integer |No |The duration of temporary security credentials. Its valid value ranges from 3,600 to 43,200 (in seconds). |
|Policy |String |No |The inline policy. |


<span id="ca215e8a"></span>
## Sample request

```text
GET /?RoleTrn=trn:iam::200000****:role/ServiceRoleFor**&RoleSessionName=ceshiassume&Action=AssumeRole&Version=2018-01-01 HTTP/1.1
Accept: application/json
Content-Type: application/x-www-form-urlencoded
Host: sts.byteplusapi.com
X-Date: 20180614T131357Z
Authorization: HMAC-SHA256 Credential=AKLT4MQ/20180614/cn-north-1/sts/request, SignedHeaders=accept;content-type;host;x-date, Signature=83671ac2**8a5581f
```


<span id="f6744ebf"></span>
## Response

The response includes the following paramters:


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|Credentials |DataTypes. Credentials |The structure of temporary security credentials. |
|AssumedRoleUser |DataTypes. AssumedRoleUser |The details about temporary security credentials. |


The structure of the `Credentials` parameter is described below:


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|CurrentTime |DateTime |Yes |The time when the temporary security credentials were generated. |
|ExpiredTime |DateTime |Yes |The time when the temporary security credentials expire. |
|AccessKeyId |String |Yes |The AccessKey ID of the temporary security cerdentials. |
|SecretAccessKey |String |Yes |The secret AccessKey of the temporary security credentials. |
|SessionToken |String |Yes |The token required to pass for using the temporary security credentials. |


The structure of the `AssumedRoleUser` parameter is described below:


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Trn |String |Yes |The TRN of the current identity that are returned from the `AssumeRole` action. |
|AssumedRoleId |String |Yes |A unique identifier that contains the role ID and the role session name of the role that is being assumed. |


<span id="066feddc"></span>
## Sample response

**Success response**

```text
{
    "ResponseMetadata": {
        "RequestId": "202104124922",
        "Action": "AssumeRole",
        "Version": "2018-01-01",
        "Service": "sts"
    },
    "Result": {
        "Credentials": {
            "CurrentTime": "2021-04-12T10:57:09+08:00",
            "ExpiredTime": "2021-04-12T11:57:09+08:00",
            "AccessKeyId": "AKTPODg0MzV**2ZDcxMDg",
            "SecretAccessKey": "TVRNNVlqRmxPR1**mRoTkdWbE1ESQ==",
            "SessionToken": "STSeyJBY2NvdW50SW**klkZW50aXR5VHlwZSI6NCwiSWRlbnRpdHlJZCI6MzAyMTcsIkNoYW5uZWwiOiJyZXNvdXJjZSIsIkFjY2Vzc0tleUlkIjoiQUtUUE9EZzBNelZrWlRNMVlqQXlOR05sWkdGbU0yVTNaVEl6T0RnMlpEY3hNRGciLCJTaWduZWRTZWNyZXRBY2Nlc3NLZXkiOiJHSHRuc2Q1b3BOOThUeUNrckVuMVAxTDd1ZzBXczZFMytzTktDMDJQT01lNzFMOUloNzhYaDB5VXE4Ni9JMW8reEZxTmtkK01tVUR0cjRHR0NodXJQdz09IiwiRXhwaXJlZFRpbWUiOjE2MTgxOTk4MjksIlBvbGljeVN0cmluZyI6IiIsIlNpZ25hdHVyZSI6IjdiZTEzNTU1MDM5NzcyM2VkMDQxYmVkNTIyNzU4YmMyNjQ3YzRmNzZiNmRjYTViNzVhZDUyOTMwYTg1NjE5ZGEiLCJTZXNzaW9uTmFtZSI6ImNlc2hpYXNzdW1lIn0="
        },
        "AssumedRoleUser": {
            "Trn": "trn:sts::20**94:assumed-role/ServiceRoleFor**/ceshiassume",
            "AssumedRoleId": "**:ceshiassume"
        }
    }
}
```


**Error response**

```text
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "AssumeRole",
        "Version": "2018-01-01",
        "Service": "sts",
        "Region": "ap-singapore-1",
        "Error": {
            "Code": "NoPermission",
            "Message": ""
        }
    }
}
```
