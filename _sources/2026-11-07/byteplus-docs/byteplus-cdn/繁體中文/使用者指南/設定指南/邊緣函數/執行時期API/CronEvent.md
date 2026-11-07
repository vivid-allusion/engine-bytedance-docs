---
title: "CronEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-CronEvent-cn-zh-tw"
---

cron 類型的事件，由 Cron 觸發器觸發。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">您必須透過呼叫 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw">addEventListener()</a> 註冊監聽器來監聽 cron 事件以取得 <code>CronEvent</code> 物件。</div>


<span id="方法"></span>
## 方法

<span id="text"></span>
### text()

此方法會回傳一個 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，當 Promise 被 resolve 後，回傳值為您在 Cron 觸發器中配置的自訂參數，類型為 [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)。請參閱 [Cron觸發器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw) 以了解如何在 Cron 觸發器中配置自訂參數。

<span id="arraybuffer"></span>
### arrayBuffer()

此方法會回傳一個 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，當 Promise 被 resolve 後，回傳值為您在 Cron 觸發器中配置的自訂參數，類型為 [ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)。請參閱 [Cron觸發器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw) 以了解如何在 Cron 觸發器中配置自訂參數。

<span id="stream"></span>
### stream()

此方法會回傳一個 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，當 Promise 被 resolve 後，回傳值為您在 Cron 觸發器中配置的自訂參數，類型為 [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)。請參閱 [Cron觸發器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw) 以了解如何在 Cron 觸發器中配置自訂參數。

<span id="json"></span>
### json()

此方法會回傳一個 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)，當 Promise 被 resolve 後，回傳值為您在 Cron 觸發器中配置的自訂參數，類型為 [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)。請參閱 [Cron觸發器](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-cron-triggers-cn-zh-tw) 以了解如何在 Cron 觸發器中配置自訂參數。

<span id="屬性"></span>
## 屬性

<span id="job"></span>
### job

回傳 Cron 觸發器的名稱。

<span id="cronexpression"></span>
### cronExpression

回傳 Cron 觸發器的 Cron 表達式。

<span id="範例程式碼"></span>
## 範例程式碼

```JavaScript
// 註冊一個事件監聽器，監聽 cron 事件
addEventListener('cron', onCron);

// cron 事件被觸發時，被呼叫的回呼函式
async function onCron(event) {
    // 這裡可以添加定時任務的具體程式碼
    return 'Parameter: ' + await event.text();
}
```
