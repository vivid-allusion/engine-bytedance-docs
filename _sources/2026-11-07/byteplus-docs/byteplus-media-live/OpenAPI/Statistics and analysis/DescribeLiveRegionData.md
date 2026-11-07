---
title: "DescribeLiveRegionData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata"
---

Call the `DescribeLiveRegionData` API to get the identifiers of the regions covered by MediaLive. Once you have the region identifiers, you can use them in APIs that support querying data by region to retrieve data for specific areas.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveRegionData&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveRegionData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Areas |Array of [Areas](https://docs.byteplus.com/en/docs/24/20945#areas) |`-` |The Area information. |


<span id="areas"></span>
### Areas


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |String |`CN` |The identifier of the region. |
|Name |String |`中国` |The name of the region. |
|Countries |Array of [Countries](https://docs.byteplus.com/en/docs/24/20945#countries) |`-` |A list of countries. |


<span id="countries"></span>
### Countries


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |String |`CN` |The identifier of the country. |
|Name |String |`中国` |The name of the country. |
|Provinces |Array of [Provinces](https://docs.byteplus.com/en/docs/24/20945#provinces) |`-` |A list of provinces. |


<span id="provinces"></span>
### Provinces


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Code |String |`beijing` |The identifier of the province. |
|Name |String |`北京` |The name of the province. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveRegionData&Version=2023-01-01
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230831140335992B73F008D5242E199D",
        "Action": "DescribeLiveRegionData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "Areas": [
            {
                "Code": "CN",
                "Name": "中国",
                "Countries": [
                    {
                        "Code": "CN",
                        "Name": "中国",
                        "Provinces": [
                            {
                                "Code": "beijing",
                                "Name": "北京"
                            },
                            {
                                "Code": "shanghai",
                                "Name": "上海"
                            },
                            {
                                "Code": "tianjin",
                                "Name": "天津"
                            }
                        ]
                    }
                ]
            },
            {
                "Code": "AP1",
                "Name": "亚太一区",
                "Countries": [
                    {
                        "Code": "CN",
                        "Name": "中国",
                        "Provinces": [
                            {
                                "Code": "HK",
                                "Name": "香港"
                            },
                            {
                                "Code": "MO",
                                "Name": "澳门"
                            }
                        ]
                    },
                    {
                        "Code": "KH",
                        "Name": "柬埔寨",
                        "Provinces": []
                    },
                    {
                        "Code": "JP",
                        "Name": "日本",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "AP2",
                "Name": "亚太二区",
                "Countries": [
                    {
                        "Code": "CN",
                        "Name": "中国",
                        "Provinces": [
                            {
                                "Code": "TW",
                                "Name": "台湾"
                            }
                        ]
                    },
                    {
                        "Code": "ID",
                        "Name": "印度尼西亚",
                        "Provinces": []
                    },
                    {
                        "Code": "PH",
                        "Name": "菲律宾",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "AP3",
                "Name": "亚太三区",
                "Countries": [
                    {
                        "Code": "KR",
                        "Name": "韩国",
                        "Provinces": []
                    },
                    {
                        "Code": "AU",
                        "Name": "澳大利亚",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "NA",
                "Name": "北美",
                "Countries": [
                    {
                        "Code": "US",
                        "Name": "美国",
                        "Provinces": []
                    },
                    {
                        "Code": "CA",
                        "Name": "加拿大",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "SA",
                "Name": "南美",
                "Countries": [
                    {
                        "Code": "BR",
                        "Name": "巴西",
                        "Provinces": []
                    },
                    {
                        "Code": "AR",
                        "Name": "阿根廷",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "EU",
                "Name": "欧洲",
                "Countries": [
                    {
                        "Code": "GB",
                        "Name": "英国",
                        "Provinces": []
                    },
                    {
                        "Code": "NL",
                        "Name": "荷兰",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "MEAA",
                "Name": "中东",
                "Countries": [
                    {
                        "Code": "TR",
                        "Name": "土耳其",
                        "Provinces": []
                    },
                    {
                        "Code": "SA",
                        "Name": "沙特阿拉伯",
                        "Provinces": []
                    }
                ]
            },
            {
                "Code": "OTHER",
                "Name": "其他",
                "Countries": []
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/20945#request-parameters) description for inspection. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
