---
title: "DescribeTemplates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates"
---

Retrieve a list of policies that meet the filter criteria.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeTemplates`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Filters |Object[] |No |Indicates a set of filtering criteria used to obtain a list of policies that meet these criteria. If you do not specify any filtering criteria, this API returns all policies under your account.<br><br>Multiple filtering criteria are related by `AND`, meaning only policies that meet all filtering criteria will be included in the list returned by this API.<br><br>In the API response, the actual policies returned are affected by `PageNum` and `PageSize`. | |
|Fuzzy |Boolean |No |Indicates the matching method. This parameter can take the following values:<br><br><br>* `true`: Indicates fuzzy matching. A policy is considered to meet the filtering criteria if the corresponding value of `Name` contains any value in the `Value` array.<br><br>* `false`: Indicates exact matching. A policy is considered to meet the filtering criteria if the corresponding value of `Name` matches any value in the `Value` array.<br><br><br>Moreover, the `Fuzzy` value you can specify is affected by the `Name` value. See the description of `Name`.<br><br>The default value of this parameter is `false`.<br><br>Note that the matching process is case\-sensitive. |`true` |
|Name |String |No |Represents the filtering type. This parameter can take the following values:<br><br><br>* `Title`: Filters policies by name.<br><br>* `Id`: Filters policies by ID. For this parameter value, the value of `Fuzzy` can only be `false`.<br><br>* `Domain`: Filters policies by the bound domain name.<br><br>* `Type`: Filters policies by type. For this parameter value, the value of `Fuzzy` can only be `false`.<br><br>* `Status`: Filters policies by status. For this parameter value, the value of `Fuzzy` can only be `false`.<br><br><br>You can specify multiple filtering criteria simultaneously, but the `Name` in different filtering criteria cannot be the same. |`Title` |
|Value |String[] |No |Represents the values corresponding to `Name`, which is an array.<br><br><br>* When `Name` is `Title`, `Id`, or `Domain`, each value in the `Value` array should not exceed 100 characters in length.<br><br>* When `Name` is `Type`, the `Value` array can include one or more of the following values:<br><br>   * `cipher`: Indicates a encryption policy.<br><br>   * `service`: Indicates a delivery policy.<br><br>   * `rule`：Indicates a rules engine policy.<br><br>* When `Name` is `Status`, the `Value` array can include one or more of the following values:<br><br>   * `locked`: Indicates the status is "published".<br><br>   * `editing`: Indicates the status is "draft".<br><br><br>tip<br><br><br>* When `Fuzzy` is `false`, you can specify multiple values in the array.<br><br>* When `Fuzzy` is `true`, you can only specify one value in the array. |`["NetTVWeb001","NetTV003"]` |
|PageNum |Long |No |For the policy list returned by the API, this parameter Indicates a page number. The actual policies returned by the API are those on the page specified by this page number.<br><br>The policies returned by the API are paginated according to `PageSize`. Assuming the API returns a total of 100 policies and you specify a `PageSize` of `10`, then the policies are distributed across 10 pages. If you specify a `PageNum` of `2`, it means to retrieve the policies on the second page.<br><br>If there are no policies on the specified page, the `Templates` parameter in the return result will be `null`.<br><br>The default value of `PageNum` is `1`. |`1` |
|PageSize |Long |No |Indicates the number of policies included in each page.<br><br>The value of this parameter ranges from 1 to 200, with a default value of `10`. |`10` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Templates |Object[] |Indicates the list of policies returned by this API.<br><br>Note that, the policies in the list are those on the page specified by the `PageNum` parameter, not necessarily all policies that meet the filtering criteria. | |
|BoundDomains |Object[] |Represents a list of domain names bound to the policy specified by `TemplateId`.<br><br>If the policy is not bound to any domain names, the value of this parameter is `null`. | |
|BoundTime |Long |Indicates the time when the policy was bound to the domain name specified by `Domain`, in Unix timestamp format. |`1709174039` |
|Domain |String |Represents one of the domain names bound to the policy. |`www.example.com` |
|CreateTime |Long |Indicates the creation time of the policy, in Unix timestamp format. |`1709173909` |
|Message |String |Indicates the description of the policy. |`This is a test` |
|Status |String |Indicates the status of `ProdVersion`. This parameter has the following values:<br><br><br>* `editing`: Indicates the status is "draft". In this case, the value of `ProdVersion` is empty ("").<br><br>* `locked`: Indicates the status is "published". |`locked` |
|TemplateId |String |Indicates the ID of a policy in the list of policies returned by the API. |`tpl-sZRpwq` |
|Title |String |Indicates the name of the policy. |`NetTVWeb001` |
|Type |String |Indicates the type of the policy. This parameter can take the following values:<br><br><br>* `cipher`: Indicates an encryption policy.<br><br>* `service`: Indicates a distribution policy.<br><br>* `rule`：Indicates a rules engine policy。 |`cipher` |
|UpdateTime |Long |Indicates the last modification time of the policy, in Unix timestamp format.<br><br>If the policy has not been updated since its creation, the value of this parameter is the same as `CreateTime`. |`1709174039` |
|Exception |Boolean |Indicates whether the policy includes special configurations. Special configurations refer to those not operated by users but by BytePlus engineers. This parameter can take the following values:<br><br><br>* `true`: Indicates it includes special configurations.<br><br>* `false`: Indicates it does not include special configurations. |`false` |
|Project |String |Indicates the project to which the policy belongs. |`default` |
|ProdVersion |String |Indicates the published version (with status `running`) of the policy. If there is no version with status `running`, this parameter value is empty (""). |`P-250411.32717` |
|DomainCount |Long |域名数量 | |
|TotalCount |Long |Indicates the number of policies that meet the filtering criteria. The value of this parameter is not affected by `PageSize` and `PageNum`. |`2` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Title",
            "Fuzzy": false,
            "Value": [
                "NetTVWeb001",
                "NetTV003"
            ]
        },
        {
            "Name": "Id",
            "Fuzzy": false,
            "Value": [
                "tpl-sZRpwq",
                "tpl-sWm5EW"
            ]
        },
        {
            "Name": "Domain",
            "Fuzzy": true,
            "Value": [
                "example.com"
            ]
        },
        {
            "Name": "Type",
            "Fuzzy": false,
            "Value": [
                "cipher",
                "service"
            ]
        },
        {
            "Name": "Status",
            "Fuzzy": false,
            "Value": [
                "locked",
                "editing"
            ]
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202403030536061418EF0E947E85EC76B6",
        "Action": "DescribeTemplates",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Templates": [
            {
                "BoundDomains": [
                    {
                        "BoundTime": 1709174039,
                        "Domain": "www.example.com"
                    }
                ],
                "CreateTime": 1709173909,
                "Exception": false,
                "Message": "",
                "Project": "default",
                "Status": "locked",
                "TemplateId": "tpl-sZRpwq",
                "Title": "NetTVWeb001",
                "Type": "service",
                "UpdateTime": 1709174039,
                "ProdVersion": "P-250411.32717"
            },
            {
                "BoundDomains": null,
                "CreateTime": 1709018409,
                "Exception": false,
                "Message": "Rewrite",
                "Project": "default",
                "Status": "editing",
                "TemplateId": "tpl-sWm5EW",
                "Title": "NetTV003",
                "Type": "service",
                "UpdateTime": 1709018409,
                "ProdVersion": ""
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
