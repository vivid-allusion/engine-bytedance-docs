---
title: "ListCdnAccessLog"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listcdnaccesslog"
---

BytePlus VOD supports querying and downloading CDN original access logs for specified domains. This interface is used to obtain the log file download URL in the specified space.

<span id="requirements"></span>
## Requirements


* Log field: For details, please refer to [Logs](https://docs.byteplus.com/en/docs/byteplus-vod/docs-logs).

* Log package latency: Under normal circumstances, the delay is within 3 hours, and it may exceed 12 hours during peak business hours.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListCdnAccessLog&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCdnAccessLog` |The API action. For the current API, the value is `ListCdnAccessLog`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Domains |String |Yes |`example.vod.com` |The domain name. You can obtain the list of space domain names by calling the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, only one domain name is supported.</div><br> |
|StartTimestamp |Integer |No |`1703433600` |The query range start time. Unix timestamp in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supports querying logs from the past 30 days.</div><br> |
|EndTimestamp |Integer |No |`1703519940` |The query range end time. Unix timestamp in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. |
|SpaceName |String |Yes |`test` |The name of the on\-demand space. The space name can be obtained in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD console [Spaces](https://console.byteplus.com/vodpaas/overview/?).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Logs |Array of [CdnAccessLogInfo](https://docs.byteplus.com/en/docs/25/8069#cdnaccessloginfo) |`-` |The log list. |


#{.custom\-md\-table\-4}#

<span id="cdnaccessloginfo"></span>
### CdnAccessLogInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`example.vod.com` |The domain name. |
|LogList |Array of [CdnAccessLogElement](https://docs.byteplus.com/en/docs/25/8069#cdnaccesslogelement) |`-` |The log list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If there are no logs, this field does not exist.</div><br> |


#{.custom\-md\-table\-4}#

<span id="cdnaccesslogelement"></span>
### CdnAccessLogElement


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DownloadUrl |String |`https://cdnlog.bytedance.com/cdn-openapi/userlog/file-download/v1?fileName=video01.ethanle******0492d40c7b3` |The download URL. |
|FileSize |Long |`208` |The file size, in bytes. |
|FileName |String |`video01.ethanle***410120000_20220410130000.gz` |The log file name. |
|StartTimestamp |Integer |`1649563200` |The log data start time in the log package, Unix timestamp. |
|EndTimestamp |Integer |`1649566800` |The end time of the log data in the log package, Unix timestamp. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListCdnAccessLog&Version=2023-01-01&Domains=example.vod.com&StartTimestamp=1703433600&EndTimestamp=1703519940&SpaceName=test
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "Logs": [
            {
                "Domain": "example.vod.com",
                "LogList": [
                    {
                        "FileName": "video01.ethanle***410120000_20220410130000.gz",
                        "FileSize": 208,
                        "DownloadUrl": "https://cdnlog.bytedance.com/cdn-openapi/userlog/file-download/v1?fileName=video01.ethanle******0492d40c7b3",
                        "EndTimestamp": 1649566800,
                        "StartTimestamp": 1649563200
                    }
                ]
            }
        ]
    },
    "ResponseMetadata": {
        "Action": "ListCdnAccessLog",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
