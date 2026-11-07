---
title: "API HTTP 請求"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/api-http-qing-qiu-zh-TW"
---

要呼叫 BytePlus Live API，您必須構建標準的 HTTP 請求。本指南說明 API HTTP 請求的基本結構，包括請求 URL、方法與參數，並以 `CreateActivityAPIV2` API 作為實際範例。

完整的 HTTP 請求包含三個部分：


* 請求 URL

* 請求方法

* 請求參數


<span id="2da07eaa"></span>
## 請求 URL

請求 URL：`{URI-scheme}://{Endpoint}/?{query-string}`

下表說明 URL 的組成部分。


|**組件** |**說明** |
|---|---|
|URI\-scheme |支援 HTTP 與 HTTPS。為了安全考量，建議使用 HTTPS。 |
|Endpoint |API 接收請求的服務端點。BytePlus Live API 的端點為 `livesaas.byteplusapi.com`。 |
|query\-string |包含共用請求參數與操作專屬參數。<br><br>操作專屬參數及部分共用請求參數，請參閱各 API 操作的詳細說明。<br><br>完整共用請求參數列表，請參閱 [共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。 |


例如，`CreateActivityAPIV2` 的請求 URL 如下：

```JSON
http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
```


<span id="97a104dc"></span>
## 請求方法

請求方法指定要對資源執行的操作。BytePlus Live API 支援以下請求方法：


|**方法** |**說明** |
|---|---|
|GET |擷取指定資源。公開資料可透過請求標頭與查詢字串參數傳送。 |
|POST |向伺服器發送請求以新增資源或執行特殊操作。公開資料僅可加入標頭。 |


`CreateActivityAPIV2` 的請求方法為 POST。請求行如下：

```JSON
POST http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
```


<span id="19cdcb6c"></span>
## 請求參數

HTTP 請求包含以下類型的參數：


* 共用參數：如需更多資訊，請參閱 [共用參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters)。

* API 請求參數：請參考各 API 的參考主題。


<span id="e4de3a6c"></span>
## 請求範例

`CreateActivityAPIV2` 的完整請求如下：

```JSON
POST http://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
{
    "Name":"Live Room A",
    "LiveTime":1642668850
}
```
