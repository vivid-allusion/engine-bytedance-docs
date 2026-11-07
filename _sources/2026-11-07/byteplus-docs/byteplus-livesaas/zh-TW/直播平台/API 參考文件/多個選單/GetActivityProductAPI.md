---
title: "GetActivityProductAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW"
---

呼叫此 API 以取得特定直播間中顯示的商品卡片配置。

<span id="Request"></span>
## 需求

配額：每個帳戶每分鐘最多 120 次查詢

<span id="ecda79a5"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityProductAPI&Version=2020-06-01`

* 方法：GET


<span id="8387d019"></span>
## 請求參數

以下表格未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="Query string parameters"></span>
### 查詢


|名稱 |資料型態 |是否必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityProductAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`1783981136301234` |直播間的活動 ID。可透過呼叫 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 取得 ID。 |


<span id="Sample request"></span>
## 回應參數


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|`-` |JSON Map |`-` |JSON 映射，其中鍵為商品卡片選單的序號，值為對應的配置。格式：`"Key":"Value"`。<br><br><br>* `"Key"`：商品卡片選單的序號，與 `Location` 值在 [GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-TW) 回應中相同。例如，若商品卡片選單的 `Location` 值為 `1`，則 `"Key"` 值為 `1`。<br><br>* `"Value"`：商品卡片的配置。更多資訊請參見 [ProductConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW#d514de4f)。 |


<span id="d514de4f"></span>
### ProductConfig


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|EnableFloating |Boolean |`false` |表示直播間是否開啟浮動頁面，讓觀眾點擊商品卡片後顯示商品詳情頁。<br><br><br>* `true`：在直播間的浮動頁面顯示商品詳情頁。觀眾可同時觀看影片並瀏覽商品詳情頁。此配置僅於行動裝置生效。<br><br>* `false`：在新頁面顯示商品詳情頁。觀眾無法同時觀看影片並瀏覽商品詳情頁。 |
|EnableUA |Boolean |`false` |表示是否啟用直連 URL 功能。此功能僅於行動裝置提供。<br><br><br>* `true`：已啟用。<br><br>* `false`：未啟用。 |
|UAAddress |String |`Mozilla` |指定 User\-Agent 字串以匹配特定客戶端環境。<br><br>當觀眾於 User Agent 包含該參數值的平台上點擊商品卡片時，將被導向商品卡片的直連 URL。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅當<code>EnableUA</code>為<code>true</code>時，此參數才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若<code>UAAddress</code>與<code>UAInfo.UAAddress</code>同時有值時，則以<code>UAInfo.UAAddress</code>為準。</div><br> |
|UAInfo |Array of[UAInfoMsg](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW#e22e1601) |`-` |配置直連 URL 功能的環境列表。最多可配置 5 個環境。環境的順序與每個商品卡片 `DirectUrls` 參數中的 URL 順序一致。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅當<code>EnableUA</code>為<code>true</code>時，此參數才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若<code>UAAddress</code>與<code>UAInfo.UAAddress</code>同時有值時，則以<code>UAInfo.UAAddress</code>為準。</div><br> |
|ProductsPosition |Integer |`0` |表示桌面觀看頁面中浮動商品卡片的顯示位置。<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：播放器右下角。 |
|DefaultRedirectImage |String |`www.example.com` |預設按鈕圖片的 URL，對應控制台上的 **Button image** 欄位。 |
|Product |Array of[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-TW#0a61e327) |`-` |商品卡片的配置。 |


<span id="e22e1601"></span>
#### UAInfoMsg


|名稱 |資料型態 |範例值 |說明 |
|---|---|---|---|
|UAName |String |`Env1` |環境名稱，對應於控制台中**特定環境的 User Agent**欄位所設定的環境名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">舊版單一環境配置名稱為<code>Env1</code>。</div><br> |
|UAAddress |String |`Mozilla/5.0 (env1)` |該環境的 User\-Agent 字串。當檢視者在 User Agent 包含此值的平台上點擊商品卡片時，將會被導向該商品卡片對應的直達 URL。 |


<span id="0a61e327"></span>
#### Product


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|標題 |String |`Dress` |您的商品名稱，對應於控制台中的**商品名稱**欄位。 |
|高亮 |String |`800` |您的商品零售價，對應於控制台中的**零售價**欄位。 |
|IntroduceImage |String |`www.example.com` |商品圖片的 URL，對應於控制台中的**商品圖片**欄位。該圖片顯示於商品卡片的左側。 |
|RedirectImage |String |`www.example.com` |按鈕圖片的 URL，對應於控制台中的**按鈕圖片**欄位。該圖片顯示於商品卡片的右下角。檢視者點擊按鈕後，將會被導向商品 URL 或直達 URL。 |
|RedirectUrl |String |`www.example.com` |商品詳情頁的 URL，對應於控制台中的**商品 URL**欄位。 |
|Index |Integer |`-` |已棄用。 |
|Id |Long |`20867` |商品卡片的 ID。 |
|EnableStatus |Integer |`1` |表示商品卡片是否已上架。<br><br><br>* `0`：未上架。<br><br>* `1`：已上架。 |
|備註 |String |`7天無條件退貨政策` |您的商品附加資訊，例如服飾尺寸。此參數對應於控制台中的**商品描述**欄位。 |
|Strikethrough |String |`1000` |您的商品劃線價，對應於控制台中的**劃線價**欄位。 |
|DirectUrl |String |`www.example.com` |商品詳情頁的直達 URL，對應於控制台中的**直達 URL**欄位。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅返回第一個環境的直達 URL。如需獲取所有已配置環境的直達 URL，請使用<code>DirectUrls</code>。</div><br> |
|DirectUrls |Array of String |`["https://www.direct_url1", "", "https://www.direct_url3"]` |商品詳情頁的直達 URL，對應於控制台中的多個**直達 URL**欄位。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅當<code>EnableUA</code>為<code>true</code>時，此參數才有值。最多返回 5 個直達 URL，分別對應於<code>UAInfo</code>列表中每個環境，順序與配置環境一致。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">空位置會以空字串返回，以保留與 <code>UAInfo</code> 的對齊。</div><br> |
|FloatingStatus |Integer |`1` |表示商品卡片是否以浮窗方式顯示。<br><br><br>* `1`：以浮窗方式顯示。<br><br>* 其他值：不以浮窗方式顯示。 |
|TagName |String |`Clothing` |商品類別，對應於控制台中的**商品類別**欄位。 |
|ExternalProductId |String |`20866` |外部商品 ID。此 ID 可防止同一商品重複新增至商品卡片選單。 |


<span id="20349dad"></span>
## 範例

<span id="3675694e"></span>
### 範例請求

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityProductAPI&Version=2020-06-01&ActivityId=1783981136301234
```


