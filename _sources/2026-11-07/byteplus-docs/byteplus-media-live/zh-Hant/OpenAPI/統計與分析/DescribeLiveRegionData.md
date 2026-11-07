---
title: "DescribeLiveRegionData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata-zh-TW"
---

呼叫 `DescribeLiveRegionData` API，以獲取 MediaLive 所覆蓋區域的識別碼。取得區域識別碼後，您可以在支援按區域查詢資料的 API 中使用這些識別碼，以檢索特定區域的資料。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveRegionData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需提供 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveRegionData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 回應參數

如需查看 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|區域 |[區域](https://docs.byteplus.com/en/docs/24/107399#areas)陣列 |`-` |區域資訊。 |


<span id="areas"></span>
### 區域


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |String |`CN` |區域識別碼。 |
|Name |String |`中國` |區域名稱。 |
|國家 |[國家](https://docs.byteplus.com/en/docs/24/107399#countries)陣列 |`-` |國家列表。 |


<span id="countries"></span>
### 國家


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |String |`CN` |國家識別碼。 |
|Name |String |`中國` |國家名稱。 |
|省份 |[省份](https://docs.byteplus.com/en/docs/24/107399#provinces)陣列 |`-` |省份列表。 |


<span id="provinces"></span>
### 省份


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |String |`beijing` |省份識別碼。 |
|Name |String |`北京` |省份名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

<span id="Sample response"></span>
### 回應範例

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
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107399#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
