---
title: "GetVodMediaPlayData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getvodmediaplaydata"
---

Retrieve video playback QoS and QoE metrics within a specified time range using the application ID.

<span id="requirements"></span>
## Requirements


* This API has a per\-user QPS limit of 10 requests per second.

* Data from the past year is supported.

* A single query's time range cannot exceed 90 days.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=GetVodMediaPlayData&Version=2025\-04\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetVodMediaPlayData` |The API action. For the current API, the value is `GetVodMediaPlayData`. |
|Version |String |Yes |`2025-04-01` |The API version. For the current API, the value is `2025-04-01`. |


#{.custom\-md\-table\-5}#

<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppID |String |Yes |`123456` |Application ID. |
|Platform |String |Yes |`mobile` |Device type. Options are:<br><br><br>* `mobile`: Mobile device.<br><br>* `web`: Web browser. |
|StartTime |String |Yes |`2024-08-29T04:46:22Z` |The start time. Follows the RFC3339 format for UTC time with second precision, formatted as `yyyy-MM-ddTHH:mm:ssZ`. |
|EndTime |String |Yes |`2025-03-01T10:00:00Z` |The end time. Follows the RFC3339 format for UTC time with second precision, formatted as `yyyy-MM-ddTHH:mm:ssZ`. |
|Granularity |Integer |No |`300` |Aggregation time granularity (in seconds). The API uses the `Granularity` to divide the statistical time period represented by `StartTime` and `EndTime` into a series of time intervals, then aggregates data for each interval. Options are:<br><br><br>* `0` (default): No time aggregation.<br><br>* `300`: 5 minutes.<br><br>* `3600`: 1 hour.<br><br>* `86400`: 1 day. |
|Metrics |Array of String |Yes |`["cnt"]` |the list of metrics. Options are:<br><br><br>* `cnt`: Video views (VV)<br><br>* `vplay_actual_cnt`: Actual video views<br><br>* `fail_rate`: Unsuccessful playback rate<br><br>* `firstframe_duration_avg`: Time to first frame (TTFF)<br><br>* `buffer_rate`: Video freeze rate<br><br>* `broken_rate`: Interruption rate<br><br>* `leave_without_play_rate`: No play rate<br><br>* `buf_time_per_100_sec_avg`: Video freezes duration within 100 seconds<br><br>* `video_bsp_avg`: Average playback bitrate<br><br>* `vplay_finish_cnt`: Number of finished playbacks<br><br>* `uv`: Number of daily active users (DAU)<br><br>* `vplay_finish_rate`: Finished playback rate<br><br>* `vv_duration_avg`: Video watching time per user<br><br>* `vv_avg`: Number of playbacks per user<br><br>* `finish_vv_avg`: Number of finished playbacks per user<br><br>* `watch_dur_avg`: Average playback duration<br><br>* `video_dur_avg`: Average video duration<br><br>* `player_bw`: Bandwidth usage of Player SDK<br><br>* `player_stream_data`: Traffic of the Player SDK<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-dimensions-and-metrics#metrics">Metrics</a> for more information.</div><br> |
|Dimensions |Array of String |No |`["os"]` |Dimension list, a maximum of 3 dimensions can be added. Options are:<br><br><br>* `os`: Operating system<br><br>* `tag`: Business tag<br><br>* `subtag`: Business subtag<br><br>* `app_version`: App version<br><br>* `sdk_version`: Player SDK version<br><br>* `codec`: Video codec<br><br>* `os_version`: Operating system with version<br><br>* `source_type`: Playback method<br><br>* `vtype`: Video container format<br><br>* `is_hw`: Hardware decoding<br><br>* `video_definition`: Video resolution<br><br>* `network`: Network<br><br>* `cdn_name`: CDN vendor<br><br>* `carrier`: Network operator<br><br>* `province`: Province<br><br>* `country`: Country<br><br>* `domain`: Domain name<br><br>* `app_channel`: Distribution channel<br><br>* `error_code_display`: Error code of the Player SDK<br><br>* `video_id`: The video ID<br><br>* `user_unique_id`: UUID<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-dimensions-and-metrics#dimensions">Dimensions</a> for more information.</div><br> |
|Filter |Object of [Filter](https://docs.byteplus.com/en/docs/25/46986#filter) |No |`-` |Filter configuration. |


#{.custom\-md\-table\-5}#

<span id="filter"></span>
### Filter


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Logic |String |No |`and` |Logical operators. Options are:<br><br><br>* `and`<br><br>* `or` |
|Filters |Array of [Filters](https://docs.byteplus.com/en/docs/25/46986#filters) |No |`-` |Sub\-filter configuration. |
|Field |String |Yes |`os` |Dimension list. Options are:<br><br><br>* `os`: Operating system<br><br>* `tag`: Business tag<br><br>* `subtag`: Business subtag<br><br>* `app_version`: App version<br><br>* `sdk_version`: Player SDK version<br><br>* `codec`: Video codec<br><br>* `os_version`: Operating system with version<br><br>* `source_type`: Playback method<br><br>* `vtype`: Video container format<br><br>* `is_hw`: Hardware decoding<br><br>* `video_definition`: Video resolution<br><br>* `network`: Network<br><br>* `cdn_name`: CDN vendor<br><br>* `carrier`: Network operator<br><br>* `province`: Province<br><br>* `country`: Country<br><br>* `domain`: Domain name<br><br>* `app_channel`: Distribution channel<br><br>* `error_code_display`: Error code of the Player SDK<br><br>* `video_id`: The video ID<br><br>* `user_unique_id`: The unique user id (UUID)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-dimensions-and-metrics#dimensions">Dimensions</a> for more information.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <code>platform</code> is <code>web</code>, <code>Field</code> cannot be set to <code>user_unique_id</code>.</div><br> |
|Op |String |Yes |`in` |Operators. Options are:<br><br><br>* `>`: Greater than<br><br>* `<`: Less than<br><br>* `>=`: Greater than or equal to<br><br>* `<=`: Less than or equal to<br><br>* `=`: Equal to<br><br>* `!=`: Not equal to<br><br>* `in`: Contains<br><br>* `not in`: Does not contain |
|Values |Array of String |Yes |`["Android"]` |Comparison value corresponding to the `Field`. For example, when `Field` is `os`, `Values` can be set to `Android` or `iOS`. Length must not exceed 100 characters. |


#{.custom\-md\-table\-5}#

<span id="filters"></span>
### Filters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Field |String |Yes |`os` |Dimension list. Options are:<br><br><br>* `os`: Operating system<br><br>* `tag`: Business tag<br><br>* `subtag`: Business subtag<br><br>* `app_version`: App version<br><br>* `sdk_version`: Player SDK version<br><br>* `codec`: Video codec<br><br>* `os_version`: Operating system with version<br><br>* `source_type`: Playback method<br><br>* `vtype`: Video container format<br><br>* `is_hw`: Hardware decoding<br><br>* `video_definition`: Video resolution<br><br>* `network`: Network<br><br>* `cdn_name`: CDN vendor<br><br>* `carrier`: Network operator<br><br>* `province`: Province<br><br>* `country`: Country<br><br>* `domain`: Domain name<br><br>* `app_channel`: Distribution channel<br><br>* `error_code_display`: Error code of the Player SDK<br><br>* `video_id`: The video ID<br><br>* `user_unique_id`: The unique user id (UUID)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">See <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-dimensions-and-metrics#dimensions">Dimensions</a> for more information.</div><br> |
|Op |String |Yes |`in` |Operators. Options are:<br><br><br>* `>`: Greater than<br><br>* `<`: Less than<br><br>* `>=`: Greater than or equal to<br><br>* `<=`: Less than or equal to<br><br>* `=`: Equal to<br><br>* `!=`: Not equal to<br><br>* `in`: Contains<br><br>* `not in`: Does not contain |
|Values |Array of String |Yes |`["Android"]` |Comparison value corresponding to the `Field`. For example, when `Field` is `os`, `Values` can be set to `Android` or `iOS`. Length must not exceed 100 characters. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TotalPoint |Float |`1` |Total point number. |
|Columns |Array of [Columns](https://docs.byteplus.com/en/docs/25/46986#columns) |`-` |Field information. |
|Data |Array of JSON Map |`-` |Detailed data, including metrics and dimensions. If the aggregation granularity is not 0, a time field will also be included. |


#{.custom\-md\-table\-4}#

<span id="columns"></span>
### Columns


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`os` |Field name. |
|Alias |String |`Operating system` |Field alias. |
|Type |String |`Count` |Data types. Options are:<br><br><br>* `String`: Dimension, unitless<br><br>* `Count`: Number of items<br><br>* `Percent`: Percentage<br><br>* `Time`: Duration<br><br>* `bps`: Bandwidth<br><br>* `Bytes`: Data volume |
|ValueAlias |String |`-` |Value alias. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://vod.byteplusapi.com?Action=GetVodMediaPlayData&Version=2025-04-01
{
    "Metrics": [
        "cnt"
    ],
    "StartTime": "2025-05-12T00:00:00Z",
    "EndTime": "2025-05-12T23:59:59Z",
    "Filter": {
        "Logic": "and",
        "Filters": [
            {
                "Field": "os",
                "Op": "=",
                "Values": [
                    "iOS"
                ]
            },
            {
                "Field": "app_version",
                "Op": ">",
                "Values": [
                    "10000.0.22"
                ]
            }
        ]
    },
    "Granularity": 3600,
    "AppID": "10085495",
    "Platform": "mobile",
    "Dimensions": [
        "app_version"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202505122044447530E6A9E8EAF4F8AFEC",
        "Action": "GetVodMediaPlayData",
        "Version": "2025-04-01",
        "Service": "vod",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Columns": [
            {
                "Name": "vqos_datetime",
                "Alias": "日期",
                "Type": "string"
            },
            {
                "Name": "app_version",
                "Alias": "App version",
                "Type": "string"
            },
            {
                "Name": "cnt",
                "Alias": "Video views (VV)",
                "Type": "count"
            }
        ],
        "Data": [
            {
                "app_version": "10000.0.23",
                "cnt": 2,
                "vqos_datetime": "2025-05-12T07:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 3,
                "vqos_datetime": "2025-05-11T18:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 16,
                "vqos_datetime": "2025-05-11T21:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 40,
                "vqos_datetime": "2025-05-12T01:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 89,
                "vqos_datetime": "2025-05-11T17:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 6,
                "vqos_datetime": "2025-05-11T20:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 76,
                "vqos_datetime": "2025-05-12T03:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 2,
                "vqos_datetime": "2025-05-11T16:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 112,
                "vqos_datetime": "2025-05-12T04:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 25,
                "vqos_datetime": "2025-05-12T05:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 7,
                "vqos_datetime": "2025-05-12T00:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 8,
                "vqos_datetime": "2025-05-11T23:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 11,
                "vqos_datetime": "2025-05-12T02:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 20,
                "vqos_datetime": "2025-05-11T22:00:00Z"
            },
            {
                "app_version": "10000.0.23",
                "cnt": 18,
                "vqos_datetime": "2025-05-12T06:00:00Z"
            }
        ],
        "TotalPoint": 15
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidReqBody |Invalid request body: %s |Invalid request content |
|400 |ErrStartGreaterThanEndTime |The end time should be greater than the start time |End time must be greater than start time |
|400 |ErrTimeSpanBeyondLimit |The time span is beyond the limit |Time range exceeded |
|400 |ErrInvalidOs |Invalid os |Invalid system parameters |
|404 |MetricNotExist |Metric '%s' cannot be found. |Metric does not exist |
|403 |AppIDNoAuth |Unauthorized appid |Insufficient application permissions |
|500 |ServiceFailure |The request processing has failed because of an unknown error |Server error |
|404 |DimensionNotExist |Dimension: '%s' cannot be found. |Dimension does not exist |
|404 |GranularityConflict |metric '%s' and dimension '%s' cannot be both found in granularity(%ds), switch to other granularity or other combined condition. |Metric and dimension do not coexist at the specified granularity; try a different granularity or combination of conditions |
|404 |GranularityConflictSingle |metric or dimension '%s' cannot be found in granularity(%ds), switch to other granularity and try again. |Metric or dimension does not exist at the specified granularity; try a different query granularity |


#{.custom\-md\-table\-4}#

&nbsp;
