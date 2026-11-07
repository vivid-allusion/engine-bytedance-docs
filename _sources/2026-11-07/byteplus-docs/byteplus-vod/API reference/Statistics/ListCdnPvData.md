---
title: "ListCdnPvData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listcdnpvdata"
---

This interface is used to set parameters such as the domain name and the category of statistical data. Within a specified time range, it retrieves the requested number of data.

<span id="requirements"></span>
## Requirements

Time Range: The time span of the query should not exceed **90 days**.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListCdnPvData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCdnPvData` |The API action. For the current API, the value is `ListCdnPvData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Domains |String |Yes |`example.vod.com` |Domains, separated by commas `,`. You can obtain the list of domains in a specific space via the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface. |
|Interval |String |Yes |`auto` |Specify the time granularity for querying data, unit: seconds. The values are as follows:<br><br><br>* `auto`: Automatically aggregate.<br><br>* `5min`: 5\-minute granularity.<br><br>* `hour`: 1\-hour granularity.<br><br>* `day`: Daily granularity. |
|StartTimestamp |Long |No |`1703519999` |The query range start time. Unix timestamp in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. Default is at midnight of the current day. |
|EndTimestamp |Long |No |`1703433600` |The query range end time. Unix timestamp in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. The default is 0:00 AM the next day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum data period supported for a single query is 90 days.</div><br> |
|DataType |String |Yes |`edge` |The category of statistical data. The values are as follows:<br><br><br>* `edge`: The statistics of edge data.<br><br>* `origin`: The statistics of origin data. |
|NeedDetail |Boolean |No |`true` |Do you need detailed data by domain? The values are as follows:<br><br><br>* `false`: (default) No.<br><br>* `true`: Yes. |
|TimeZone |String |No |`Etc/GMT+8` |The time zone. Supported values are as follows: `Etc/GMT`, `Etc/GMT-1`, `Etc/GMT-2`, `Etc/GMT-3`, `Etc/GMT-4`, `Etc/GMT-5`, `Etc/GMT-6`, `Etc/GMT-7`, `Etc/GMT-8`, `Etc/GMT-9`, `Etc/GMT-10`, `Etc/GMT-11`, `Etc/GMT-12`, `Etc/GMT+1`, `Etc/GMT+2`, `Etc/GMT+3`, `Etc/GMT+4`, `Etc/GMT+5`, `Etc/GMT+6`, `Etc/GMT+7`, `Etc/GMT+8`, `Etc/GMT+9`, `Etc/GMT+10`, `Etc/GMT+11`, `Etc/GMT+12`. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Datas |Array of [VodCdnStatisticsData](https://docs.byteplus.com/en/docs/25/8059#vodcdnstatisticsdata) |`-` |The usage information. |
|NoPermissionDomains |Array of String |`["example.vod.com"]` |The unauthorized domain list. |


#{.custom\-md\-table\-4}#

<span id="vodcdnstatisticsdata"></span>
### VodCdnStatisticsData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`total` |The statistical target name. |
|Metric |String |`pv` |The category of indicators, value is `pv`. |
|DataType |String |`origin` |Statistical categories. The values are as follows:<br><br><br>* `edge`: The edge data statistics.<br><br>* `origin`: The origin data statistics. |
|Points |Array of [VodPoint](https://docs.byteplus.com/en/docs/25/8059#vodpoint) |`-` |The data points. |


#{.custom\-md\-table\-4}#

<span id="vodpoint"></span>
### VodPoint


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Timestamp |Double |`1653494400` |The timestamp. |
|Value |Double |`458700098.3547` |Numerical value, measured in occurrences.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter may not be present.</div><br> |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListCdnPvData&Version=2023-01-01&Domains=example.vod.com&Interval=auto&StartTimestamp=1703519999&EndTimestamp=1703433600&DataType=edge&NeedDetail=true
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022052615313***620412B5A92D",
        "Action": "ListCdnPvData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "Datas": [
            {
                "Name": "total",
                "Metric": "pv",
                "DataType": "origin",
                "Points": [
                    {
                        "Timestamp": 1653494400,
                        "Value": 458700098.3547
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
