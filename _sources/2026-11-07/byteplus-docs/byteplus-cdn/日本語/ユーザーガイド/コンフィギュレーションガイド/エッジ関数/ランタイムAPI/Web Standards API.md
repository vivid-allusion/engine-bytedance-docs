---
title: "Web Standards API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Web-standards-jp"
---

このドキュメントでは、エッジ関数ランタイムでサポートされている標準Web APIについて説明します。

<span id="textencoder-textdecoder"></span>
## TextEncoder/TextDecoder

TextEncoderは、UnicodeコードポイントをUTF\-8エンコードされたバイトストリームに変換することのみをサポートしています。TextDecoderは、UTF\-8、GB2312、およびGBKエンコードされたバイトストリームをUnicodeコードポイントに変換することのみをサポートしています。

[TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder)と[TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder)のMDNドキュメントを参照してください。

<span id="制限事項"></span>
### 制限事項


* サービス拒否（DoS）のリスクを防ぐため、各デコーダーの入力は8MBを超えてはいけません。

* マルチバイト文字列攻撃などの潜在的なリスクを防ぐため、ランタイムはTextEncoder/TextDecoderに制限を課す場合があります。例えば、バッファサイズを制限して、テキストの正確性とセキュリティを確保します。


<span id="settimeout-setimmediate-setinterval-cleartimeout-clearimmediate-clearinterval"></span>
## setTimeout()/setImmediate()/setInterval()/clearTimeout()/clearImmediate()/clearInterval()

これらのメソッドを使用して、指定した時間遅延後にコールバック関数を実行したり、指定した時間間隔で繰り返し実行したりすることができます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">高精度タイムスタンプに基づくサイドチャネル攻撃（スペクトル攻撃など）を防ぐため、これらのメソッドは積極的に時間精度を調整し、高精度クロックをサポートしていません。</div>


以下のMDNドキュメントを参照してください：


* [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setTimeout)

* [setImmediate()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setImmediate)

* [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/setInterval)

* [clearTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearTimeout)

* [clearImmediate()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearImmediate)

