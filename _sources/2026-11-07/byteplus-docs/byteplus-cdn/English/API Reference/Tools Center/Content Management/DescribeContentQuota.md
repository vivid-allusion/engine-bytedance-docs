---
title: "DescribeContentQuota"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecontentquota"
---

Retrieve the daily purge and prefetch quotas and remaining quotas for your BytePlus account.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeContentQuota`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|PreloadLimit |Long |Indicates the maximum number of URLs that can be prefetched per request. |`100` |
|PreloadQuota |Long |Indicates the daily number of URLs that can be prefetched. |`1000` |
|PreloadRemain |Long |Indicates the remaining number of URLs that can be prefetched today. |`10` |
|RefreshDirLimit |Long |Indicates the maximum number of directories that can be purged per request. |`100` |
|RefreshDirQuota |Long |Indicates the daily number of directories that can be purged. |`50` |
|RefreshDirRemain |Long |Indicates the remaining number of directories that can be purged today. |`15` |
|RefreshQuota |Long |Indicates the daily number of URLs that can be purged. |`10000` |
|RefreshQuotaLimit |Long |Indicates the maximum number of URLs that can be purged per request. |`100` |
|RefreshRemain |Long |Indicates the remaining number of URLs that can be purged today. |`200` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021-03-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202310271225559FCEDC662FFE48246DCB",
        "Action": "DescribeContentQuota",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PreloadLimit": 100,
        "PreloadQuota": 1000,
        "PreloadRemain": 1000,
        "RefreshDirLimit": 100,
        "RefreshDirQuota": 50,
        "RefreshDirRemain": 50,
        "RefreshQuota": 10000,
        "RefreshQuotaLimit": 100,
        "RefreshRemain": 1000
    }
}
```


&nbsp;
