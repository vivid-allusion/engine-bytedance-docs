---
title: "DescribeCdnIP"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnIP_En"
---

Query whether one or more specified IP addresses are the IP addresses of CDN nodes. CDN nodes include edge nodes and regional nodes.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCdnIP`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|IPs |String[] |Yes |Indicates the list of IP addresses to be queried. The list can contain up to 50 IP addresses. |`["xx.xxx.xxx.102", "xxx.xxx.234.67"]` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|IPs |Object[] |Indicates the list of IP addresses in the request parameters. | |
|IP |String |Indicates an IP address in the IP address list. |`xx.xxx.xxx.102` |
|CdnIp |Boolean |Indicates whether the IP address is the IP address of a CDN edge node. This parameter has the following values:<br><br><br>* `true`: Indicates that the IP address is the IP address of a CDN edge node.<br><br>* `false`: Indicates that the IP address is not the IP address of a CDN edge node. |`false` |
|ISP |String |Indicates the ISP to which the IP address belongs.<br><br><br>* If `CdnIp` is `false`, this parameter value is empty ("").<br><br>* If `CdnIp` is `true` but the CDN has not obtained the ISP to which the IP address belongs, this parameter value is `DEFAULT`. |`DEFAULT` |
|Location |String |Indicates the country or region to which the IP address belongs. If `CdnIp` is `false`, this parameter value is empty (""). |`United States-Florida-Florida` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnIP&Version=2021-03-01
{
    "IPs": [
        "xxx.xxx.xx.139",
        "xxx.xx.xx.34"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024101011033668CF51ECED9C5477E3C6",
        "Action": "DescribeCdnIP",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "IPs": [
            {
                "CdnIp": true,
                "IP": "xxx.xxx.xx.139",
                "ISP": "DEFAULT",
                "Location": "Singapore-Singapore-Singapore"
            },
            {
                "CdnIp": false,
                "IP": "xxx.xx.xx.34",
                "ISP": "",
                "Location": ""
            }
        ]
    }
}
```


&nbsp;
