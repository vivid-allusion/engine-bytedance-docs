---
title: "FetchEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-FetchEvent-cn-zh-tw"
---

fetch 類型的事件，由網域名稱觸發器觸發。

請參考 MDN 文件中的 [FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">邊緣函數執行時期不允許您使用 <code>FetchEvent()</code> 建構函數來建構 <code>FetchEvent</code> 物件。您需要透過呼叫 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-addEventListener-cn-zh-tw">addEventListener()</a> 來註冊監聽器以監聽 fetch 事件，進而取得 <code>FetchEvent</code> 物件。</div>


<span id="方法"></span>
## 方法

<span id="respondwith"></span>
### respondWith()

在 fetch 事件被觸發時，邊緣函數會攔截使用者請求，並將您向該方法傳入的 [Response](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Response-cn-zh-tw) 物件或一個 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 物件作為回應。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">如果您未呼叫 <code>respondWith()</code> 方法，邊緣函數會在 fetch 事件被觸發時將使用者請求轉送至 BytePlus CDN。</div>


<span id="範例"></span>
#### 範例

```js
// 邊緣函數會將使用者請求轉送至 BytePlus CDN。
addEventListener(
    'fetch', (event) => {
      console.log("callback1 has been triggered");
    });

// 邊緣函數會攔截使用者請求，並允許您將 Response 物件作為回應傳遞給此方法的參數。
addEventListener(
    'fetch', (event) => {
      console.log("callback2 has been triggered");
      event.respondWith(new Response("callback2 has been triggered"));  
    });
```


<span id="waituntil"></span>
### waitUntil()

通知邊緣函數執行時期等待回呼函數中註冊的所有 [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) 物件被解析或拒絕。`waitUntil()` 方法可以被多次呼叫。您也可以在彼此之間巢狀使用 `waitUntil()` 方法。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">如果函數的執行時間超過<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/functions-usage-limits-zh-tw">回應時間限制</a>，邊緣函數執行時期會銷毀請求內容，並且不再等待處於擱置狀態的 <code>Promise</code> 物件。</div>


* <div data-tips="true" data-tips-type="warning">如果任何由 <code>waitUntil()</code> 註冊的 <code>Promise</code> 物件被拒絕，邊緣函數執行時期會銷毀請求內容。建議為每個 <code>Promise</code> 新增錯誤處理，例如使用 <code>.catch()</code> 方法或 <code>try-catch</code> 陳述式。</div>



如果您未呼叫 `waitUntil()` 方法且未使用 `await`，當回呼函數透過 `respondWith()` 傳回回應後，邊緣函數執行時期會銷毀請求內容，並且不再等待處於擱置狀態的 `Promise` 物件。`await` 雖然可以等待 `Promise` 被解析或拒絕，但會暫停回呼函數的執行。相比之下，`waitUntil()` 方法允許回呼函數在等待 `Promise` 被解析或拒絕的同時，繼續執行其他作業。

<span id="範例"></span>
#### 範例

```JavaScript
// 定義上傳日誌的 URL
const uploadURL = "https://log-collection.example.com/";

// 非同步函數，用於上傳回應時間
async function uploadLog(waiter) {
    const start = Date.now();
    // 等待 waiter promise 完成，表示請求的回應已傳送完成
    await waiter;
    // 記錄結束時間。注意，邊緣函數的時鐘對齊到 10 ms 左右，這是為了規避側通道攻擊（side-channel attack）。
    const end = Date.now();
    const cost = (end - start);
    // 將物件序列化為 JSON 字串作為請求主體
    const body = JSON.stringify({ cost: cost });
    await fetch(uploadURL, {
        method: "POST",
        body: body,
        headers: {
            'Content-Type': 'application/json'
        }
    });
}

// 監聽 fetch 事件，並在事件發生時呼叫 handle 函數處理
addEventListener('fetch', (event) => {
    event.respondWith(handle(event));
});

// 處理事件的函數
async function handle(event) {
    const response = new Response("Hello World");
    // response.body 是一個 readableStream。邊緣函數執行時期 API 包含 waitClose 方法
    // waitClose 會傳回一個 promise。當串流被終止時（可能是因為錯誤或完成），waitClose 會被解析
    // 注意：如果您的Response是用於返回不含Body的回應，例如對 HTTP HEAD 請求的回應、304回應、204回應，則waitClose() 無效
    event.waitUntil(uploadLog(response.body.waitClose()));
    return response;
}
```


<span id="屬性"></span>
## 屬性

<span id="info"></span>
### info

取得用戶端資訊。


* `info.clientIp`：用戶端的 IP 位址。如果用戶端設定了代理伺服器，則此屬性會傳回代理伺服器的 IP 位址。

* `info.geo`：用戶端 IP 的地理資訊。geo 有以下屬性：

   * `geo.country`：傳回此 IP 位址所屬國家的名稱，例如 `China` 或 `United States`。

   * `geo.countryCode`：傳回此 IP 位址所屬國家的兩位字母代碼，符合 ISO 3166\-1 alpha\-2 標準。例如 `CN` 或 `US`。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">您只能透過 <code>province</code> 欄位識別中國香港（Hong Kong）、中國澳門（Macao）和中國台灣（Taiwan）。中國香港、中國澳門和中國台灣的 <code>countryCode</code> 皆為 <code>CN</code>。   </div>
   

   * `geo.region`：傳回此 IP 位址所屬中國地理大區的名稱。例如 `EastChina`。如果此 IP 位址不屬於中國大陸，此參數會傳回 `XX`。

   * `geo.province`：傳回此 IP 位址所屬第一級行政區的名稱。例如 `Hebei` 或 `New Jersey`。

   * `geo.city`：傳回此 IP 位址所屬城市的名稱。例如 `Shijiazhuang` 或 `Tampere`。

   * `geo.isp`：傳回此 IP 位址所屬 ISP 的名稱。例如 `ChinaUnicom` 或 `DigitalOcean`。


<span id="範例"></span>
#### 範例

```JavaScript
addEventListener(
    'fetch', (event) => { event.respondWith(handle(event)); });
    
async function handle(event) {
  const info = event.info;
  console.log(info);  // 取得用戶端的所有資訊

  const clientIp = event.info.clientIp;
  console.log(clientIp); // 取得用戶端的 IP 位址

  const country = event.info.geo.country;
  console.log(country); // 取得用戶端 IP 位址所屬的國家名稱

  return new Response("done");
}
```


<span id="file"></span>
### File

請參考 MDN 文件 [File](https://developer.mozilla.org/en-US/docs/Web/API/File)。

<span id="blob"></span>
### Blob

請參考 MDN 文件 [Blob](https://developer.mozilla.org/en-US/docs/Web/API/Blob)。

<span id="formdata"></span>
### FormData

請參考 MDN 文件 [FormData](https://developer.mozilla.org/en-US/docs/Web/API/FormData)。
