---
title: "API"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/api-zh-TW"
---

<span id="40775529"></span>
## IDanmuItem


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|id |String |是 |無 |評論的唯一 ID。請將此設為直播間內唯一的值。 |
|txt |String |是 |無 |彈幕內容。 |
|isPresenter |Boolean |否 |無 |指定彈幕是否由主持人發送。有效值：<br><br><br>* `true`：由主持人發送。<br><br>* `false`：非主持人發送。 |
|isSelf |Boolean |否 |無 |指定彈幕是否由當前用戶發送。有效值：<br><br><br>* `true`：由當前用戶發送。<br><br>* `false`：非當前用戶發送。 |
|duration |Number |否 |無 |彈幕顯示時長。單位：毫秒。 |


<span id="7ea0d771"></span>
## ILang

觀看頁面的語言資訊。


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|label |String |是 |無 |語言名稱。有效值：<br><br><br>* `简中`：簡體中文。<br><br>* `EN`：英文。<br><br>* `日本語`：日文。<br><br>* `繁中`：繁體中文。<br><br>* `한국인`：韓文。<br><br>* `แบบไทย`：泰文。<br><br>* `Tiếng Việt`：越南文。<br><br>* `بالعربية` ：阿拉伯文。<br><br>* `Türkçe`：土耳其文。<br><br>* `Español`：西班牙文。<br><br>* `Bahasa Indonesia`：印尼文。<br><br>* `Português`：葡萄牙文。<br><br>* `Русский`：俄文。 |
|value |Number |是 |無 |各語言對應的值。有效值：<br><br><br>* `0`：簡體中文。<br><br>* `1`：英文。<br><br>* `2`：日文。<br><br>* `3`：繁體中文。<br><br>* `4`：韓文。<br><br>* `5`：泰文。<br><br>* `6`：越南文。<br><br>* `7`：阿拉伯文。<br><br>* `8`：土耳其文。<br><br>* `9`：西班牙文。<br><br>* `10`：印尼文。<br><br>* `11`：葡萄牙文。<br><br>* `12`：俄文。 |


<span id="6ec26091"></span>
## ILangMap

