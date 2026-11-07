---
title: "SubmitPreloadTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-submitpreloadtask"
---

Submit a prefetch task in BytePlus CDN to cache one or more files in advance to the CDN cache nodes.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

By default, each BytePlus primary account has the following task quotas:


* Up to 1,000 URLs can be prefetched per day.

* Up to 100 URLs can be prefetched per task.


<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `SubmitPreloadTask`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|UrlList |String[] |No |Indicates one or more file URLs. CDN will cache these files in advance to the cache nodes.<br><br>tip<br><br>URLs cannot contain wildcard domains. If you need to submit a prefetch task for multiple subdomains under a wildcard domain, you must specify the URLs to be prefetched for each subdomain. |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|Area |String |No |Indicates a service region. CDN will cache each file in `Urls` in advance to the cache nodes under this region. The available values for this parameter are:<br><br><br>* `chinese_mainland`: Indicates Chinese mainland.<br><br>* `outside_chinese_mainland`: Indicates global, excluding Chinese mainland.<br><br>* `global`: Indicates global.<br><br><br>If this parameter is not specified, for a URL in `Urls`, the service region is the service region of the domain name contained in that URL. |`outside_chinese_mainland` |
|ConcurrentLimit |Long |No |Indicates the maximum number of files requested from the origin server by CDN when executing prefetch tasks. The default value is `10`, and the value range of this parameter is 1\-1000. |`20` |
|Urls |String |No |It is **not recommended** to use this parameter. Please use `UrlList` instead.<br><br>This parameter has the same function as `UrlList` . When specifying multiple URLs in `Urls` , the URLs must be separated by `\n` .<br><br>If you specify both `UrlList` and `Urls` , only `UrlList` takes effect. |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TaskID |String |Indicates the ID of the task. You can call [DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecontenttasks) to view the prefetch results of each URL in `Urls`. |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021-03-01
{
    "UrlList": [
        "https://www.example.com/1.jpg",
        "https://www.example.com/2.jpg"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202406300908245F2C63BC765D774F1CB0",
        "Action": "SubmitPreloadTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871"
    }
}
```


&nbsp;
