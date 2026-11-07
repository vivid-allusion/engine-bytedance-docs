---
title: "DescribeIpInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describeipinfo"
---

Call this API to query whether the specified one or more IP addresses belong to a node within the BytePlus CDN network.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DescribeIpInfo&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeIpInfo` |The API action. For the current API, the value is `DescribeIpInfo`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Ips |String |Yes |`1.1.1.1` |The list of IP addresses. Separate multiple IP addresses with a newline or a comma. Supports up to 50 IP addresses. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Ip |String |`1.1.1.1` |The IP address. |
|Isp |String |`Telecommunications` |The ISP (Internet Service Provider) to which the IP address belongs. Currently, this API only supports returning ISPs in the Chinese Mainland.<br><br><br>* If `CdnIp` is `false`, the value of this parameter is `"-"`.<br><br>* If `CdnIp` is `true` and `Location` does not in the Chinese Mainland, the value of this parameter is invalid. |
|CdnIp |Boolean |`true` |Whether the IP address is associated with the BytePlus CDN service. The possible values are:<br><br><br>* `true`: The IP address belongs to a node within the BytePlus CDN network.<br><br>* `false`: The IP address does not belong to the BytePlus CDN network. |
|Location |String |`China - Shandong Province - Qingdao City` |The country or region to which the IP address belongs. If `CdnIp` is `false`, the value of this parameter is `"-"`.<br><br>For IP addresses that are located in the Chinese Mainland:<br><br><br>* If the city of the location is a municipality, `Location` is displayed at the district level.<br><br>* If the city of the location is not a municipality, `Location` is displayed at the city level. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DescribeIpInfo&Version=2023-01-01&Ips=1.1.1.1
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": [
        {
            "Ip": "1.1.1.1",
            "Isp": "Telecommunications",
            "CdnIp": true,
            "Location": "China - Shandong Province - Qingdao City"
        }
    ],
    "ResponseMetadata": {
        "Action": "DescribeIpInfo",
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
