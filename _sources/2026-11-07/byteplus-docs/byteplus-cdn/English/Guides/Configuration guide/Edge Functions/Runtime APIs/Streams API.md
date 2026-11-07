---
title: "Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams"
---

The [Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API) allows you to access and process data streams received from the network. The edge function runtime supports the following Streams API.

<span id="transformstream"></span>
## TransformStream

Refer to the MDN documentation [TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the Edge Functions runtime, you can only create <code>TransformStream</code> objects using the <code>TransformStream()</code> constructor.</div>


<span id="readablestream"></span>
## ReadableStream

Refer to the MDN documentation [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The Edge Functions runtime does not allow you to create <code>ReadableStream</code> objects using the <code>ReadableStream()</code> constructor. You can only obtain <code>ReadableStream</code> objects via the <code>readable</code> property of a <a href="https://docs.byteplus.com/en/docs/18/17395#transformstream">TransformStream</a> object.</div>


* <div data-tips="true" data-tips-type="warning">The <a href="https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/tee">ReadableStream.tee()</a> method consumes memory. You need to prevent the function's runtime from returning an OOM error due to memory exceeding <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/Usage_Limits_Functions">Usage Limits</a>.</div>



<span id="additional-methods-and-properties-supported-by-the-edge-functions-runtime"></span>
### Additional methods and properties supported by the Edge Functions Runtime

In the Edge Functions runtime, the `ReadableStream` interface also supports the following additional methods and properties.

<span id="waitclose"></span>
#### waitClose()

Returns a promise. The promise is resolved when the stream is fully read or encounters an error while reading.

<span id="finished"></span>
#### finished

Indicates whether the stream has been fully read or encountered an error while reading.


* true: The stream has been fully read or encountered an error while reading.

* false: The stream has not been fully read.


<span id="readablestreamdefaultreader"></span>
## ReadableStreamDefaultReader

Refer to the MDN documentation [ReadableStreamDefaultReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader).

<span id="writablestream"></span>
## WritableStream

Refer to the MDN documentation [WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Edge Functions runtime does not allow you to create <code>WritableStream</code> objects using the <code>WritableStream()</code> constructor. You can only obtain <code>WritableStream</code> objects via the <code>writable</code> property of a <a href="https://docs.byteplus.com/en/docs/18/17395#transformstream">TransformStream</a> object.</div>


<span id="additional-methods-and-properties-supported-by-the-edge-functions-runtime"></span>
### Additional methods and properties supported by the Edge Functions Runtime

In the Edge Functions runtime, the `WritableStream` interface also supports the following additional methods.

<span id="waitclose"></span>
#### waitClose()

Returns a promise. The promise is resolved when the stream is fully read or encounters an error while reading.

<span id="writablestreamdefaultwriter"></span>
## WritableStreamDefaultWriter

Refer to the MDN documentation [WritableStreamDefaultWriter](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the Edge Functions runtime, the <code>desiredSize()</code> method and <code>ready</code> property of the <code>WritableStreamDefaultWriter</code> interface are not implemented.</div>


<span id="properly-handle-readablestream-and-writablestream"></span>
## Properly handle ReadableStream and WritableStream

In the Edge Functions runtime, the underlying implementation of the `TransformStream` interface extensively uses zero\-copy methods, but data buffering may still occur. To prevent deadlocks caused by data buffering, it is recommended that you handle `ReadableStream` and `WritableStream` objects as follows:


* In the same asynchronous function, avoid using `await` to block methods of both `ReadableStream` objects and `WritableStream` objects simultaneously. This can cause read and write operations to block each other.

* Prioritize processing methods of `ReadableStream` objects to ensure continuous data flow. Do not block methods of `WritableStream` objects with `await` first.

* Encapsulate methods of `WritableStream` objects in separate asynchronous functions whenever possible.


The following example demonstrates how to correctly handle `ReadableStream` and `WritableStream` objects.

```JavaScript
// This example demonstrates auto-generating data to send a response.
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

  // Note: Do not await this controller; let it run in the background. If you await this controller,
  // depending on the buffer size, if the buffer is small but the data being awaited by write
  // is too large, it will cause a deadlock. This is because
  // the awaited promise cannot resolve, and readable has not yet returned, so no data is being read from readable.
  // Consequently, the writable end will block on write, and the entire function will be locked.
  controller();

  return readable;
}

// The example above outputs "Hello World" 1000 times.
// Because of the association between TransformStream and readable/writable, there is no need to await
// the controller. Simply returning readable is sufficient. The controller will automatically complete its execution,
// and continuous reading from readable will ensure the controller runs automatically in the background.
```