定義觀看頁面可用的語言及當前語言。


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|languageOptional |[ILang](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#7ea0d771)[] |是 |`-` |觀看頁面支援的語言。 |
|currentLang |[ILang](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#7ea0d771) |是 |`-` |觀看頁面的當前語言。 |


<span id="40cc095d"></span>
## WebSDKBase

型別：`class`

<span id="338057e9"></span>
### getPlayerInstance()

取得播放器實例。

```TypeScript
() => any
```


**回傳值**

`any`

<span id="794f6502"></span>
### destroy()

銷毀 SDK。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">若當前觀看頁面不再需要 SDK，可呼叫此 API 銷毀 SDK 並釋放資源。但我們不建議在銷毀後重新建立 SDK。若再次需要 SDK，建議將 SDK 集成至新的觀看頁面，而非銷毀後重建。</div>


```TypeScript
() => void
```


<span id="e4f32962"></span>
### preloadActivity()

預先加載並快取直播間資料，以加速基於資訊流切換時的房間建立。

在基於資訊流場景切換直播間前呼叫此方法，可減少加載延遲。呼叫此方法後，若於**1 分鐘**內建立直播間，SDK 會重用快取資料以加速房間建立流程。

```TypeScript
(conf: SDKConf) => Promise<void>
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|conf |[SDKconf](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#2c9e46bc) |是 |無 |用於預載活動資料的 SDK 配置。 |


<span id="e41839ed"></span>
### sendDanmu()

發送彈幕。

```TypeScript
(payload: IDanmuItem[]) => void
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|payload |[IDanmuItem](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#40775529)[] |是 |`-` |彈幕配置。 |


<span id="8ba13e15"></span>
### updateModulesConf()

動態更新 SDK 的 `modules` 或 `options` 配置。

例如，可呼叫此 API 以在行動裝置上實現子母畫面（PiP）模式。有關效果的更多資訊，請參見[demo](https://live.byteplus.com/demo/sdk/index.mobile.pip.html)。

```TypeScript
(conf: Partial<SDKConfAll>) => void
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|conf |Partial |是 |無 |待更新的 SDK 配置。詳情請參閱[SDKconf](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-can-shu-zh-TW#2c9e46bc)。 |


<span id="4f4ea3d6"></span>
### updateMode2Token()

將 token 從 `mode=1` 升級為 `mode=2`。

```TypeScript
 (token: string) => Promise<{ status: boolean; info: string;}>
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|token |String |是 |無 |`mode=2` 的 token。 |


**回傳值**

`Promise<{ status: boolean; info: string; }>`


* `status`：表示更新是否成功。

   * `true`：成功。

   * `false`：失敗。

* `info`：錯誤訊息。


<span id="6db63c70"></span>
### seekVideo()

跳轉至預覽或回放中的指定時間點。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在 iOS 裝置上，若影片尚未播放，此 API 無法於微信內對影片進行定位。</div>


```TypeScript
(param: { time: number;}) => void
```



|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|param |\- |是 |`-` |預覽或回放時定位至指定時間點的配置。 |
|time |Number |是 |無 |定位至的時間點。單位：秒。 |


<span id="cb44cfa8"></span>
### getVodPlayInfo()

取得預覽或回放的資訊。

```TypeScript
() => { vid: string; currentTime: number; duration: number;}
```


**回傳值**

`{ vid: string; currentTime: number; duration: number; }`


* `vid`：影片唯一 ID。

* `currentTime`：當前播放時間點。單位：秒。

* `duration`：影片總時長。單位：秒。


<span id="88ab1ee1"></span>
### switchChannel()

切換至指定的直播源（若房間為直播中）或回放影片（若房間為回放模式）。

```TypeScript
webSDK.switchChannel(index);
```



|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|index |Number |是 |無 |直播源或回放影片的索引。<br><br>例如，索引為 0 時切換至第一個源/影片，索引為 1 時切換至第二個。 |


<span id="35db7c0e"></span>
### getPageLanguage()

取得觀看頁面支援的語言及當前語言。此方法通常與 `switchLanguage()` 搭配，用於自訂語言切換按鈕時。

```TypeScript
() => ILangMap
```


**回傳值**

[ILangMap](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#6ec26091)

<span id="a58b37a7"></span>
### switchLanguage()

切換觀看頁面語言。自訂語言切換按鈕時使用此方法。

```TypeScript
(lang: number) => void
```



|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|lang |Number |是 |無 |要切換觀看頁面的語言。請使用從 `getPageLanguage()` 取得的語言值。有效值：<br><br><br>* `0`：簡體中文。<br><br>* `1`：英文。<br><br>* `2`：日文。<br><br>* `3`：繁體中文。<br><br>* `4`：韓文。<br><br>* `5`：泰文。<br><br>* `6`：越南文。<br><br>* `7`：阿拉伯文。<br><br>* `8`：土耳其文。<br><br>* `9`：西班牙文。<br><br>* `10`：印尼文。<br><br>* `11`：葡萄牙文。<br><br>* `12`：俄文。 |


<span id="186d390f"></span>
### **showPlaybackListPopup()** 

在觀看頁面顯示回放集合列表彈窗。此方法通常與[hidePlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#8484f7d1)方法搭配，適用於觀看頁面有自有回放列表的場景。

```Plain
() => void
```


<span id="8484f7d1"></span>
### **hidePlaybackListPopup()** 

隱藏觀看頁面的回放集合列表彈窗。此方法通常與[showPlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#186d390f)方法搭配，適用於觀看頁面有自有回放列表的場景。

```Plain
() => void
```


<span id="15a73849"></span>
### **getPlayBackListInfo()** 

取得觀看頁面的回放集合列表資訊。此方法通常與[showPlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#186d390f)和[hidePlaybackListPopup()](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#8484f7d1)方法搭配，適用於觀看頁面有自有回放列表的場景。

```Plain
() => Array<{ vid: string; poster: string; name: string; duration: number }>
```


**回傳值：** 

回傳回放影片陣列。

`Array<{ vid: string; poster: string; name: string; duration: number }>`

每個項目包含：


* `vid`：影片唯一 ID。

* `poster`：帶協定頭的影片縮圖 URL。

* `name`：影片名稱。

* `duration`：影片總時長。單位：秒。


<span id="67c44fd2"></span>
### **lockPlayBackVods()** 

鎖定回放集合列表中的指定影片。此方法通常與[unlockPlayBackVods()](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#cddd4919)方法搭配，用於限制影片僅付費或 VIP 用戶可觀看。

```Plain
(vids: string[]) => void
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|`vids` |`string[]` |是 |無 |要鎖定的影片 ID 陣列。被鎖定的影片無法播放。 |


<span id="cddd4919"></span>
### **unlockPlayBackVods()** 

解鎖先前鎖定的回放影片。此方法通常與[lockPlayBackVods()](https://docs.byteplus.com/docs/byteplus-livesaas/api-zh-TW#67c44fd2)方法搭配，用於限制影片僅付費或 VIP 用戶可觀看。

```Plain
(vids: string[]) => void
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|`vids` |`string[]` |是 |無 |要解鎖的影片 ID 陣列。 |


<span id="ada4c709"></span>
### getProductList()

取得觀看頁面顯示的商品列表。

```TypeScript
() => Promise<ProductInfo[]>
```


**回傳值**

`ProductInfo[]`

產品物件陣列。欲了解更多資訊，請參閱[ProductInfo](https://docs.byteplus.com/docs/byteplus-livesaas/web-viewer-sdk-xing-bie-ding-yi-zh-TW#fe534689)。

<span id="bd140bf3"></span>
### updateProductInfo()

更新一個或多個產品的資訊。

```TypeScript
(props: Partial<ProductInfo>[]) => Promise<void>
```


**參數**


|名稱 |資料型別 |必填 |預設值 |說明 |
|---|---|---|---|---|
|`props` |`Partial<ProductInfo>[]` |是 |無 |產品資訊物件陣列。為了識別要更新的產品，每個物件必須包含產品的 `Id`。僅會更新每個物件中提供的欄位，未指定的欄位保持不變。更多資訊請參閱 `ProductInfo`。 |
