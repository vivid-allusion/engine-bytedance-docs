---
title: "ListCdnUsageData"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listcdnusagedata"
---

This interface is used to set parameters such as the domain name, the category of statistics, the category of metrics, etc. Within a specified time range, it retrieves the designated bandwidth traffic data.

<span id="usage-scenario"></span>
## Usage scenario


* If you do not specify `StartTimestamp` and `EndTimestamp`, this interface returns data for the current day (0:00\-24:00).

* If you specify `StartTimestamp` and `EndTimestamp`, this interface returns data for the specified time period.


<span id="requirements"></span>
## Requirements


* Rate limit: The request rate limit for a single user is **10 times/second**.

* Data Latency: **5 minutes**.

* Time Range: The time span for queries should not exceed **90 days**.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListCdnUsageData&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCdnUsageData` |The API action. For the current API, the value is `ListCdnUsageData`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Domains |String |Yes |`example.vod.com` |The domain names, separated by English commas. You can obtain the list of domain names under a specific space via [ListDomain](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listdomain) interface. |
|Interval |String |Yes |`auto` |Specify the time granularity for querying data, with the unit in seconds. The values are as follows:<br><br><br>* `auto`: Automatic aggregation.<br><br>* `5min`: 5\-minute granularity.<br><br>* `hour`: 1\-hour granularity.<br><br>* `day`: Daily granularity. |
|StartTimestamp |Long |No |`1687276800` |The query range start time. Unix timestamp, in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. The default is today at 00:00. |
|EndTimestamp |Long |No |`1687967999` |The query range end time. Unix timestamp in seconds. It represents the number of seconds from January 1, 1970, 00:00:00 UTC to the specified time. The default is 0:00 the next day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum data retrieval is supported for up to 90 days per query.</div><br> |
|DataType |String |Yes |`edge` |Statistical Data Categories. The values are as follows:<br><br><br>* `edge`: The edge data statistics.<br><br>* `origin`: The origin data statistics. |
|Metric |String |Yes |`bandwidth` |The category of metrics. The values are as follows:<br><br><br>* `bandwidth`: The bandwidth perspective.<br><br>* `flux`: The traffic perspective. |
|NeedDetail |Boolean |No |`true` |Do you need to return detailed data for subdomains? The values are as follows:<br><br><br>* `false`: (default) No.<br><br>* `true`: Yes. |
|Area |String |No |`China` |Access area. Default is empty. Values are as follows:<br><br><br>* `China`: Mainland China.<br><br>* `Global`: Worldwide.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Area</code> parameter is only effective when the <code>DataType</code> parameter is set to <code>edge</code>.</div><br> |
|Region |String |No |`BJ` |Country or region code. Statistics on the detailed access data attributed to that area. You can obtain the country, region, and province codes through [Countries, provinces, and ISPs](https://docs.byteplus.com/en/docs/byteplus-vod/reference-countries-provinces-and-isps). The default is all data; multiple countries or regions are separated by `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Region</code> parameter is only effective when the <code>DataType</code> parameter is set to <code>edge</code>.</div><br> |
|Isp |String |No |`CT` |The user operator. You can obtain the operator data through [Countries, provinces, and ISPs](https://docs.byteplus.com/en/docs/byteplus-vod/reference-countries-provinces-and-isps). The default is all data; multiple operators are separated by `,`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>Isp</code> parameter is only effective when the <code>DataType</code> parameter is set to <code>edge</code>.</div><br> |
|Protocol |String |No |`https` |The application protocol. The values are as follows:<br><br><br>* `http`: HTTP.<br><br>* `https`: HTTPS.<br><br>* `quic`: QUIC.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>Protocol</code> parameter is effective only when the <code>DataType</code> parameter is set to <code>edge</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting multiple values is not supported; by default, it is set to all if not specified.</div><br> |
|IpVersion |String |No |`ipv4` |The Network Layer Protocol. The values are as follows:<br><br><br>* `ipv4`: IPv4.<br><br>* `ipv6`: IPv6.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The <code>IpVersion</code> parameter is effective only when the <code>DataType</code> parameter is set to <code>edge</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Setting multiple values is not supported; by default, it is set to all if not specified.</div><br> |
|BillingRegion |String |No |`CHN` |The billing region. It defaults to an empty value. When this parameter is empty, it will return the summary data for all billing regions. The values are as follows:<br><br><br>* `CHN`: Mainland China<br><br>* `EU`: Europe<br><br>* `NA`: North America<br><br>* `SA`: South America<br><br>* `MEA`: Middle East and Africa<br><br>* `AP1`: Asia Pacific Region 1<br><br>* `AP2`: Asia Pacific Region 2<br><br>* `AP3`: Asia Pacific Region 3<br><br>* `All`: Statistics for access data are calculated separately for each billing region.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details on the countries and regions included in Asia Pacific Region 1, 2, and 3, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-vod/docs-pay-as-you-go-pricing#content-acceleration">Pay\-as\-you\-go pricing:</a>.</div><br> |
|TimeZone |String |No |`Etc/GMT+8` |The time zone. Supported values are as follows: `Etc/GMT`, `Etc/GMT-1`, `Etc/GMT-2`, `Etc/GMT-3`, `Etc/GMT-4`, `Etc/GMT-5`, `Etc/GMT-6`, `Etc/GMT-7`, `Etc/GMT-8`, `Etc/GMT-9`, `Etc/GMT-10`, `Etc/GMT-11`, `Etc/GMT-12`, `Etc/GMT+1`, `Etc/GMT+2`, `Etc/GMT+3`, `Etc/GMT+4`, `Etc/GMT+5`, `Etc/GMT+6`, `Etc/GMT+7`, `Etc/GMT+8`, `Etc/GMT+9`, `Etc/GMT+10`, `Etc/GMT+11`, `Etc/GMT+12`. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Datas |Array of [VodCdnStatisticsData](https://docs.byteplus.com/en/docs/25/8058#vodcdnstatisticsdata) |`-` |The usage information. |
|NoPermissionDomains |Array of String |`["example.vod.com"]` |The unauthorized domain list. |


#{.custom\-md\-table\-4}#

<span id="vodcdnstatisticsdata"></span>
### VodCdnStatisticsData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`total` |The statistical target name. |
|Metric |String |`bandwidth` |The category of indicators. |
|DataType |String |`origin` |Statistical categories. The values are as follows:<br><br><br>* `edge`: The edge data statistics.<br><br>* `origin`: The origin data statistics. |
|Points |Array of [VodPoint](https://docs.byteplus.com/en/docs/25/8058#vodpoint) |`-` |The data points. |


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
https://vod.byteplusapi.com?Action=ListCdnUsageData&Version=2023-01-01&Domains=example.vod.com&Interval=auto&StartTimestamp=1687276800&EndTimestamp=1687967999&DataType=edge&Metric=bandwidth&NeedDetail=true&Area=China&Region=BJ&Isp=CT&Protocol=https&IpVersion=ipv4&BillingRegion=CHN
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202205261531390***05620412B5A92D",
        "Action": "ListCdnUsageData",
        "Version": "2023-01-01",
        "Service": "vod"
    },
    "Result": {
        "Datas": [
            {
                "Name": "total",
                "Metric": "bandwidth",
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
