---
title: "UpdateActivityProductAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW"
---

調用此 API 以更新直播間中產品卡片的配置。

<span id="Request"></span>
## 需求

配額：每個帳號每分鐘 120 次查詢

<span id="36bded50"></span>
## HTTP 請求


* URL：`https://livesaas.byteplusapi.com/?Action=UpdateActivityProductAPI&Version=2020-06-01`

* 方法：POST


<span id="53aa7d97"></span>
## 請求參數

下列表格未包含所有通用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/docs/byteplus-livesaas/gong-yong-can-shu-zh-TW#f1706967)。

<span id="f145b498"></span>
### 查詢


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityProductAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。當前版本：`2020-06-01`。 |


<span id="8cd6fc93"></span>
### 主體


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|ActivityId |Long |是 |`1783981136301234` |直播間的活動 ID。可通過調用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW) 獲取 ID。 |
|Products |[Products](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW#a460b55a) 陣列 |是 |`-` |產品卡片的配置。 |


<span id="a460b55a"></span>
#### Products


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|`-` |JSON 映射 |是 |`-` |產品卡片選單的序號及產品卡片的配置。格式：`"Key":"Value"`。<br><br><br>* `"Key"`：產品卡片選單的序號。可通過調用 [GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-TW) 獲取序號。例如，若 `GetActivityMenuAPI` 回應中產品卡片選單的 `Location` 為 `1`，則 `"1"` 作為 `"Key"` 使用。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">請確保此位置對應於產品卡片選單，且 <code>Type</code> 在 <code>GetActivityMenuAPI</code> 回應中的值為 <code>2</code>。   </div><br>   <br><br>* `"Value"`：產品卡片的配置。更多資訊請參見 [ProductConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW#993adfaa)。 |


<span id="993adfaa"></span>
##### **ProductConfig**


|名稱 |資料型別 |是否必填 |範例值 |描述 |
|---|---|---|---|---|
|EnableFloating |Boolean |是 |`false` |指定觀眾點擊產品卡片後，是否在直播間中以浮動頁面顯示產品詳情頁。<br><br>有效值：<br><br><br>* `true`：是。在直播間中以浮動頁面顯示產品詳情頁。觀眾可同時觀看視頻並瀏覽產品詳情頁。此配置僅於行動裝置生效。<br><br>* `false`：否。於新頁面顯示產品詳情頁。觀眾無法同時觀看視頻並瀏覽產品詳情頁。 |
|EnableUA |Boolean |否 |`false` |指定是否啟用直達 URL 功能。此功能僅於行動裝置可用。<br><br>預設值：`false`。<br><br>有效值：<br><br><br>* `true`：啟用該功能。<br><br>* `false`：停用該功能。 |
|UAAddress |String |否 |`Mozilla` |特定環境的 User Agent。<br><br>當觀眾於 User Agent 包含該參數值的平台點擊產品卡片時，將跳轉至產品卡片的直達 URL。但若觀眾於其他平台點擊產品卡片，則會跳轉至產品 URL（RedirectUrl）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅設定單一環境，並保留以維持向後相容性。若要設定最多 5 個環境，請改用 <code>UAInfo</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>EnableUA</code> 為 <code>true</code> 且未傳入 <code>UAInfo</code> 時，此參數為必填。若兩者皆傳入，則以 <code>UAInfo</code> 為主。</div><br> |
|UAInfo |[UAInfoMsg](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW#3a35fa91) 陣列 |否 |`-` |直達 URL 功能的環境列表。最多可配置 5 個環境。環境順序需與每個產品卡片 `DirectUrls` 參數中的 URL 順序一致。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>EnableUA</code> 為 <code>true</code> 且未傳入 <code>UAAddress</code> 時，此參數為必填。若兩者皆傳入，則以 <code>UAInfo</code> 為主。</div><br> |
|ProductsPosition |Integer |否 |`0` |指定浮動產品卡片於 PC 端觀看頁面上的顯示位置。<br><br>預設值：`0`。<br><br>有效值：<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：在播放器的右下角。 |
|DefaultRedirectImage |字串 |否 |`https://example.com` |預設按鈕圖片的 URL，對應控制台上的 **Button image** 欄位。<br><br>圖片必須為 JPG、GIF、PNG 或 BMP 格式，並會取代系統預設圖片。建議解析度為 160×60。 |
|Product |Array of[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-TW#Product) |是 |`-` |商品卡片的配置。 |


<span id="3a35fa91"></span>
###### **UAInfoMsg**


|Name |資料型別 |必填 |範例值 |描述 |
|---|---|---|---|---|
|UAName |字串 |是 |`TikTokiOSEnv1` |環境名稱，最多 20 個字元。此名稱會標記商品卡片配置時對應的直連 URL。 |
|UAAddress |字串 |是 |`TikTok` |環境的 User Agent 字串，最多 500 個字元。當觀眾在 User Agent 包含此值的平台上點擊商品卡片時，將跳轉至商品卡片對應的直連 URL。 |


<span id="244cef61"></span>
###### **Product**


|Name |資料型別 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Title |字串 |是 |`Dress` |您的商品名稱，對應控制台上的 **Product name** 欄位。<br><br>值必須為 1\-3315 個字元。 |
|Highlight |字串 |否 |`800` |您的商品零售價，對應控制台上的 **Retail price** 欄位。<br><br>值必須為 1\-260 個字元。 |
|IntroduceImage |字串 |否 |`www.example.com` |商品圖片的 URL，對應控制台上的 **Product image** 欄位。圖片顯示於商品卡片的左側。<br><br>商品圖片支援的格式：JPG、GIF、PNG、BMP。 |
|RedirectImage |字串 |否 |`www.example.com` |按鈕圖片的 URL，對應控制台上的 **Button image** 欄位。圖片顯示於商品卡片的右下角。觀眾點擊按鈕後會跳轉至商品 URL 或直連 URL。<br><br>按鈕圖片支援的格式：JPG、GIF、PNG、BMP。 |
|RedirectUrl |字串 |否 |`www.example.com` |商品詳情頁的 URL，對應控制台上的 **Product URL** 欄位。 |
|Index |整數 |否 |`-` |已棄用。 |
|Id |長整數 |否 |`-` |已棄用。 |
|EnableStatus |整數 |否 |`1` |指定是否列出商品卡片。預設值：`0`。<br><br>有效值：<br><br><br>* `0`：商品卡片未列出。<br><br>* `1`：商品卡片已列出。 |
|DirectUrl |字串 |否 |`www.example.com` |商品詳情頁的直連 URL，對應控制台上的 **Direct URL** 欄位。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅當 <code>EnableUA</code> 的值為 <code>true</code> 時，直連 URL 才會生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅設定第一個環境的直連 URL，並保留以維持向後相容性。若要為每個環境設定直連 URL，請改用 <code>DirectUrls</code>。</div><br> |
|DirectUrls |字串陣列 |否 |`["www.example.com"]` |商品詳情頁的直連 URL，對應選單（`UAInfo`）的直連 URL 配置項。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅當 <code>EnableUA</code> 的值為 <code>true</code> 時，直連 URLs 才會生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>DirectUrls</code> 的數量應與 <code>UAInfo</code> 環境數量一致：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">若 <code>DirectUrls</code> 的數量多於 <code>UAInfo</code> 的環境數量，則多出的 URL 不會生效。例如，若已設定 2 個 UA 環境並傳入 <code>["https://direct_url1", "https://direct_url2", "https://direct_url3"]</code>，則 <code>https://direct_url3</code> 不會生效。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">若 <code>DirectUrls</code> 的數量少於 <code>UAInfo</code> 的環境數量，缺少的位置會以空字串補齊。例如，若已設定 2 個 UA 環境並傳入 <code>["https://direct_url1"]</code>，則 UA1 的直連 URL 為 <code>https://direct_url1</code>，UA2 的直連 URL 為空值（<code>""</code>）。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若不想為特定 UA 環境設定直連 URL，請於對應位置傳入 <code>""</code>。例如，若環境 1 和 3 需要直連 URL，而環境 2 不需要，請傳入 <code>["https://direct_url1", "", "https://direct_url3"]</code>。</div><br> |
|Remark |字串 |否 |`XL` |商品的額外資訊，例如服裝尺寸。此參數對應控制台上的 **Product description** 欄位。<br><br>值必須為 1\-3315 個字元。 |
|Strikethrough |字串 |否 |`1000` |您的商品列表價，對應控制台上的 **List price** 欄位。<br><br>值必須為 1\-260 個字元。 |
|TagName |字串 |否 |`Clothing` |商品分類，對應控制台上的 **Product category** 欄位。<br><br>值必須為 1\-20 個字元。 |
|ExternalProductId |字串 |否 |`20866` |外部產品 ID。此 ID 可防止同一產品被重複新增至同一產品卡片選單。<br><br>該值必須為 1\-128 個字元長度。 |


<span id="d57c9da0"></span>
## 回應參數


|名稱 |資料型別 |範例值 |描述 |
|---|---|---|---|
|狀態 |布林值 |`true` |表示產品卡片是否成功更新。<br><br><br>* `true`：成功。<br><br>* `false`：失敗。 |


<span id="8865deac"></span>
## 範例

<span id="c6eb5b80"></span>
### 請求範例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityProductAPI&Version=2020-06-01
{
     "ActivityId":1783981136301234,
     "Products":{
         "1":{
             "EnableFloating":false,
             "EnableUA":true,
             "UAInfo":[
                {
                     "UAName":"MozillaEnv1",
                     "UAAddress":"Mozilla/5.0 (env1)"
                },
                {
                     "UAName":"MozillaEnv2",
                     "UAAddress":"Mozilla/5.0 (env2)"
                }
             ],
             "ProductsPosition":0, 
             "DefaultRedirectImage":"https://example.com",
             "Product":[
                {
                     "Title":"Dress", 
                     "Highlight":"800", 
                     "IntroduceImage":"www.example.com", 
                     "RedirectImage":"www.example.com", 
                     "RedirectUrl":"www.example.com", 
                     "EnableStatus":1,
                     "DirectUrls":[
                        "www.example.com/env1/dress",
                        "www.example.com/env2/dress"
                     ],
                     "Remark":"XL",
                     "Strikethrough":"1000",
                     "TagName":"Clothing",
                     "ExternalProductId": "20866"
                }
            ]
        }
    }
}
```


<span id="da670bbe"></span>
### 回應範例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateActivityProductAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1708782797
    },
    "Result": {
        "Status": true
    }
}
```


<span id="f0c323f3"></span>
## 錯誤碼

有關通用錯誤碼的列表，請參見 [常見錯誤與狀態碼](https://docs.byteplus.com/docs/byteplus-livesaas/chang-jian-cuo-wu-yu-zhuang-tai-ma-zh-TW)。