* [clearInterval()](https://developer.mozilla.org/en-US/docs/Web/API/Window/clearInterval)


<span id="制限事項"></span>
### 制限事項


* 各リクエストコンテキストにおいて、setTimeout()、setImmediate()、またはsetInterval()の累積呼び出し回数は1000回を超えることはできません。例えば、リクエストコンテキストでsetTimeout()が200回、setImmediate()が600回呼び出された場合、setInterval()は最大200回まで呼び出すことができます。

* 他のリクエストコンテキストで定義されたメソッドをsetTimeout()、setImmediate()、またはsetInterval()のパラメータとして渡すことはできません。また、他のリクエストコンテキストから取得したtimeoutID、immediateID、またはintervalIDをclearTimeout()、clearImmediate()、またはclearInterval()に渡すこともできません。


<span id="session"></span>
## session

ランタイムが各リクエストコンテキストに対して設定するオブジェクトです。各リクエストコンテキストには、他から見えないsessionグローバルオブジェクトがあります。sessionには以下のプロパティが含まれます：


* **requestId**: 現在のリクエストの一意のIDを返します。利用できない場合は空の文字列を返します。

* **event**: 現在のコンテキストのトリガーイベントを返します。これはaddEventListener()のコールバック関数内のイベントです。

* **context**: リクエストコンテキストから独立したオブジェクトで、ユーザーがリクエストコンテキストから独立したデータにアクセスするために使用されます。ランタイムに対して透過的です。


<span id="例"></span>
### 例

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

[atob()](https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/atob)と[btoa()](https://developer.mozilla.org/en-US/docs/Web/API/btoa)のMDNドキュメントを参照してください。

<span id="url"></span>
## URL

[URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)のMDNドキュメントを参照してください。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">セキュリティ上の理由から、URLの各部分にはメモリしきい値が設定されています。問題が発生した場合は、<a href="https://console.byteplus.com/workorder/create">チケットを作成</a>して設定を変更することができます。</div>


<span id="urlsearchparams"></span>
## URLSearchParams

[URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams)のMDNドキュメントを参照してください。

<span id="urlpattern"></span>
## URLPattern

[URLPattern](https://developer.mozilla.org/en-US/docs/Web/API/URLPattern)のMDNドキュメントを参照してください。

<span id="console"></span>
## console

[console](https://developer.mozilla.org/en-US/docs/Web/API/console)のMDNドキュメントを参照してください。

各リクエストコンテキストでconsoleに割り当てられるデフォルトのストレージ容量は1 KBです。1 KBを超えるデータは切り捨てられます。この制限はデバッグ環境では有効ではありません。

<span id="ランタイムでサポートされているインスタンスメソッド"></span>
### ランタイムでサポートされているインスタンスメソッド

consoleは以下のメソッドをサポートしています：


* info()

* log()

* error()

* warn()

* trace()

* assert()

* alert()


<span id="self"></span>
## self

現在のランタイムのグローバル変数を指す読み取り専用の変数です。

<span id="例"></span>
### 例

例えば、console.log()を呼び出してselfを出力する場合：

```javascript
console.log(self)
```


現在のランタイム内のすべてのオブジェクトを取得します。

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

現在の実行環境がエッジ関数ランタイムであるかどうかを示すブール型のグローバル変数です。これを使用して、コードがエッジ関数ランタイムで実行されているかどうかを判断できます。


* true: 現在の実行環境はエッジ関数ランタイムです。

* false: 現在の実行環境はエッジ関数ランタイムではありません。


<span id="structuredclone"></span>
## structuredClone()

[structuredClone()](https://developer.mozilla.org/en-US/docs/Web/API/structuredClone)のMDNドキュメントを参照してください。

<span id="queuemicrotask"></span>
## queueMicrotask()

[queueMicrotask()](https://developer.mozilla.org/en-US/docs/Web/API/queueMicrotask)のMDNドキュメントを参照してください。

<span id="navigator-useragent"></span>
## Navigator.userAgent

[Navigator.userAgent](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/userAgent)のMDNドキュメントを参照してください。

<span id="domexception"></span>
## DOMException

[DOMException](https://developer.mozilla.org/en-US/docs/Web/API/DOMException)のMDNドキュメントを参照してください。

<span id="event"></span>
## Event

[Event](https://developer.mozilla.org/en-US/docs/Web/API/Event)のMDNドキュメントを参照してください。

<span id="制限事項"></span>
### 制限事項


* [bubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/bubbles)プロパティはサポートされていません。

* [timestamp](https://developer.mozilla.org/en-US/docs/Web/API/Event/timeStamp)プロパティは0のみを返すことができます。

* [isTrusted](https://developer.mozilla.org/en-US/docs/Web/API/Event/isTrusted)プロパティはtrueのみを返すことができます。

* 以下の非推奨APIはサポートされていません：

   * [cancelBubble](https://developer.mozilla.org/en-US/docs/Web/API/Event/cancelBubble)

   * [returnValue](https://developer.mozilla.org/en-US/docs/Web/API/Event/returnValue)

   * [srcElement](https://developer.mozilla.org/en-US/docs/Web/API/Event/srcElement)

   * [initEvent](https://developer.mozilla.org/en-US/docs/Web/API/Event/initEvent)


<span id="eventtarget"></span>
## EventTarget

[EventTarget](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget)のMDNドキュメントを参照してください。

<span id="制限事項"></span>
### 制限事項


* EventTarget.addEventListener()のoptionsパラメータでは、passiveとcaptureはデフォルトでfalseに設定され、変更できません。

* EventTarget.removeEventListener()のoptionsパラメータでは、captureはデフォルトでfalseに設定され、変更できません。


<span id="abortsignal"></span>
## AbortSignal

[AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal)のMDNドキュメントを参照してください。

<span id="abortcontroller"></span>
## AbortController

[AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)のMDNドキュメントを参照してください。

<span id="url"></span>
## URL

[URL](https://developer.mozilla.org/en-US/docs/Web/API/URL)のMDNドキュメントを参照してください。
