---
title: "DuplicateTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-duplicatetemplate"
---

Create a policy by duplicating an existing one with the same configurations and type.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DuplicateTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ReferredTemplateId |String |Yes |Indicates the ID of the policy to be duplicated.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) to obtain the ID of the policy you wish to duplicate. |`tpl-sZRpwq` |
|Message |String |No |Indicates the description of the created policy, which should not exceed 120 characters in length. |`This is a dup policy.` |
|Title |String |No |Indicates the name of the created policy, which should not exceed 100 characters in length.<br><br>If the parameter is not specified, CDN will generate a random name. |`Dup_Policy` |
|Project |String |No |Indicates the project to which the created policy belongs.<br><br>The default value of this parameter is "default", indicating the Default project. |`default` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TemplateId |String |Indicates the ID of the created policy. |`tpl-s2N4rW` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021-03-01
{
    "ReferredTemplateId": "tpl-sZRpwq",
    "Title": "Dup_Policy",
    "Message": "This is a dup policy."
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024030403552737EB957CFE0697DBB981",
        "Action": "DuplicateTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-s2N4rW"
    }
}
```


&nbsp;
