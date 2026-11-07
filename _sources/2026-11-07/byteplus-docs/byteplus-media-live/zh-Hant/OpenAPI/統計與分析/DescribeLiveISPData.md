---
title: "DescribeLiveISPData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata-zh-TW"
---

呼叫 `DescribeLiveISPData` API，以獲取為 BytePlus MediaLive 提供網路接入服務的網際網路服務供應商（ISP）識別碼。取得 ISP 識別碼後，可於支援 ISP 查詢的 API 中，使用這些識別碼查詢特定 ISP 的維度資料。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 30 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveISPData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveISPData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Response parameters"></span>
## 回應參數

如需查看 API 專屬回應參數，請參閱下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|ISPList |[ISPList](https://docs.byteplus.com/en/docs/24/107358#isplist) 陣列 |`-` |表示網際網路服務供應商（ISP）識別碼的陣列。 |


<span id="isplist"></span>
### ISPList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Code |String |`unicom` |網際網路服務供應商（ISP）識別碼。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|Name |String |`unicom` |網際網路服務供應商（ISP）名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202309042019116E825EC4FC63CD166C91",
        "Action": "DescribeLiveISPData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "ISPList": [
            {
                "Code": "unicom",
                "Name": "unicom"
            },
            {
                "Code": "railcom",
                "Name": "railcom"
            },
            {
                "Code": "telecom",
                "Name": "telecom"
            },
            {
                "Code": "mobile",
                "Name": "mobile"
            },
            {
                "Code": "cernet",
                "Name": "cernet"
            },
            {
                "Code": "tianwei",
                "Name": "tianwei"
            },
            {
                "Code": "alibaba",
                "Name": "alibaba"
            },
            {
                "Code": "tencent",
                "Name": "tencent"
            },
            {
                "Code": "drpeng",
                "Name": "drpeng"
            },
            {
                "Code": "btvn",
                "Name": "btvn"
            },
            {
                "Code": "huashu",
                "Name": "huashu"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參閱 [請求參數](https://docs.byteplus.com/en/docs/24/107358#request-parameters) 說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置和憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
