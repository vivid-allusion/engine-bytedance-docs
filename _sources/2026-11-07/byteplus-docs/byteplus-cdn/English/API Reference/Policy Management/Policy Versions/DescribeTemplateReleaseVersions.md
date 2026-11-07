---
title: "DescribeTemplateReleaseVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us"
---

Get the version list of a specified policy. You can additionally specify parameters to filter and sort the version list.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each policy records a maximum of 50 published versions.</div>


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeTemplateReleaseVersions`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the policy ID for which to get the version list. |`tpl-s18ynd9` |
|Filters |Object[] |No |Indicates a list of filter conditions, containing up to 10 conditions. | |
|Name |String |No |Indicates the filter object. This parameter has the following values:<br><br><br>* `Status`: Filters the version list by policy status.<br><br>* `Version`: Filters the version list by version number. |`Status` |
|Value |String[] |No |Indicates the list of filter values.<br><br><br>* When `Name` is `Status`, you can specify one or more of the following values:<br><br>   * `stop`: Indicates the status is "Unpublished".<br><br>   * `running`: Indicates the status is "Published".<br><br>   * `draft`: Indicates the status is "Draft".<br><br>* When `Name` is `Version`, you can specify one or more version numbers, up to 10. |`["stop","running"]` |
|Fuzzy |Boolean |No |Indicates the matching method. This parameter value can only be `false`, indicating exact matching.<br><br>The default value of this parameter is `false`. |`false` |
|SortRule |Object |No |Indicates the sorting rules. | |
|OrderBy |String |No |Indicates the sorting object. This parameter has the following values:<br><br><br>* `CreateTime`: Indicates the creation time of the version.<br><br>* `ReleaseTime`: Indicates the latest publish time of the version.<br><br>* `Version`: Indicates the version number. |`CreateTime` |
|Asc |Boolean |No |Indicates the sorting order. This parameter has the following values:<br><br><br>* `false`: Indicates descending order.<br><br>* `true`: Indicates ascending order.<br><br><br>The default value of this parameter is `false`. |`false` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Total |Long |Indicates the number of versions that meet the filter conditions. |`10` |
|Versions |Object[] |Indicates the list of versions that meet the conditions. | |
|Version |String |Indicates the version number of a version in the list.<br><br><br>* If `Status` is `draft`, the version number is `draft`.<br><br>* If `Status` is not `draft`, the version number is a string, following the naming convention `P-<first_publish_date>-<random_5_digits>`. |`P-250414.89520` |
|CreateTime |Long |Indicates the creation time of the version in Unix timestamp format. |`1744610623` |
|Env |String |Indicates the publishing environment of the version.<br><br><br>* If `Status` is not `draft`, this parameter value is always `prod`, indicating the production environment.<br><br>* If `Status` is `draft`, this parameter value is empty (""). |`prod` |
|Message |String |Indicates the description of the version. |`my desc` |
|ReleaseTime |Long |Indicates the latest publish time of the version in Unix timestamp format. |`1744610623` |
|Status |String |Indicates the status of the version.<br><br><br>* `stop`: Indicates the status is "Unpublished".<br><br>* `running`: Indicates the status is "Published".<br><br>* `draft`: Indicates the status is "Draft". |`stop` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Filters": [
        {
            "Name": "Status",
            "Value": [
                "stop",
                "running",
                "draft"
            ]
        }
    ],
    "SortRule": {
        "OrderBy": "CreateTime",
        "Asc": true
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202504140728216B5EA730EF294C000118",
        "Action": "DescribeTemplateReleaseVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "CreateTime": 1744361302,
                "Env": "prod",
                "Message": "aaa",
                "ReleaseTime": 1744613891,
                "Status": "running",
                "Version": "P-250411.16282"
            },
            {
                "CreateTime": 1744364788,
                "Env": "prod",
                "Message": "sdfgh",
                "ReleaseTime": 1744599039,
                "Status": "stop",
                "Version": "P-250414.89520"
            },
            {
                "CreateTime": 1744610623,
                "Env": "",
                "Message": "",
                "ReleaseTime": 1744610623,
                "Status": "draft",
                "Version": "draft"
            }
        ]
    }
}
```


&nbsp;
