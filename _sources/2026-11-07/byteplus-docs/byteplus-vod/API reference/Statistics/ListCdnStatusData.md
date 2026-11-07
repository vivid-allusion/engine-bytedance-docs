---
title: "ListCdnStatusData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listcdnstatusdata"
---

This interface is used for setting parameters such as the domain name, the data category, and the metric category. Within a certain time range, it retrieves the specified status code data statistics.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListCdnStatusData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCdnStatusData` |The API action. For the current API, the value is `ListCdnStatusData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Domains |String |Yes |`example.vod.com` |Domains, separated by commas `,`. You can obtain the list of domains under a specific space via the [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface. |
|Interval |String |Yes |`auto` |Specify the time granularity for querying data, unit: seconds. The supported values are as follows:<br><br><br>* `auto`: Automatically aggregate.<br><br>* `5min`: 5\-minute granularity.<br><br>* `hour`: 1\-hour granularity.<br><br>* `day`: Daily granularity. |
|StartTimestamp |Long |No |`1702828800` |The query range start time. Unix timestamp, in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. Default is today at 00:00. |
|EndTimestamp |Long |No |`1703519999` |The query range end time. Unix timestamp in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. The default is 0:00 the next day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum supported data retrieval is for 90 days per query.</div><br> |
|DataType |String |Yes |`edge` |Statistical data categories. The values are as follows:<br><br><br>* `edge`: The edge data statistics.<br><br>* `origin`: The origin data statistics. |
|Metric |String |Yes |`status_total` |The category of metrics. The supported values are as follows:<br><br><br>* `status_total`: Overview.<br><br>* `2xx`: Details of 2xx data.<br><br>* `3xx`: Details of 3xx data.<br><br>* `4xx`: Details of 4xx data.<br><br>* `5xx`: Details of 5xx data. |
|NeedDetail |Boolean |No |`false` |Whether need detailed data or not. The values are as follows:<br><br><br>* `false`: (default) No.<br><br>* `true`: Yes. |
|TimeZone |String |No |`Etc/GMT+8` |The time zone. Supported values are as follows: `Etc/GMT`, `Etc/GMT-1`, `Etc/GMT-2`, `Etc/GMT-3`, `Etc/GMT-4`, `Etc/GMT-5`, `Etc/GMT-6`, `Etc/GMT-7`, `Etc/GMT-8`, `Etc/GMT-9`, `Etc/GMT-10`, `Etc/GMT-11`, `Etc/GMT-12`, `Etc/GMT+1`, `Etc/GMT+2`, `Etc/GMT+3`, `Etc/GMT+4`, `Etc/GMT+5`, `Etc/GMT+6`, `Etc/GMT+7`, `Etc/GMT+8`, `Etc/GMT+9`, `Etc/GMT+10`, `Etc/GMT+11`, `Etc/GMT+12`. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Datas |Array of [VodCdnStatisticsData](https://docs.byteplus.com/en/docs/25/8060#vodcdnstatisticsdata) |`-` |The usage information. |
|NoPermissionDomains |Array of String |`["example.vod.com"]` |The unauthorized domain list. |


#{.custom\-md\-table\-4}#

<span id="vodcdnstatisticsdata"></span>
### VodCdnStatisticsData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`total` |The statistical target name. |
|Metric |String |`bandwidth` |The category of indicators. |
|DataType |String |`origin` |Statistical categories. The values are as follows:<br><br><br>* `edge`: The edge data statistics.<br><br>* `origin`: The origin data statistics. |
|Points |Array of [VodPoint](https://docs.byteplus.com/en/docs/25/8060#vodpoint) |`-` |The data points. |


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
https://vod.byteplusapi.com?Action=ListCdnStatusData&Version=2023-01-01&Domains=example.vod.com&Interval=auto&StartTimestamp=1702828800&EndTimestamp=1703519999&DataType=edge&Metric=status_total&NeedDetail=false
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2022052615****0807422501B3C82E",
        "Action": "ListCdnStatusData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "Datas": [
            {
                "Name": "total",
                "Metric": "2xx",
                "DataType": "edge",
                "Points": [
                    {
                        "Timestamp": 1653494400,
                        "Value": 681353
                    }
                ]
            },
            {
                "Name": "total",
                "Metric": "3xx",
                "DataType": "edge",
                "Points": [
                    {
                        "Timestamp": 1653494400,
                        "Value": 182
                    }
                ]
            },
            {
                "Name": "total",
                "Metric": "4xx",
                "DataType": "edge",
                "Points": [
                    {
                        "Timestamp": 1653494400,
                        "Value": 39182
                    }
                ]
            },
            {
                "Name": "total",
                "Metric": "5xx",
                "DataType": "edge",
                "Points": [
                    {
                        "Timestamp": 1653494400
                    }
                ]
            },
            {
                "Name": "total",
                "Metric": "total",
                "DataType": "edge",
                "Points": [
                    {
                        "Timestamp": 1653494400,
                        "Value": 720717
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
