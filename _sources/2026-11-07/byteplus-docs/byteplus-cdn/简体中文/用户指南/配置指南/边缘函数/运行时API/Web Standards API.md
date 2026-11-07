---
title: "Web Standards API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-Web-standards-cn"
---

本文档介绍边缘函数运行时支持的标准 Web API。

<span id="textencoder-textdecoder"></span>
## TextEncoder/TextDecoder

`TextEncoder` 仅支持把 Unicode Codepoint 转换为 UTF\-8 编码的字节流。`TextDecoder` 仅支持把 UTF\-8、GB2312、GBK 编码的字节流转换为 Unicode Codepoint。

参见 MDN 文档 [TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder) 和 [TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder)。

<span id="限制"></span>
### 限制


* 为了防止 Denial of Service (DoS) 风险，每次 `decoder` 的输入数据不得超过 8MB。

* 为了防范多字节字符串攻击等潜在风险，运行时可能会对 `TextEncoder`/`TextDecoder` 进行限制，例如限制缓冲区大小，以确保文本的正确性和安全性。


<span id="settimeout-setimmediate-setinterval-cleartimeout-clearimmediate-clearinterval"></span>
## setTimeout()/setImmediate()/setInterval()/clearTimeout()/clearImmediate()/clearInterval()

您可以使用这些方法在指定的时间延迟后执行回调函数，或者在指定的时间间隔内重复执行回调函数。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">为了防止基于高精度时间戳的侧信道攻击（例如 Spectrum 攻击），这些方法会主动调整时间精度，不支持高精度时钟。</div>


参见以下 MDN 文档：


* [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout)

* [setImmediate()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setImmediate)

* [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setInterval)

* [clearTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearTimeout)

* [clearImmediate()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearImmediate)

* [clearInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearInterval)


<span id="限制"></span>
### 限制


* 在每个请求上下文中，`setTimeout()`、`setImmediate()` 或 `setInterval()` 的累积调用次数不能超过 1000 次。例如，在一个请求上下文中，`setTimeout()` 被调用 200 次，`setImmediate()` 被调用 600 次，则 `setInterval()` 最多只能被调用 200 次。

* 你不能把在其他请求上下文中定义的方法作为参数传入 `setTimeout()`、`setImmediate()` 或 `setInterval()`，也不能把在其他请求上下文中获取的 `timeoutID`、`immediateID` 或 `intervalID` 传入 `clearTimeout()`、`clearImmediate()` 或 `clearInterval()`。


<span id="session"></span>
## session

运行时为每个请求上下文设置的对象，每个请求上下文有一个互相不可见的 `session` 全局对象。`session` 包含以下属性：


* requestId：返回当前请求的唯一 ID，如果没有则为空字符串。

* event：返回当前上下文的触发事件，即 `addEventListener()` 中回调函数的 `event`。

* context：独立于请求上下文的对象，用于用户访问独立于请求上下文的数据，对运行时透明。


<span id="示例"></span>
### 示例

```JavaScript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  const table = session.context; // 每次请求的context都是不一样的，互相独立

  table.set("my-own-data", session.requestId);
}
```


<span id="atob-btoa"></span>
## atob()/btoa()

参见 MDN 文档 [atob()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/atob)、[btoa()](https://developer.mozilla.org/en-US/docs/Web/API/btoa)。

<span id="url"></span>
## URL

参见 MDN 文档 [URL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">出于安全原因，<code>URL</code> 的每个部分都有内存阈值设置，如果您遇到问题，可以通过<a href="https://console.byteplus.com/workorder/create">创建工单</a>更改配置。</div>


<span id="urlsearchparams"></span>
## URLSearchParams

参见 MDN 文档 [URLSearchParams](https://developer.mozilla.org/zh-CN/docs/Web/API/URLSearchParams)。

<span id="urlpattern"></span>
## URLPattern

参见 MDN 文档 [URLPattern](https://developer.mozilla.org/en-US/docs/Web/API/URLPattern)。

<span id="console"></span>
## console

参见 MDN 文档 [console](https://developer.mozilla.org/en-US/docs/Web/API/console)。

`console` 在每个请求上下文中被分配的存储容量默认为 1 KB，超过 1KB 的数据会被截断。该限制在调试环境下不生效。

<span id="运行时支持的实例方法"></span>
### 运行时支持的实例方法

`console` 支持以下方法：


* `info()`

* `log()`

* `error()`

* `warn()`

* `trace()`

* `assert()`

* `alert()`


<span id="self"></span>
## self

一个指向当前运行时全局变量的只读变量。

<span id="示例"></span>
### 示例

例如，如果您调用 `console.log()` 打印 `self`：

```javascript
console.log(self)
```


您会得到当前运行时范围内的所有对象：

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

一个 `Boolean` 全局变量，表示当前运行环境是否边缘函数的运行时。您可以使用它来确定代码是否在边缘函数运行时中运行。


* `true`：当前运行环境是边缘函数的运行时。

* `false`：当前运行环境不是边缘函数的运行时。


<span id="structuredclone"></span>
## structuredClone()

参见 MDN 文档 [structuredClone()](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)。

<span id="queuemicrotask"></span>
## queueMicrotask()

参见 MDN 文档 [queueMicrotask()](https://developer.mozilla.org/en-US/docs/Web/API/queueMicrotask)。

<span id="navigator-useragent"></span>
## Navigator.userAgent

参见 MDN 文档 [Navigator.userAgent](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent)。

<span id="domexception"></span>
## DOMException

参见 MDN 文档 [DOMException](https://developer.mozilla.org/en-US/docs/Web/API/DOMException)。

<span id="event"></span>
## Event

参见 MDN 文档 [Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)。

<span id="限制"></span>
### 限制


* 不支持 [bubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles) 属性。

* [timestamp](https://developer.mozilla.org/en-US/docs/Web/API/Event/timeStamp) 属性只能返回 0。

* [isTrusted](https://developer.mozilla.org/en-US/docs/Web/API/Event/isTrusted) 属性只能返回 `true`。

* 不支持以下废弃 API：

   * [cancelBubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/cancelBubble)

   * [returnValue](https://developer.mozilla.org/en-US/docs/Web/API/Event/returnValue)

   * [srcElement](https://developer.mozilla.org/en-US/docs/Web/API/Event/srcElement)

   * [initEvent](https://developer.mozilla.org/en-US/docs/Web/API/Event/initEvent)


<span id="eventtarget"></span>
## EventTarget

参见 MDN 文档 [EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)。

<span id="限制"></span>
### 限制


* `EventTarget.addEventListener()` 的 `options` 参数中的 `passive` 和 `capture` 默认被设置为 `false` 且无法更改。

* `EventTarget.removeEventListener()` 的 `options` 参数中的 `capture` 默认被设置为 `false` 且无法更改。


<span id="abortsignal"></span>
## AbortSignal

参见 MDN 文档 [AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)。

<span id="abortcontroller"></span>
## AbortController

参见 MDN 文档 [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)。

<span id="url"></span>
## URL

参见 MDN 文档 [URL](https://developer.mozilla.org/zh-CN/docs/Web/API/URL)。
