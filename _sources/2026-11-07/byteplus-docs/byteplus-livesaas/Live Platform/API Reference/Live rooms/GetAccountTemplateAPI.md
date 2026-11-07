---
title: "GetAccountTemplateAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccounttemplateapi"
---

Call this API to get the list of live room templates under your BytePlus account. You can then find the ID of a published template and use it to create a live room with the template's configurations.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetAccountTemplateAPI&Version=2020-06-01`

* Method: GET


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following table. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetAccountTemplateAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|PageNo |Integer |No |`1` |The number of the page to return.<br><br>Default value: `1`. |
|PageItemCount |Integer |No |`10` |The number of results to return on each page.<br><br>Value range: [1,500].<br><br>Default value: `10`. |
|Status |Integer |No |`0` |The template status.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Returns created, unpublished, and published templates.<br><br>* `1`: Created and unpublished templates are to be returned.<br><br><br>A “created” template has not yet been published, while an “unpublished” template was previously published. |
|Keyword |String |No |`Template A` |A keyword for filtering templates by name. The API returns only templates whose names contain this keyword.<br><br>Value range: [1,64] |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|TemplateList |Array of [TemplateList](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi) |`-` |List of templates. |
|PageNo |Integer |`1` |The returned page number. |
|PageItemCount |Integer |`10` |The number of results returned on each page. |
|TotalItemCount |Integer |`1` |The total number of returned templates. |
|EnabledTemplateCount |Integer |`0` |The total number of published templates. |


<span id="templatelist"></span>
### TemplateList


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|TemplateId |Long |`172436707693****` |The template ID. |
|TemplateName |String |`Template A` |The template name. |
|Status |Integer |`1` |The template status.<br><br><br>* `1`: Created.<br><br>* `2`: Unpublished.<br><br>* `3`: Published.<br><br>* A created template is not yet published, while an unpublished template was published before.<br><br>* Only published templates can be used to create live rooms. |
|CoverImage |String |`//p1-live.byteimg.com/tos-cn-i-gjr78lqtd0/29133e74110444****42013881a6be4b~tplv-gjr78lqtd0-image.image` |The URL of the returned template's cover image, without a protocol header. |
|Description |String |`A template for game streaming.` |The template description. |
|ModifyTime |Long |`1706166059` |The time the template was last updated, in Unix timestamp format (seconds). |
|IsSystemTemplate |Integer |`2` |Indicates whether the template is a system template or a custom template. You cannot modify a system template.<br><br><br>* `1`: System template.<br><br>* `2`: Custom template. |
|IsDefaultTemplate |Integer |`0` |Indicates whether the template is the default template.<br><br><br>* `0`: Not the default template.<br><br>* `1`: The default template. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAccountTemplateAPI&Version=2020-06-01&PageNo=1&PageItemCount=10&Status=0&Keyword=Template A
```


<span id="sample-response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetAccountTemplateAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1706166145
    },
    "Result": {
        "PageNo": 1,
        "PageItemCount": 10,
        "TotalItemCount": 1,
        "TemplateList": [
            {
                "TemplateId": 172436707693****,
                "TemplateName": "Template A",
                "Status": 1,
                "CoverImage": "//p1-live.byteimg.com/tos-cn-i-gjr78lqtd0/29133e74110444****42013881a6be4b~tplv-gjr78lqtd0-image.image",
                "Description": "A template for game streaming.",
                "ModifyTime": 1706166059,
                "IsSystemTemplate": 2,
                "IsDefaultTemplate": 0
            }
        ],
        "EnabledTemplateCount": 0
    }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Name |Message |Solution |
|---|---|---|
|100000 |Internal error. |Contact technical support. |
|200001 |The PageItemCount must be equal to or less than 500. |Change the `PageItemCount` value. |
|200001 |The specified parameter Status is invalid. |Change the `Status` value. |
