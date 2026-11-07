---
title: "ExplainProduct"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/shuo-ming-chan-pin-zh-TW"
---

將產品釘選至選單頂部並在觀看頁面顯示於浮動視窗，或將產品恢復至選單下的原始位置並從觀看頁面的浮動視窗移除顯示。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每分鐘最多 120 次請求

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://livesaas.byteplusapi.com/?Action=ExplainProduct&Version=2023\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

下列表格並未包含所有通用請求參數。完整列表請參見[通用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ExplainProduct` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。目前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ActivityId |Long |是 |`17791682871580` |直播間的活動 ID。你可以呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)，從回應參數`Id`取得 ID。 |
|ExplainStatus |Integer |是 |`1` |對產品執行的操作。有效值：<br><br><br>* `1`：將產品釘選至選單頂部並在觀看頁面顯示於浮動視窗。<br><br>* `2`：將產品恢復至選單下的原始位置並從觀看頁面的浮動視窗移除顯示。 |
|ProductId |Long |否 |`492046` |產品卡片的 ID。你可以呼叫[GetActivityProductAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityproductapi)，從回應參數`Id`取得 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請傳入<code>ProductId</code>或<code>ExternalProductId</code>其中之一。若同時傳入，僅<code>ProductId</code>生效。</div><br> |
|ExternalProductId |String |否 |`your_product_id_12345` |外部產品 ID，在每個選單中的產品卡片皆唯一。你可以呼叫[GetActivityProductAPI](https://docs.byteplus.com/zh-CN/docs/byteplus-livesaas/docs-getactivityproductapi)取得 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">請傳入<code>ProductId</code>或<code>ExternalProductId</code>其中之一。若同時傳入，僅<code>ProductId</code>生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若你的直播間中有多個此 ID 的產品，操作將針對產品卡片最左側選單下的產品執行。</div><br> |


<span id="Response parameters"></span>
## 回應參數


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Status |Boolean |`true` |表示操作是否成功執行。有效值：<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://livesaas.byteplusapi.com/?Action=ExplainProduct&Version=2023-08-01
{
    "ActivityId": 17791****71580,
    "ProductId": 49**46,
    "ExternalProductId": "your_product_id_12345",
    "ExplainStatus": 1
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ExplainProduct",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參見[常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
