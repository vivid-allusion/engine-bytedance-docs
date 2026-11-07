---
title: "DescribeCdnRegionAndIsp"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en"
---

Get the names and codes of Chinese provincial administrative regions, global countries and regions, and Chinese Internet Service Providers (ISPs) covered by the BytePlus IP address database.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCdnRegionAndIsp`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Area |String |No |Indicates the scope of the query. This parameter has the following values:<br><br><br>* `China`: refers to the codes and names of Chinese provincial administrative regions and Chinese ISPs.<br><br>* `Global`: refers to the codes and names of countries and regions, as well as Chinese ISPs.<br><br><br>The default value of this parameter is `china`. |`Global` |
|Lang |String |No |Indicates the language in which query results are displayed. This parameter has the following values:<br><br><br>* `zh`: refers to Simplified Chinese.<br><br>* `en`: refers to English.<br><br><br>The default value of this parameter is `en`. |`en` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Isps |Object[] |Indicates a list of Chinese ISPs. | |
|Code |String |Indicates a code representing a Chinese ISP. |`CU` |
|Name |String |Indicates the name of the Chinese ISP. |`China Unicom` |
|Regions |Object[] |Indicates a list of areas.<br><br><br>* If `Area` is `Global`, this parameter indicates a list of countries and regions.<br><br>* If `Area` is `China`, this parameter indicates a list of China's provincial administrative regions in China. | |
|Code |String |Indicates a code representing a country, region, or China's provincial administrative region. |`BJ` |
|Name |String |Indicates the name of the country, region, or China's provincial administrative region. |`Beijing` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021-03-01
{
    "Area": "Global"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423061106DA1BD20A355B07CBEC2D",
        "Action": "DescribeCdnRegionAndIsp",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Isps": [
            {
                "Code": "CT",
                "Name": "China Telecom"
            },
            {
                "Code": "CM",
                "Name": "China Mobile"
            },
            {
                "Code": "CU",
                "Name": "China Unicom"
            },
            {
                "Code": "GWBN",
                "Name": "Great Wall Broadband"
            },
            ...
        ],
        "Regions": [
            {
                "Code": "CHE",
                "Name": "Switzerland"
            },
            {
                "Code": "AZE",
                "Name": "Azerbaijan"
            },
            {
                "Code": "PNG",
                "Name": "Papua New Guinea"
            },
            {
                "Code": "PSE",
                "Name": "Palestine"
            },
            {
                "Code": "FSM",
                "Name": "Micronesia"
            },
            ...
        ]
    }
}
```


&nbsp;
