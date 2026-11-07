---
title: "Streams API"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams-jp"
---

[Streams API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)を使用すると、ネットワークから受信したデータストリームにアクセスして処理することができます。エッジ関数ランタイムは、以下のStreams APIをサポートしています。

<span id="transformstream"></span>
## TransformStream

MDNドキュメントの[TransformStream](https://developer.mozilla.org/en-US/docs/Web/API/TransformStream)を参照してください。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">エッジ関数ランタイムでは、コンストラクタ <code>TransformStream()</code> を使用してのみ <code>TransformStream</code> オブジェクトを作成できます。</div>


<span id="readablestream"></span>
## ReadableStream

MDNドキュメントの[ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)を参照してください。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">エッジ関数ランタイムでは、コンストラクタ <code>ReadableStream()</code> を使用して <code>ReadableStream</code> オブジェクトを作成することはできません。<a href="https://docs.byteplus.com/en/docs/18/36563#transformstream">TransformStream</a> オブジェクトの <code>readable</code> プロパティを介してのみ <code>ReadableStream</code> オブジェクトを取得できます。</div>


* <div data-tips="true" data-tips-type="warning"><a href="https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream/tee">ReadableStream.tee()</a> メソッドはメモリを消費します。関数のランタイムがメモリ制限を超過し、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/usage-limits-jp">エッジ関数の使用制限</a>によりOOMエラーが返されるのを避ける必要があります。</div>



<span id="エッジ関数ランタイムで追加サポートされるメソッドとプロパティ"></span>
### エッジ関数ランタイムで追加サポートされるメソッドとプロパティ

エッジ関数ランタイムでは、`ReadableStream` インターフェースは以下のメソッドとプロパティをさらにサポートします。

<span id="waitclose"></span>
#### waitClose()

プロミスを返します。ストリームが完全に読み取られたか、読み取り中にエラーが発生した場合にプロミスが解決されます。

<span id="finished"></span>
#### finished

ストリームが完全に読み取られたか、読み取り中にエラーが発生したかを示します。


* true: ストリームが完全に読み取られたか、読み取り中にエラーが発生しました。

* false: ストリームはまだ完全に読み取られていません。


<span id="readablestreamdefaultreader"></span>
## ReadableStreamDefaultReader

MDNドキュメントの[ReadableStreamDefaultReader](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStreamDefaultReader)を参照してください。

<span id="writablestream"></span>
## WritableStream

MDNドキュメントの[WritableStream](https://developer.mozilla.org/en-US/docs/Web/API/WritableStream)を参照してください。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">エッジ関数ランタイムでは、コンストラクタ <code>WritableStream()</code> を使用して <code>WritableStream</code> オブジェクトを作成することはできません。<a href="https://docs.byteplus.com/en/docs/18/36563#transformstream">TransformStream</a> オブジェクトの <code>writable</code> プロパティを介してのみ <code>WritableStream</code> オブジェクトを取得できます。</div>


<span id="エッジ関数ランタイムで追加サポートされるメソッドとプロパティ"></span>
### エッジ関数ランタイムで追加サポートされるメソッドとプロパティ

エッジ関数ランタイムでは、`WritableStream` インターフェースは以下のメソッドをさらにサポートします。

<span id="waitclose"></span>
#### waitClose()

プロミスを返します。ストリームが完全に読み取られたか、読み取り中にエラーが発生した場合にプロミスが解決されます。

<span id="writablestreamdefaultwriter"></span>
## WritableStreamDefaultWriter

MDNドキュメントの[WritableStreamDefaultWriter](https://developer.mozilla.org/en-US/docs/Web/API/WritableStreamDefaultWriter)を参照してください。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">エッジ関数ランタイムでは、<code>WritableStreamDefaultWriter</code> インターフェースの <code>desiredSize()</code> メソッドと <code>ready</code> プロパティは実装されていません。</div>


<span id="readablestreamとwritablestreamの適切な処理"></span>
## ReadableStreamとWritableStreamの適切な処理

エッジ関数ランタイムでは、`TransformStream` インターフェースの基盤となる実装はゼロコピー方式を多用していますが、依然としてデータバッファリングが発生する可能性があります。データバッファリングによるデッドロックを防ぐために、`ReadableStream` オブジェクトと `WritableStream` オブジェクトを次の方法で処理することをお勧めします。


* 同じ非同期関数内で、`ReadableStream` オブジェクトのメソッドと `WritableStream` オブジェクトのメソッドを同時に `await` でブロックしないでください。これにより、読み取り操作と書き込み操作が相互にブロックされる可能性があります。

* データの継続的なフローを確保するために、`ReadableStream` オブジェクトのメソッドを優先的に処理してください。最初に `await` で `WritableStream` オブジェクトのメソッドをブロックしないでください。

* 可能な限り、`WritableStream` オブジェクトのメソッドを独立した非同期関数にカプセル化してください。


次の例は、`ReadableStream` オブジェクトと `WritableStream` オブジェクトを正しく処理する方法を示しています。

```JavaScript
// この例は、レスポンスを送信するためにデータを自動生成する方法を示しています。
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

  // 注意：このコントローラーをawaitしないで、バックグラウンドで実行させてください。このコントローラーをawaitすると、
  // バッファサイズに依存しますが、バッファが小さく、writeによってawaitされるデータが大きすぎる場合、
  // デッドロックが発生します。これは、awaitされたプロミスが解決できず、readableがまだ返されておらず、
  // readableからデータが読み取られていないためです。
  // その結果、書き込み可能な側はwriteでブロックされ、関数全体がロックされます。
  controller();

  return readable;
}

// 上記の例では、「Hello World」を1000回出力します。
// TransformStreamとreadable/writableの関連付けにより、コントローラーをawaitする必要はありません。
// readableを直接返すだけで十分です。コントローラーは自動的に実行を完了し、
// readableからの継続的な読み取りにより、コントローラーはバックグラウンドで自動的に実行されます。
```
