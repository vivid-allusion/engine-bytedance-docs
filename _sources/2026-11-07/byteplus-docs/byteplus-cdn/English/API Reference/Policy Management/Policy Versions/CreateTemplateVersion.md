---
title: "CreateTemplateVersion"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_en-us"
---

Create a draft version for a policy.


* By default, this API creates a draft version based on the currently published version, which corresponds to the "Create Version" operation in the console. The created draft version has the same configuration as the currently published version.

* You can also specify an existing version to create a draft version, which corresponds to the "Duplicate Version" operation in the console.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot call this API for a policy that already contains a draft version.</div>


<div data-tips="true" data-tips-type="tip">To determine whether a specified policy contains a draft version, you can call <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us">DescribeTemplateReleaseVersions</a> for the specified policy. In the version list returned by the API, check if there is a version with <code>Status</code> set to <code>draft</code>.</div>


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `CreateTemplateVersion`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the policy ID for which a draft version needs to be created. |`tpl-s18ynd9` |
|Message |String |No |Indicates the description of this draft version. |`my desc` |
|ReferredVersion |String |No |Indicates an existing version ID based on which this API creates a draft version.<br><br>The value of this parameter cannot be `draft`. The default value is the ID of the currently published version.<br><br>You can call [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us) to get all versions under this policy. |`P-250414.89520` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Message": "Hello World",
    "ReferredVersion": "P-250414.89520"
}
```


&nbsp;
