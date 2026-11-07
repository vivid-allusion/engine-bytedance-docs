---
title: "CronEvent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-CronEvent-jp"
---

cronタイプのイベントは、Cronトリガーによってトリガーされます。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-addEventListener-jp">addEventListener()</a>を呼び出してcronイベントをリッスンするリスナーを登録し、<code>CronEvent</code>オブジェクトを取得する必要があります。</div>


<span id="メソッド"></span>
## メソッド

<span id="text"></span>
### text()

このメソッドは[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)を返します。Promiseが解決されると、返される値はCronトリガーで設定したカスタムパラメータで、[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)型です。Cronトリガーでカスタムパラメーターを設定する方法については、[Cronトリガー](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers-jp) を参照してください。

<span id="arraybuffer"></span>
### arrayBuffer()

このメソッドは[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)を返します。Promiseが解決されると、返される値はCronトリガーで設定したカスタムパラメータで、[ArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)型です。Cronトリガーでカスタムパラメーターを設定する方法については、[Cronトリガー](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers-jp) を参照してください。

<span id="stream"></span>
### stream()

このメソッドは[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)を返します。Promiseが解決されると、返される値はCronトリガーで設定したカスタムパラメータで、[ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream)型です。Cronトリガーでカスタムパラメーターを設定する方法については、[Cronトリガー](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers-jp) を参照してください。

<span id="json"></span>
### json()

このメソッドは[Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)を返します。Promiseが解決されると、返される値はCronトリガーで設定したカスタムパラメータで、[JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON)型です。Cronトリガーでカスタムパラメーターを設定する方法については、[Cronトリガー](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers-jp) を参照してください。

<span id="プロパティ"></span>
## プロパティ

<span id="job"></span>
### job

Cronトリガーの名前を返します。

<span id="cronexpression"></span>
### cronExpression

Cronトリガーのcron式を返します。

<span id="サンプルコード"></span>
## サンプルコード

```JavaScript
// イベントリスナーを登録して、cronイベントを監視する
addEventListener('cron', onCron);

// cronイベントがトリガーされたときに呼び出されるコールバック関数
async function onCron(event) {
    // ここにスケジュールされたタスクの具体的なコードを追加できます
    return 'Parameter: ' + await event.text();
}
```
