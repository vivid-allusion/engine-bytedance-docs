---
title: "Web Standards API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Web-standards"
---

This document introduces the standard Web APIs supported by the Edge Functions runtime.

<span id="textencoder-textdecoder"></span>
## TextEncoder/TextDecoder

TextEncoder only supports converting Unicode Codepoints to UTF\-8 encoded byte streams. TextDecoder only supports converting UTF\-8, GB2312, and GBK encoded byte streams to Unicode Codepoints.

Refer to MDN documentation for [TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder) and [TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder).

<span id="limitations"></span>
### Limitations


* To prevent Denial of Service (DoS) risks, each decoder input must not exceed 8MB.

* To guard against potential risks such as multi\-byte string attacks, the runtime may impose restrictions on TextEncoder/TextDecoder, such as limiting buffer size, to ensure text correctness and security.


<span id="settimeout-setimmediate-setinterval-cleartimeout-clearimmediate-clearinterval"></span>
## setTimeout()/setImmediate()/setInterval()/clearTimeout()/clearImmediate()/clearInterval()

You can use these methods to execute callback functions after a specified time delay or repeatedly at specified time intervals.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To prevent side\-channel attacks based on high\-precision timestamps (such as Spectrum attacks), these methods actively adjust time precision and do not support high\-precision clocks.</div>


Refer to the following MDN documentation:


* [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout)

* [setImmediate()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate)

* [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setInterval)

* [clearTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearTimeout)

* [clearImmediate()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearImmediate)

* [clearInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearInterval)


<span id="limitations"></span>
### Limitations


* In each request context, the cumulative number of calls to setTimeout(), setImmediate(), or setInterval() cannot exceed 1000 times. For example, if setTimeout() is called 200 times and setImmediate() is called 600 times in a request context, setInterval() can be called at most 200 times.

* You cannot pass methods defined in other request contexts as parameters to setTimeout(), setImmediate(), or setInterval(), nor can you pass timeoutID, immediateID, or intervalID obtained from other request contexts to clearTimeout(), clearImmediate(), or clearInterval().


<span id="session"></span>
## session

An object set by the runtime for each request context. Each request context has a session global object that is invisible to others. The session includes the following properties:


* **requestId**: Returns the unique ID of the current request, or an empty string if not available.

* **event**: Returns the trigger event of the current context, which is the event in the callback function of addEventListener().

* **context**: An object independent of the request context, used for users to access data independent of the request context, transparent to the runtime.


<span id="example"></span>
### Example

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  const table = session.context; // The context of each requests is independent

  table.set("my-own-data", session.requestId);
}
```


<span id="atob-btoa"></span>
## atob()/btoa()

Refer to MDN documentation for [atob()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/atob) and [btoa()](https://developer.mozilla.org/en-US/docs/Web/API/btoa).

<span id="url"></span>
## URL

Refer to MDN documentation for [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For security reasons, each part of the URL has a memory threshold set. If you encounter any issues, you can <a href="https://console.byteplus.com/workorder/create">create a ticket</a> to change the configuration.</div>


<span id="urlsearchparams"></span>
## URLSearchParams

Refer to MDN documentation for [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams).

<span id="urlpattern"></span>
## URLPattern

Refer to MDN documentation for [URLPattern](https://developer.mozilla.org/en-US/docs/Web/API/URLPattern).

<span id="console"></span>
## console

Refer to MDN documentation for [console](https://developer.mozilla.org/en-US/docs/Web/API/console).

The default storage capacity allocated to console in each request context is 1 KB. Data exceeding 1 KB will be truncated. This limitation is not effective in the debugging environment.

<span id="instance-methods-supported-by-the-runtime"></span>
### Instance methods supported by the runtime

console supports the following methods:


* info()

* log()

* error()

* warn()

* trace()

* assert()

* alert()


<span id="self"></span>
## self

A read\-only variable that points to the current runtime global variables.

<span id="example"></span>
### Example

For example, if you call console.log() to print self:

```javascript
console.log(self)
```


You will get all objects within the current runtime.

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

A Boolean global variable that indicates whether the current running environment is the edge function runtime. You can use it to determine if the code is running in the edge function runtime.


* true: The current running environment is the edge function runtime.

* false: The current running environment is not the edge function runtime.


<span id="structuredclone"></span>
## structuredClone()

Refer to MDN documentation for [structuredClone()](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone).

<span id="queuemicrotask"></span>
## queueMicrotask()

Refer to MDN documentation for [queueMicrotask()](https://developer.mozilla.org/en-US/docs/Web/API/queueMicrotask).

<span id="navigator-useragent"></span>
## Navigator.userAgent

Refer to MDN documentation for [Navigator.userAgent](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent).

<span id="domexception"></span>
## DOMException

Refer to MDN documentation for [DOMException](https://developer.mozilla.org/en-US/docs/Web/API/DOMException).

<span id="event"></span>
## Event

Refer to MDN documentation for [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event).

<span id="limitations"></span>
### Limitations


* The [bubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles) property is not supported.

* The [timestamp](https://developer.mozilla.org/en-US/docs/Web/API/Event/timeStamp) property can only return 0.

* The [isTrusted](https://developer.mozilla.org/en-US/docs/Web/API/Event/isTrusted) property can only return true.

* The following deprecated APIs are not supported:

   * [cancelBubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/cancelBubble)

   * [returnValue](https://developer.mozilla.org/en-US/docs/Web/API/Event/returnValue)

   * [srcElement](https://developer.mozilla.org/en-US/docs/Web/API/Event/srcElement)

   * [initEvent](https://developer.mozilla.org/en-US/docs/Web/API/Event/initEvent)


<span id="eventtarget"></span>
## EventTarget

Refer to MDN documentation for [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget).

<span id="limitations"></span>
### Limitations


* In the options parameter of EventTarget.addEventListener(), passive and capture are set to false by default and cannot be changed.

* In the options parameter of EventTarget.removeEventListener(), capture is set to false by default and cannot be changed.


<span id="abortsignal"></span>
## AbortSignal

Refer to MDN documentation for [AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal).

<span id="abortcontroller"></span>
## AbortController

Refer to MDN documentation for [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController).

<span id="url"></span>
## URL

Refer to MDN documentation for [URL](https://developer.mozilla.org/en-US/docs/Web/API/URL).