<span id="39032423"></span>
### 範例回應

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityProductAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1708786019
    },
    "Result": {
        "1": {
            "EnableFloating": false,
            "Product": [
                {
                    "Title": "Dress",
                    "Highlight": "800",
                    "IntroduceImage": "www.example.com",
                    "RedirectImage": "www.example.com",
                    "RedirectUrl": "www.example.com",
                    "Index": 0,
                    "Id": 20867,
                    "EnableStatus": 1,
                    "Strikethrough": "1000",
                    "DirectUrl": "www.example.com/env1/dress",
                    "DirectUrls": [
                        "www.example.com/env1/dress",
                        "www.example.com/env2/dress"
                    ],
                    "Remark": "7-day unconditional return policy",
                    "FloatingStatus": 1,                    
                    "TagName": "Clothing",
                    "ExternalProductId": "20866"
                }
            ],
            "EnableUA": true,
            "UAAddress": "Mozilla/5.0 (env1)",
            "UAInfo": [
                {
                    "UAName": "Env1",
                    "UAAddress": "Mozilla/5.0 (env1)"
                },
                {
                    "UAName": "Env2",
                    "UAAddress": "Mozilla/5.0 (env2)"
                }
            ],
            "ProductsPosition": 0,
            "DefaultRedirectImage": ""            
        }
    }
}
```


<span id="35b66db0"></span>
## 錯誤碼

共用錯誤碼列表請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
