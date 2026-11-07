---
title: "ListCdnTopAccess"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listcdntopaccess"
---

Call `ListCdnTopAccess` to get hot data and request count for specified domain names within a given time period.

<span id="usage-scenario"></span>
## Usage scenario

This interface performs statistics on the following fields in user requests:


* URL: Obtain the TOP 1,000 request URLs by traffic or request count.

* Referer: Obtain the TOP 1,000 request Referers by traffic or request count.

* Client IP: Obtain the TOP 1,000 client IPs by traffic or request count.


The minimum time granularity for statistics is **1 hour**. The system selects a time range greater than or equal to `StartTime` and less than or equal to `EndTime`, using one\-hour increments as data points to sort and statisticize the fields. Examples are as follows:


* `StartTime` is `2022-01-14 03:00:00` and `EndTime` is `2022-01-14 04:00:00`: Data is sorted based on the aggregate statistics of the two time periods: 03:00:00 \- 04:00:00 and 04:00:00 \- 05:00:00.

* `StartTime` is `2022-01-14 03:20:00` and `EndTime` is `2022-01-14 04:20:00`: Data is sorted based on the statistics of the 04:00:00 \- 05:00:00 time period.

* `StartTime` is `2022-01-14 03:20:00` and `EndTime` is `2022-01-14 05:00:00`: Data is sorted based on the aggregate statistics of the 04:00:00 \- 05:00:00 and 05:00:00 \- 06:00:00 time periods.

* `StartTime` is `2022-01-14 03:00:00` and `EndTime` is `2022-01-14 04:20:00`: Data is sorted based on the aggregate statistics of the 03:00:00 \- 04:00:00 and 04:00:00 \- 05:00:00 time periods.


<span id="requirements"></span>
## Requirements


* Data Stability: Monitoring data statistics may fluctuate due to network variations at edge nodes. In most cases, statistics will stabilize within 12 hours after the data is generated.

* Data Latency: Hot data statistics are based on hourly granularity indicators. Therefore, there may be a delay of approximately 2 hours. For example, accurate results for the 09:00 to 10:00 period can typically be retrieved around 11:00.

* You can query data for up to the past 92 days.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListCdnTopAccess&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCdnTopAccess` |The API action. For the current API, the value is `ListCdnTopAccess`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|Domains |String |Yes |`example.com` |The domain name. You can obtain the domain list for a specific space through [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only a single domain is supported.</div><br> |
|StartTimestamp |Integer |No |`1672531200` |The start timestamp for querying, in Unix seconds. Defaults to `00:00:00` of the current day. |
|EndTimestamp |Integer |No |`1672617600` |The end timestamp for querying, in Unix seconds. Defaults to `23:59:59` of the current day. |
|SortType |String |No |`pv` |The statistical metric used for sorting `Item`. Supported values are as follows:<br><br><br>* `flux`: Sort by traffic;<br><br>* `pv`: (Default) Sort by request count (access volume). |
|Item |String |No |`url` |The statistical field. Supported values are as follows:<br><br><br>* `url`: (Default) Refers to the request URL;<br><br>* `referer`: Refers to the request Referer.<br><br>* `clientip`: Refers to the client IP. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ItemInfos |Array of [VodCdnTopAccessElement](https://docs.byteplus.com/en/docs/25/95087#vodcdntopaccesselement) |`-` |The information list of hot data statistics. |


#{.custom\-md\-table\-4}#

<span id="vodcdntopaccesselement"></span>
### VodCdnTopAccessElement


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Value |Double |`59` |The corresponding values retrieved from the statistical fields and statistical method. |
|ItemKey |String |`example.com` |The key corresponding to the `Item` parameter. Possible values are:<br><br><br>* When `Item` is `url`, this value represents the request URL.<br><br>* When `Item` is `referer`, this value represents the request Referer.<br><br>* When `Item` is `clientip`, this value represents the client IP. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListCdnTopAccess&Version=2023-07-01&Domains=example.com&StartTimestamp=1672531200&EndTimestamp=1672617600&SortType=pv&Item=url
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104****100232280022D31",
        "Action": "ListCdnTopAccess",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "ItemInfos": [
            {
                "ItemKey": "www.example.vod.com",
                "Value": 59
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).
