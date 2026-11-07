---
title: "Web Standards API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Web-standards-cn-zh-tw"
---

本文檔介紹邊緣函數執行時期支援的標準 Web API。

<span id="textencoder-textdecoder"></span>
## TextEncoder/TextDecoder

TextEncoder 僅支援將 Unicode Codepoint 轉換為 UTF\-8 編碼的位元組流。TextDecoder 僅支援將 UTF\-8、GB2312、GBK 編碼的位元組流轉換為 Unicode Codepoint。

參見 MDN 文件 [TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder) 與 [TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder)。

<span id="限制條件"></span>
### 限制條件


* 為防範阻斷服務(DoS)風險，每次 decoder 輸入資料不得超過 8MB

* 為防範多字元串攻擊等潛在風險，執行時期會對 TextEncoder/TextDecoder 施加限制(例如緩衝區大小限制)以確保文字正確性與安全性


<span id="settimeout-setimmediate-setinterval-cleartimeout-clearimmediate-clearinterval"></span>
## setTimeout()/setImmediate()/setInterval()/clearTimeout()/clearImmediate()/clearInterval()

這些方法可用於在指定時間延遲後執行回調函數，或在指定間隔重複執行回調函數。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">為防範基於高精度時間戳記的旁路攻擊(如 Spectrum 攻擊)，這些方法會主動調整時間精度，不支援高精度時鐘</div>


參見以下 MDN 文件：


* [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout)

* [setImmediate()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setImmediate)

* [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setInterval)

* [clearTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearTimeout)

* [clearImmediate()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearImmediate)

* [clearInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearInterval)


<span id="限制條件"></span>
### 限制條件


* 單一請求上下文中，setTimeout()、setImmediate() 或 setInterval() 的累積呼叫次數不得超過 1000 次(例如：setTimeout() 呼叫 200 次 + setImmediate() 600 次，則 setInterval() 最多只能呼叫 200 次)

* 不可將其他請求上下文中定義的方法作為參數傳入，也不可將其他請求上下文取得的 ID 用於清除方法


<span id="session"></span>
## session

執行時期為每個請求上下文設定的全域物件，各請求上下文彼此不可見。session 包含以下屬性：


* **requestId**：回傳當前請求唯一 ID(無則回傳空字串)

* **event**：回傳觸發事件物件(即 addEventListener() 回調函數的 event 參數)

* **context**：獨立於請求上下文的物件，用於存取與請求無關的資料


<span id="範例"></span>
### 範例

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  const table = session.context; // 每次請求的 context 都是獨立的
  table.set("my-own-data", session.requestId);
}
```


<span id="atob-btoa"></span>
## atob()/btoa()

參見 MDN 文件 [atob()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/atob)、[btoa()](https://developer.mozilla.org/en-US/docs/Web/API/btoa)

<span id="url"></span>
## URL

參見 MDN 文件 [URL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">基於安全考量，URL 各組成部分設有記憶體閾值，若遇問題可透過<a href="https://console.byteplus.com/workorder/create">提交工單</a>調整配置</div>


<span id="urlsearchparams"></span>
## URLSearchParams

參見 MDN 文件 [URLSearchParams](https://developer.mozilla.org/zh-CN/docs/Web/API/URLSearchParams)

<span id="urlpattern"></span>
## URLPattern

參見 MDN 文件 [URLPattern](https://developer.mozilla.org/en-US/docs/Web/API/URLPattern)

<span id="console"></span>
## console

參見 MDN 文件 [console](https://developer.mozilla.org/en-US/docs/Web/API/console)

console 在每個請求上下文的儲存容量預設為 1 KB，超量資料將被截斷(除錯環境不受此限)

<span id="執行時期支援的方法"></span>
### 執行時期支援的方法

console 支援以下方法：


* info()

* log()

* error()

* warn()

* trace()

* assert()

* alert()


<span id="self"></span>
## self

指向當前執行時期全域變數的唯讀參照

<span id="範例"></span>
### 範例

呼叫 console.log() 輸出 self：

```javascript
console.log(self)
```


將獲得當前執行時期所有物件：

```js
Object {atob: "#function", btoa: "#function", setTimeout: "#function", setInterval: "#function", setImmediate: "#function", …}
AbortController: "#function"
AbortSignal: "#function"
Blob: "#function"
Body: "#function"
CompressionStream: "#function"
CronEvent: "#function"
CryptoKey: "#function"
CryptoKeyPair: "#function"
DOMException: "#function"
DecompressionStream: "#function"
Event: "#function"
EventTarget: "#function"
ExtendableEvent: "#function"
FetchEvent: "#function"
File: "#function"
FormData: "#function"
Headers: "#function"
HtmlComment: "#function"
HtmlDocend: "#function"
HtmlDoctype: "#function"
HtmlElement: "#function"
HtmlEndElement: "#function"
HtmlText: "#function"
InternalErrorEvent: "#function"
InternalEvent: "#function"
...
```


<span id="issparrow"></span>
## isSparrow

布林全域變數，用於判斷是否處於邊緣函數執行時期：


* true：當前為邊緣函數運行環境

* false：非邊緣函數運行環境


<span id="structuredclone"></span>
## structuredClone()

參見 MDN 文件 [structuredClone()](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)

<span id="queuemicrotask"></span>
## queueMicrotask()

參見 MDN 文件 [queueMicrotask()](https://developer.mozilla.org/en-US/docs/Web/API/queueMicrotask)

<span id="navigator-useragent"></span>
## Navigator.userAgent

參見 MDN 文件 [Navigator.userAgent](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent)

<span id="domexception"></span>
## DOMException

參見 MDN 文件 [DOMException](https://developer.mozilla.org/en-US/docs/Web/API/DOMException)

<span id="event"></span>
## Event

參見 MDN 文件 [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)

<span id="限制條件"></span>
### 限制條件


* 不支援 [bubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles) 屬性

* [timestamp](https://developer.mozilla.org/en-US/docs/Web/API/Event/timeStamp) 固定回傳 0

* [isTrusted](https://developer.mozilla.org/en-US/docs/Web/API/Event/isTrusted) 固定回傳 true

* 不支援以下廢棄 API：

   * [cancelBubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/cancelBubble)

   * [returnValue](https://developer.mozilla.org/en-US/docs/Web/API/Event/returnValue)

   * [srcElement](https://developer.mozilla.org/en-US/docs/Web/API/Event/srcElement)

   * [initEvent](https://developer.mozilla.org/en-US/docs/Web/API/Event/initEvent)


<span id="eventtarget"></span>
## EventTarget

參見 MDN 文件 [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)

<span id="限制條件"></span>
### 限制條件


* EventTarget.addEventListener() 的 options 參數中 passive 與 capture 固定為 false

* EventTarget.removeEventListener() 的 options 參數中 capture 固定為 false


<span id="abortsignal"></span>
## AbortSignal

參見 MDN 文件 [AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)

<span id="abortcontroller"></span>
## AbortController

參見 MDN 文件 [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)

<span id="url"></span>
## URL

參見 MDN 文件 [URL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)
