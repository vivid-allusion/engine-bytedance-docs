---
title: "Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn-zh-tw"
---

[Streams API](https://developer.mozilla.org/zh-CN/docs/Web/API/Streams_API) 允許您存取並處理來自網路的資料流。邊緣函數的執行時期支援以下 Streams API。

<span id="transformstream"></span>
## TransformStream

參見 MDN 文件 [TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在邊緣函數執行時期中，您只能透過建構函數 <code>TransformStream()</code> 建立 <code>TransformStream</code> 物件。</div>


<span id="readablestream"></span>
## ReadableStream

參見 MDN 文件 [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">邊緣函數執行時期不允許您使用建構函數 <code>ReadableStream()</code> 建立 <code>ReadableStream</code> 物件。您只能透過 <a href="https://docs.byteplus.com/en/docs/18/45022#transformstream">TransformStream</a> 物件的 <code>readable</code> 屬性取得 <code>ReadableStream</code> 物件。</div>


* <div data-tips="true" data-tips-type="warning"><a href="https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/tee">ReadableStream.tee()</a> 方法會佔用記憶體。您需要避免函數的執行時期因記憶體超出<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/functions-usage-limits-zh-tw">使用限制</a>而傳回 OOM 錯誤。</div>



<span id="邊緣函數執行時期額外支援的方法與屬性"></span>
### 邊緣函數執行時期額外支援的方法與屬性

在邊緣函數執行時期中，`ReadableStream` 介面還額外支援以下方法與屬性。

<span id="waitclose"></span>
#### waitClose()

回傳一個 promise。當 stream 被讀取完畢或發生錯誤時，promise 會被 resolve。

<span id="finished"></span>
#### finished

表示 stream 是否已讀取完畢或發生錯誤：


* true ：stream 已讀取完畢或發生錯誤

* false：stream 尚未讀取完畢


<span id="readablestreamdefaultreader"></span>
## ReadableStreamDefaultReader

參見 MDN 文件 [ReadableStreamDefaultReader](https://developer.mozilla.org/zh-CN/docs/Web/API/ReadableStreamDefaultReader)。

<span id="writablestream"></span>
## WritableStream

參見 MDN 文件 [WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">邊緣函數執行時期不允許您使用建構函數 <code>WritableStream()</code> 建立 <code>WritableStream</code> 物件。您只能透過 <a href="https://docs.byteplus.com/en/docs/18/45022#transformstream">TransformStream</a> 物件的 <code>writable</code> 屬性取得 <code>WritableStream</code> 物件。</div>


<span id="邊緣函數執行時期額外支援的方法與屬性"></span>
### 邊緣函數執行時期額外支援的方法與屬性

在邊緣函數執行時期中，`WritableStream` 介面還額外支援以下方法。

<span id="waitclose"></span>
#### waitClose()

回傳一個 promise。當 stream 被寫入完畢或發生錯誤時，promise 會被 resolve。

<span id="writablestreamdefaultwriter"></span>
## WritableStreamDefaultWriter

參見 MDN 文件 [WritableStreamDefaultWriter](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在邊緣函數執行時期中，<code>WritableStreamDefaultWriter</code> 介面的 <code>desiredSize()</code> 方法和 <code>ready</code> 屬性未實作。</div>


<span id="正確處理-readablestream-和-writablestream"></span>
## 正確處理 ReadableStream 和 WritableStream

在邊緣函數執行時期中，`TransformStream` 介面的底層實作大量使用了零複製的方法，但仍然可能出現資料緩衝。為了防止因資料緩衝而導致的死鎖，建議您依照以下方法處理 `ReadableStream` 物件和 `WritableStream` 物件：


* 在同一個非同步函數中，避免同時使用 await 阻塞 `ReadableStream` 物件的方法和 `WritableStream` 物件的方法。這樣可能導致讀寫操作相互阻塞。

* 優先處理 `ReadableStream` 物件的方法確保資料持續流動。不要先使用 await 阻塞 `WritableStream` 物件的方法。

* 盡可能將 `WritableStream` 物件的方法封裝在獨立的非同步函數中。


下面的範例演示了如何正確處理 `ReadableStream` 物件和 `WritableStream` 物件。

```JavaScript
// 此範例演示自動產生資料用於回傳
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  const {readable, writable} = new TransformStream();
  async function controller() {
    const writer = writable.getWriter();
    for (let i = 0; i < 1000; ++i) {
      await writer.write('Hello World');
    }
    await writer.close();
  }

  // 注意不要 await 這個 controller，直接讓它在背景執行。如果 await 這個 controller，那麼
  // 取決於緩衝區大小，如果緩衝区很小，但是 await
  // write 的資料過大，就會導致死鎖，因為
  // await 的 promise 無法解析，而 readable 還沒有返回，沒有從 readable 讀取資料，那麼
  // writable 端就會阻塞在 write 上，整個函數就會被鎖住
  controller();

  return readable;
}

// 此範例會輸出 1000 次 Hello World
// 因 TransformStream 與 readable/writable 的關聯
// 無需 await controller，直接回傳 readable 即可
```
