---
title: "ReleaseTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ReleaseTemplate_en-us"
---

Release a specific version of a policy.


* If the status of the version to be released is `draft`, this API operation corresponds to the "Publish" operation in the console.

* If the status of the version to be released is `stop`, this API operation corresponds to the "Rollback" operation in the console.


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ReleaseTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |The policy ID where the version to be released is located. |`tpl-s18ynd9` |
|Env |String |No |The release environment. Currently, this parameter can only be set to `prod`, indicating the production environment. The default value is also `prod`. |`prod` |
|Message |String |No |The description of the release operation. |`My Desc` |
|TemplateVersion |String |No |The version number to be released. The default value is `draft`. |`P-250411.16282` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "TemplateVersion": "P-250411.16282"
}
```


&nbsp;
