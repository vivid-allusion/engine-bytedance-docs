---
title: "DescribeLiveASRDurationData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveasrdurationdata"
---

Call the `DescribeLiveASRDurationData` API to query the duration of AI speech\-to\-subtitle conversion within a specified time range.

<span id="requirements"></span>
## Requirements

Rate limit: 30 queries per second per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveASRDurationData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveASRDurationData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com"]` |List of domains. By default, it is empty, indicating that the duration of AI speech\-to\-subtitle usage data for all domains under your BytePlus MediaLive will be queried. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or go to the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domains to be queried. |
|AppList |Array of String |No |`["live"]` |A list of application names must match the value of the AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|ASRSourceType |String |No |`ZH` |This parameter refers to the language type of the speech during AI speech\-to\-subtitle conversion. By default, it indicates querying all languages. The specific values and meanings are as follows:<br><br><br>* `ZH`: Chinese;<br><br>* `EN`: English;<br><br>* `JA`: Japanese;<br><br>* `KO`: Korean.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both <code>ASRTargetTypeList</code> and <code>ASRSourceType</code> must be specified simultaneously.</div><br> |
|ASRTargetTypeList |Array of String |No |`["ZH"]` |List of language types of the subtitles generated during AI speech\-to\-subtitle conversion. By default, it indicates querying all languages. The specific values and meanings are as follows:<br><br><br>* `ZH`: Chinese;<br><br>* `EN`: English;<br><br>* `JA`: Japanese;<br><br>* `KO`: Korean.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both <code>ASRTargetTypeList</code> and <code>ASRSourceType</code> must be specified simultaneously.</div><br> |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |Yes |`2021-04-13T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |No |`300` |The aggregation time granularity, measured in seconds, supports the following time granularities:<br><br><br>* `300`: (default) 5 minutes. When the time granularity is 5 minutes, the maximum time span for a single query is 31 days, and the historical query time range is 93 days;<br><br>* `3600`: 1 hour. When the time granularity is 1 hour, the maximum time span for a single query is 93 days, and the historical query time range is 93 days;<br><br>* `86400`: 1 day. When the time granularity is 1 day, the maximum time span for a single query is 93 days, and the historical query time range is 93 days. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"]` |The list of domains. |
|AppList |Array of String |`["live"]` |List of application names. |
|ASRSourceType |String |`ZH` |Language type of the speech during AI speech\-to\-subtitle conversion, with values and meanings as follows:<br><br><br>* `ZH`: Chinese;<br><br>* `EN`: English;<br><br>* `JA`: Japanese;<br><br>* `KO`: Korean. |
|ASRTargetTypeList |Array of String |`["ZH"]` |List of language types of the subtitles generated during AI speech\-to\-subtitle conversion, with values and meanings as follows:<br><br><br>* `ZH`: Chinese;<br><br>* `EN`: English;<br><br>* `JA`: Japanese;<br><br>* `KO`: Korean. |
|StartTime |String |`2021-04-13T00:00:00Z` |The start time of your query's range in RFC 3339 format with second precision. |
|EndTime |String |`2021-04-13T00:00:00Z` |The end time of your query's range in RFC 3339 format with second precision. |
|Aggregation |Integer |`300` |Data granularity, measured in seconds. |
|Duration |Float |`1.1` |Total duration of AI speech\-to\-subtitle transcoding, measured in minutes. |
|ASRDurationData |Array of [ASRDurationData](https://docs.byteplus.com/en/docs/24/25106#asrdurationdata) |`-` |Data for all time granularities. |
|ASRDurationDetailData |Array of [ASRDurationDetailData](https://docs.byteplus.com/en/docs/24/25106#asrdurationdetaildata) |`-` |Detailed data of time granularities split by the language type of the subtitles generated during AI speech\-to\-subtitle conversion. |


<span id="asrdurationdata"></span>
### ASRDurationData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2021-04-13T00:00:00Z` |Start time of each time granularity when data is aggregated by time granularity, in the UTC time of RFC3339 format timestamps with second precision. |
|Duration |Float |`1.1` |Duration of AI speech\-to\-subtitle conversion within the current data aggregation time granularity, measured in minutes. |


<span id="asrdurationdetaildata"></span>
### ASRDurationDetailData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ASRSourceType |String |`ZH` |Language type of the speech during AI speech\-to\-subtitle conversion. |
|ASRTargetTypeList |Array of String |`["ZH"]` |List of language types of the subtitles generated during AI speech\-to\-subtitle conversion. |
|ASRDurationData |Array of [ASRDurationData](https://docs.byteplus.com/en/docs/24/25106#asrdurationdata) |`-` |Data for all time granularities split by the language type of the speech. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveASRDurationData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "AppList": [
        "live"
    ],
    "ASRSourceType": "ZH",
    "ASRTargetTypeList": [
        "ZH"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-13T00:00:00Z",
    "Aggregation": 300
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveASRDurationData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "AppList": [
            "live"
        ],
        "ASRSourceType": "ZH",
        "ASRTargetTypeList": [
            "ZH"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-13T00:00:00Z",
        "Aggregation": 300,
        "Duration": 1.1,
        "ASRDurationData": [
            {
                "TimeStamp": "2021-04-13T00:00:00Z",
                "Duration": 1.1
            }
        ],
        "ASRDurationDetailData": [
            {
                "ASRSourceType": "ZH",
                "ASRTargetTypeList": [
                    "ZH"
                ],
                "ASRDurationData": [
                    {
                        "TimeStamp": "2021-04-13T00:00:00Z",
                        "Duration": 1.1
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/25106#request-parameters) description for inspection. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
