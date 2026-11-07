---
title: "DescribeLiveRegionData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata-zh-CN"
---

调用`DescribeLiveRegionData` API 获取 MediaLive 覆盖区域的标识符。获取区域标识符后，可在支持按区域查询数据的 API 中使用这些标识符，以获取特定区域的数据。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveRegionData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需传递各自的专用参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveRegionData` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 专用返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|区域 |[区域](https://docs.byteplus.com/en/docs/24/107052#areas)数组 |`-` |区域信息。 |


<span id="areas"></span>
### 区域


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |String |`CN` |区域标识符。 |
|Name |String |`中国` |区域名称。 |
|国家 |[国家](https://docs.byteplus.com/en/docs/24/107052#countries)数组 |`-` |国家列表。 |


<span id="countries"></span>
### 国家


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |String |`CN` |国家标识符。 |
|Name |String |`中国` |国家名称。 |
|省份 |[省份](https://docs.byteplus.com/en/docs/24/107052#provinces)数组 |`-` |省份列表。 |


<span id="provinces"></span>
### 省份


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Code |String |`beijing` |省份标识符。 |
|Name |String |`北京` |省份名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

<span id="Sample response"></span>
### 返回调用结果示例

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


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107052#request-parameters)说明进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，原因是当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
