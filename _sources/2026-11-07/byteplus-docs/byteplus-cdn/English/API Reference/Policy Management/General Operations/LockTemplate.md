---
title: "LockTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-locktemplate"
---

Publish a policy, which means publishing a version with `draft` status under this policy.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This API is no longer maintained. We recommend using <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/ReleaseTemplate_en-us">ReleaseTemplate</a> instead.</div>


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=LockTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `LockTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the ID of the policy to be published.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to obtain the ID of the policy you wish to publish. |`tpl-s2N4rW` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=LockTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-s2N4rW"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "StartCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
