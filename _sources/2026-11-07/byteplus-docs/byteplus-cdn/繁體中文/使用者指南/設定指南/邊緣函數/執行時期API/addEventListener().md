---
title: "addEventListener()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw"
---

註冊一個事件監聽器。參見 MDN 文件 [addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)。

邊緣函數支援以下事件類型：


* fetch：網域名稱觸發器觸發的事件類型。参见 [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw)。

* cron：Cron 觸發器觸發的事件類型。参见 [CronEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-CronEvent-cn-zh-tw)。


您可以在同一個程式碼檔案中同時註冊 cron 事件和 fetch 事件，這兩種事件對應的回呼函數互不干擾。每個事件最多可註冊 16 個回呼函數。

您可以多次呼叫 `addEventListener()` 來註冊多個相同或不同事件的監聽器。每個監聽器需註冊一個回呼函數：


* 對於 fetch 事件：多個回呼函數將依註冊順序執行。若某個回呼函數已透過 [FetchEvent](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw#respondwith) 回傳結果，後續註冊但未執行的回呼函數將不再被呼叫。若所有回呼函數在回應時間限制內均未回傳結果，執行時期將會拋出錯誤。

* 對於 cron 事件：僅會執行第一個回呼函數。若該函數在回應時間限制內未回傳結果，執行時期將會拋出錯誤。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">參見 <a href="https://docs.byteplus.com/docs/byteplus-cdn/functions-usage-limits">使用限制</a> 了解邊緣函數的回應時間限制。</div>


<span id="範例"></span>
## 範例

<span id="監聽-fetch-事件"></span>
### 監聽 fetch 事件

以下程式碼描述如何監聽 fetch 事件

```JavaScript
addEventListener(
    'fetch', (event) => {
      // 回呼函數1 印出 "callback1 has been triggered"
      console.log("callback1 has been triggered");
    });

addEventListener(
    'fetch', (event) => {
      // 回呼函數2 印出 "callback2 has been triggered"
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  // 此呼叫表示已處理回應，後續回呼函數不會被執行
    });

addEventListener('fetch', (event) => {
    // 回呼函數3 根據程式碼結構，此函數永遠不會被執行
    console.log("這個永遠不會被顯示");
});
```


<span id="監聽-cron-事件"></span>
### 監聽 cron 事件

以下程式碼描述如何監聽 cron 事件

```javascript
addEventListener('cron', onCron);

async function onCron(event) {

  // 1. 可透過OpenAPI或控制台為Cron觸發器添加 payload
  //    此資料不影響程式運作，可透過event物件API取得
  const text = await event.text();

  // 2. 取得Cron觸發器的相關屬性
  const job = event.job; // Cron觸發器名稱
  const cronExpression = event.cronExpression; // Cron時間規則
  console.log("cron triggered");
}
```
