---
title: "ListSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en"
---

Based on the specified query conditions, get the list of universal catalogs that meet the conditions.

<span id="usage-limits"></span>
## Usage Limits

Rate Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListSharedConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConfigName |String |No |Indicates the name of a universal catalog, used to get the universal catalog that exactly matches this name. |`my_list` |
|ConfigType |String |No |Indicates the type of a universal catalog, used to get the list of universal catalogs of this type. This parameter has the following values:<br><br><br>* `deny_ip_access_rule`: Indicates IP blocklist.<br><br>* `allow_ip_access_rule`: Indicates IP allowlist.<br><br>* `4xx_error_page`: Indicates custom error page.<br><br>* `deny_referer_access_rule`: Indicates Referer blocklist.<br><br>* `allow_referer_access_rule`: Indicates Referer allowlist.<br><br>* `common_match_list`: Indicates general list. |`allow_ip_access_rule` |
|PageNum |Long |No |Indicates a page number. CDN paginates the list of universal catalogs that meet the query conditions based on `PageSize`. Suppose the number of universal catalogs returned by this API is 100, and `PageSize` is `10`, then these universal catalogs are distributed on 10 pages. CDN displays the universal catalogs on the first page by default.<br><br>The default value of this parameter is `1`. |`1` |
|PageSize |Long |No |Indicates the number of universal catalogs contained per page.<br><br>The value range of this parameter is 1\-1,000, the default value is `10`. |`10` |
|Project |String |No |Indicates a project name, used to get the list of universal catalogs belonging to this project. |`default` |
|ConfigTypeList |String[] |No |Indicates one or more types of universal catalogs, used to get the list of universal catalogs of these types. The value of this parameter can be a combination of available `ConfigType` values. `ConfigType` and `ConfigTypeList` cannot be specified at the same time. |`["allow_ip_access_rule","deny_ip_access_rule"]` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|ConfigData |Object[] |Indicates the list of universal catalogs that meet the query conditions. | |
|ConfigName |String |Indicates the name of a universal catalog in the list. |`my_list` |
|ConfigType |String |Indicates the type of this universal catalog. This parameter has the following values:<br><br><br>* `deny_ip_access_rule`: Indicates IP blocklist.<br><br>* `allow_ip_access_rule`: Indicates IP allowlist.<br><br>* `4xx_error_page`: Indicates custom error page.<br><br>* `deny_referer_access_rule`: Indicates Referer blocklist.<br><br>* `allow_referer_access_rule`: Indicates Referer allowlist.<br><br>* `common_match_list`: Indicates common list. |`deny_ip_access_rule` |
|DomainCount |Long |Indicates the number of domain names associated with this universal catalog. |`2` |
|Project |String |Indicates the project to which this universal catalog belongs. |`default` |
|UpdateTime |Long |Indicates the last modification time of this universal catalog, in Unix timestamp. |`1655856000` |
|PageNum |Long |Indicates the `PageNum` you specified in the request parameters. |`1` |
|PageSize |Long |Indicates the `PageSize` you specified in the request parameters. |`10` |
|Total |Long |Indicates the total number of universal catalogs that meet the query conditions. |`20` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021-03-01
{
    "ConfigType":"allow_ip_access_rule"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240117195639014D4059167D42B2C640",
        "Action": "ListSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigData": [
            {
                "ConfigName": "deny_ip",
                "ConfigType": "deny_ip_access_rule",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705492181
            },
            {
                "ConfigName": "error_page",
                "ConfigType": "4xx_error_page",
                "DomainCount": 1,
                "Project": "default",
                "UpdateTime": 1705334019
            },
            {
                "ConfigName": "common_list",
                "ConfigType": "common_match_list",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705332721
            },
            {
                "ConfigName": "deny_referer",
                "ConfigType": "deny_referer_access_rule",
                "DomainCount": 3,
                "Project": "default",
                "UpdateTime": 1702484378
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 34
    }
}
```


&nbsp;
