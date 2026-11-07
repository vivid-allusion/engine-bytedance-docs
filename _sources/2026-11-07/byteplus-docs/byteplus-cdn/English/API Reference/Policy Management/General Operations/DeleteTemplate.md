---
title: "DeleteTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-deletetemplate"
---

Delete a policy or a specific version of a policy.

**Delete a policy**

When a policy is deleted, all versions under this policy will be deleted.

To delete a policy, the policy must not be bound to any domain. You can call [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to check if a policy is bound to any domain. You can only delete a policy when its `BoundDomains` is `null`.

If a policy is bound to one or more domains and you need to unbind it from these domains, see the related description in [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updatetemplatedomain-05d27).

**Delete a policy version**

You can only delete unpublished policy versions, which means you can only delete versions with `Status` set to `draft` or `stop`. To get all versions under a policy and the status of each version, see [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us).

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DeleteTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the ID of the policy you want to delete.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to obtain the ID of the policy you want to delete. |`tpl-s2N4rW` |
|TemplateVersion |String |No |Indicates the version to be deleted. The status of this version cannot be `running`.<br><br>You can call [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn) to get all versions under this policy and their status. |`P-250414.89520` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-sqdYQ2",
    "TemplateVersion": "P-250414.89520"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202508251227583CD38EED31C8FCA7FF07",
        "Action": "DeleteTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
