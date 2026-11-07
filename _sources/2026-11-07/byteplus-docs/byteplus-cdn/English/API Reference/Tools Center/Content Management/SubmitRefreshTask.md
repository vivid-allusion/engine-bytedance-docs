---
title: "SubmitRefreshTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitrefreshtask"
---

Submit a purge task in BytePlus CDN. If file URLs are specified in the task, the CDN will delete these files when executing the task. If directories are specified in the task, the CDN will mark the files in these directories as expired by default.

<span id="instructions"></span>
## Instructions

Throttle limits: You can send up to 20 requests per second.

By default, the purge quota for each BytePlus primary account is as follows:


* Purge up to 10,000 URLs per day.

* Purge up to 50 directories per day.

* Each task can contain up to 100 URLs or 50 directories.


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `SubmitRefreshTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Type |String |No |Indicates a purge type. The parameter has the following values:<br><br><br>* `file`: Indicates URL Purge, performing purge operations on one or more files.<br><br>* `dir`: Indicates Directory Purge, performing purge operations on all files under one or more directories, including files in subdirectories.<br><br>* `regex`: Indicates a RegEx Purge. Specify one or more regular expressions to perform a purge operation on file URLs that match the regular expressions. To use RegEx Purge, please [submit a ticket](https://console.byteplus.com/workorder/create). For an introduction to RegEx Purge and URL specifications, see [RegEx Purge](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge#regex-purge).<br><br><br>The default value of this parameter is `file`. |`file` |
|Prefix |Boolean |No |Indicates whether to use Purge by Prefix. This parameter is only valid when `Type` is `dir`, with the following values:<br><br><br>* `true`: Indicates using Purge by Prefix, performing purge operations on all files under directories starting with the specified prefix.<br><br>* `false`: Indicates not using Purge by Prefix.<br><br><br>The default value of this parameter is `false`. |`true` |
|UrlList |String[] |No |Indicates a list of URLs to be purged. Each URL must start with `http://` or `https://`.<br><br><br>* When `Type` is `file`, you specify file URLs.<br><br>* When `Type` is `dir`,<br><br>   * If `Prefix` is `false`, you specify directories ending with `/`, for example, `http://www.example.com/image/`.<br><br>   * If `Prefix` is `true`, you specify directory prefixes. For example, `http://www.example.com/im` can match both `http://www.example.com/image/` and `http://www.example.com/ime/` directories.<br><br>* When `Type` is `regex`, you specify regular expressions to match file URLs. See [RegEx Purge](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge#regex-purge). To specify this parameter value, please [submit a ticket](https://console.byteplus.com/workorder/create).<br><br><br>tip<br><br>You cannot directly purge files and directories under a wildcard domain. Instead, you need to perform these operations for each subdomain. |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|Delete |Boolean |No |Indicates whether to delete the files specified by `Urls` or `UrlList` from the cache. This parameter is only valid when `Type` is `dir`. To use this parameter, please [submit a ticket](https://console.byteplus.com/workorder/create).<br><br>This parameter has the following values:<br><br><br>* `true`: Indicates deleting these files. After that, if requests for these files are received, the CDN will request these files from the origin server.<br><br>* `false`: Indicates not deleting these files, only marking them as expired. After that, if requests for these files are received, the CDN will perform [origin validation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules#origin-validation).<br><br><br>The default value of this parameter is `false`. |`false` |
|Urls |String |No |It is **not recommended** to use this parameter. Please use `UrlList` instead.<br><br>This parameter has the same function as `UrlList` . When specifying multiple URLs in `Urls` , the URLs must be separated by `\n` .<br><br>If you specify both `UrlList` and `Urls` , only `UrlList` takes effect. |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |
|RequestHeaderInstances |Object[] |No |Specifies the request headers that must be included in the cache key of the files to be purged. A file is matched and purged only when its cache key completely contains the request headers specified here.<br><br>The list can contain up to 10 request headers. | |
|Key |String |No |Specifies the name of a request header in the list. The name has the following requirements:<br><br><br>* The name cannot be `User-Agent`.<br><br>* The name cannot start with `x-bdcdn-` or `Volc-Cdn`.<br><br>* The length cannot exceed 1,024 characters. |`header1` |
|Value |String |No |Specifies the value of the request header. The length cannot exceed 1,024 characters. |`value1` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TaskID |String |Indicates the ID of the task. You can call [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecontenttasks) to view the purge results of each object in the `Urls` list. |`refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021-03-01
{
    "Type": "file",
    "UrlList": [
        "https://www.example.com/1.txt",
        "https://www.example.com/2.txt"
    ],
    "RequestHeaderInstances": [
        {
            "Key": "header1",
            "Value": "value1"
        },
        {
            "Key": "header2",
            "Value": "value2"
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202201141648440102100180260E003ABA",
        "Action": "SubmitRefreshTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0"
    }
}
```
