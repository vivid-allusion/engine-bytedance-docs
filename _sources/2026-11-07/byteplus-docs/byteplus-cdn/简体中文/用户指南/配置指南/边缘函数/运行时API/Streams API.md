---
title: "Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Streams-cn"
---

[Streams API](https://developer.mozilla.org/zh-CN/docs/Web/API/Streams_API) 允许您访问并处理从网络接收的数据流。边缘函数的运行时支持以下 Streams API。

<span id="transformstream"></span>
## TransformStream

参见 MDN 文档 [TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在边缘函数运行时中，您只能通过构造函数 <code>TransformStream()</code> 创建 <code>TransformStream</code> 对象。</div>


<span id="readablestream"></span>
## ReadableStream

参见 MDN 文档 [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">边缘函数运行时不允许您使用构造函数 <code>ReadableStream()</code> 创建 <code>ReadableStream</code> 对象。您只能通过 <a href="https://docs.byteplus.com/en/docs/18/20508#transformstream">TransformStream</a> 对象的 <code>readable</code> 属性获取 <code>ReadableStream</code> 对象。</div>


* <div data-tips="true" data-tips-type="warning"><a href="https://developer.mozilla.org/zh-CN/docs/Web/API/ReadableStream/tee">ReadableStream.tee()</a> 方法会占用内存。您需要避免函数的运行时由于内存超出<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/functions-usage-limits">限制</a>而返回 OOM 错误。</div>



<span id="边缘函数运行时额外支持的方法和属性"></span>
### 边缘函数运行时额外支持的方法和属性

在边缘函数运行时中，`ReadableStream` 接口还额外支持以下方法和属性。

<span id="waitclose"></span>
#### waitClose()

返回一个 promise。当该 stream 被读取完毕或读取出错的时候，promise 被 resolve。

<span id="finished"></span>
#### finished

表示 stream 是否被读取完毕或读取出错。


* true ：stream 被读取完毕或读取出错。

* false：stream 没有被读取完毕。


<span id="readablestreamdefaultreader"></span>
## ReadableStreamDefaultReader

参见 MDN 文档 [ReadableStreamDefaultReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader)。

<span id="writablestream"></span>
## WritableStream

参见 MDN 文档 [WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">边缘函数运行时不允许您使用构造函数 <code>WritableStream()</code> 创建 <code>WritableStream</code> 对象。您只能通过 <a href="https://docs.byteplus.com/en/docs/18/20508#transformstream">TransformStream</a> 对象的 <code>writable</code> 属性获取 <code>WritableStream</code> 对象。</div>


<span id="边缘函数运行时额外支持的方法和属性"></span>
### 边缘函数运行时额外支持的方法和属性

在边缘函数运行时中，`WritableStream` 接口还额外支持以下方法。

<span id="waitclose"></span>
#### waitClose()

返回一个 promise。当该 stream 被读取完毕或读取出错的时候，promise 被 resolve。

<span id="writablestreamdefaultwriter"></span>
## WritableStreamDefaultWriter

参见 MDN 文档 [WritableStreamDefaultWriter](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在边缘函数运行时中，<code>WritableStreamDefaultWriter</code> 接口的 <code>desiredSize()</code> 方法和 <code>ready</code> 属性未实现。</div>


<span id="正确处理-readablestream-和-writablestream"></span>
## 正确处理 ReadableStream 和 WritableStream

在边缘函数运行时中，`TransformStream` 接口的底层实现大量使用了零拷贝的方法，但仍然可能出现数据缓冲。为了防止因数据缓冲而导致的死锁，建议您按以下方法处理 `ReadableStream` 对象和 `WritableStream` 对象：


* 在同一个异步函数中，避免同时使用 await 阻塞 `ReadableStream` 对象的方法和 `WritableStream` 对象的方法。这样可能导致读写操作相互阻塞。

* 优先处理 `ReadableStream` 对象的方法确保数据持续流动。不要先使用 await 阻塞 `WritableStream` 对象的方法。

* 尽可能将 `WritableStream` 对象的方法封装在独立的异步函数中。


下面的示例演示了如何正确处理 `ReadableStream` 对象和 `WritableStream` 对象。

```JavaScript
// 这个例子演示自动生成数据，用于发送回复
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

  // 注意不要await这个controller，直接让其在后台运行。如果await这个controller，那么
  // 取决于buffer大小，如果buffer很小，但是await
  // write的数据过大，就会导致死锁，因为
  // await的promise无法resolve，而readable还没有返回，没有从readable读数据，那么
  // writable端就会阻塞在write上，整个函数就会被锁住
  controller();

  return readable;
}

// 上述例子输出了一个1000次的Hello
// World，因为TransformStream和readable/writable的关联，不需要await
// controller，而直接返回readable即可，controller会自动运行完毕，
// readable不断读取会保证controller在后台的自动运行
```
