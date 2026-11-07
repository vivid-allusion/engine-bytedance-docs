---
title: "createHtmlStream()"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/function-createHtmlStream-jp"
---

ストリームHTMLドキュメントを解析し、書き換えます。

このメソッドを使用して、CSSセレクターのコールバック関数を登録できます。このメソッドが呼び出されると、エッジ関数ランタイムは組み込みのHTMLパーサーを使用してHTMLドキュメントを解析します。HTMLパーサーがCSSセレクターに一致する要素を解析すると、HTMLドキュメントまたはHTML要素を処理するためのコールバック関数が呼び出されます。これらのコールバック関数を使用して、要素の前後にコンテンツを挿入したり、要素の属性を変更したり、要素を削除したりできます。

<span id="構文"></span>
## 構文

```JavaScript
createHtmlStream(ReadableStream, Object | null, Object | null)
```


<span id="パラメータ"></span>
## パラメータ

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">パラメータは順番に指定する必要があり、中間のパラメータを省略することはできません。</div>



* 最初のパラメータは、書き換え対象のストリーミングHTMLドキュメントを表す[ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams-jp#readablestream)オブジェクトです。この`ReadableStream`オブジェクトは読み取ったりキャンセルしたりすることはできません。このパラメータは必須です。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>createHtmlStream()</code> は、読み取られたまたはキャンセルされた <code>ReadableStream</code> オブジェクトを渡すことを許可していません。   </div>
   

* 2番目のパラメータは、HTMLドキュメントレベルの解析イベントハンドラーを表す[DocumentHandler](https://docs.byteplus.com/en/docs/18/36569#documenthandler)オブジェクトです。HTMLドキュメントレベルの解析イベントをリッスンする必要がない場合は、このパラメータに`undefined`または`null`を渡すことができます。

* 3番目のパラメータは配列で、各要素は2つの要素を含むサブ配列です。HTML要素の解析イベントハンドラーを設定する必要がない場合は、このパラメータに`undefined`または`null`を渡すことができます。このサブ配列に含まれる2つの要素は、次のものを表します。

   * [CSSセレクターで選択されたタグ](https://docs.byteplus.com/en/docs/18/36569#css)。CSSセレクターはHTML要素を照合するために使用されます。

   * CSSセレクターに一致する[ElementHandler](https://docs.byteplus.com/en/docs/18/36569#elementhandler)オブジェクト。CSSセレクターによって照合されたDOM要素の解析イベントをリッスンおよび処理するために使用されるHTML要素レベルの解析イベントハンドラーを表します。


<span id="戻り値"></span>
## 戻り値

このメソッドは、処理されたストリーミングHTMLドキュメントを表す[ReadableStream](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-Streams-jp#readablestream)オブジェクトを返します。このメソッドが返す`ReadableStream`オブジェクトをクライアントへの応答として返すことができます。

<span id="エラー処理"></span>
## エラー処理

コールバック関数でスローされた例外はストリーム全体が中断されます。これを回避するには、コールバック関数内でtry...catchステートメントを使用して例外をキャッチして処理することをお勧めします。

<span id="サンプルコード"></span>
# サンプルコード

`createHtmlStream()`メソッドを使用してストリーミングHTMLページを書き換える方法を理解するには、次のサンプルコードを参照してください。

<span id="htmlの外部リンクを書き換える"></span>
### HTMLの外部リンクを書き換える

WebサイトでIPv6が有効になっている場合、ページ内の外部リンクを通じて参照されるサードパーティリソースがIPv4のみをサポートしていると、純粋なIPv6ネットワーク環境のユーザーはこれらのリソースにアクセスできなくなります。これにより、コンテンツを読み込めないページの空白領域が発生します。この問題を解決するための効果的な解決策は、これらの外部リンクをIPv4/IPv6デュアルスタックをサポートするIP転送サービスにリダイレクトすることです。このサービスはIPv6ユーザーからのリクエストを受け取り、ユーザーに代わってIPv4のみをサポートするリソースにアクセスし、結果をユーザーに返します。

次のサンプルコードは、`createHtmlStream()`メソッドを使用してページ上のすべての `<a>` タグの `href` 属性を照合および変更し、リンクを指定したIP転送サービスアドレスにリダイレクトする方法を示しています。`createHtmlStream()` メソッドは、ゼロコピープリンシパルに基づいてエッジ関数ランタイム内でストリーミングHTMLを処理し、Webページによって読み込まれるJavaScriptコードに依存しないため、Time to First Byte（TTFB）に影響しません。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 元のHTMLページをフェッチします。
  const req = await fetch('https://origin.example.com');

  // CSSセレクターを介して書き換える要素を照合し、HTMLページコンテンツを書き換えます。
  const htmlStream = createHtmlStream(
      req.body,  // パラメーター1：書き換えるReadableStreamオブジェクト、つまりオリジン応答の本文。
      undefined, // パラメーター2：ここでは使用されないドキュメントレベルのハンドラー。
      [['a',      // パラメーター3：CSSセレクターと対応するハンドラーを含む配列。
        {
          // onElementハンドラー：<a>タグが解析されるとトリガーされます。
          onElement(element) {
            console.assert(element.tagName == 'a');
            if (element.hasAttribute('href')) {
              const href = element.getAttribute('href');
              // href属性値をIP転送サービスのアドレスに変更します。
              element.setAttribute(
                  'href', `https://ipforwardservice.example.com?url=${href}` );
            }
          }
        }
      ]]);

  // 変更されたReadableStreamオブジェクトをクライアントへの応答として返します。
  return htmlStream;
}
```


<span id="コンテンツを非同期に取得し、取得したコンテンツをhtmlに挿入する"></span>
### コンテンツを非同期に取得し、取得したコンテンツをHTMLに挿入する

`createHtmlStream()` メソッドを使用すると、エッジノードでHTML応答を動的に変更できます。一般的なアプリケーションは、HTMLでプレースホルダータグを定義し、エッジでデータを非同期にフェッチしてから、フェッチしたデータをHTMLに挿入してプレースホルダーを置き換えることです。この方法を使用すると、アプリケーションサービスロジックを変更せずに動的コンテンツを配信できます。

たとえば、HTMLページにカスタムの `<fetch>` タグが含まれているとします。このタグの `url` 属性が指すコンテンツをエッジノードでフェッチし、タグをフェッチしたコンテンツに置き換えたいとします。

**処理前**

```html
<html>
  <head></head>
  <body>
    <!-- ページにカスタムのfetchタグが含まれています -->
    <fetch url="https://api.example.com/data"></fetch>
  </body>
</html>
```


**処理後**

```html
<html>
  <head></head>
  <body>
  <!-- fetchタグは、そのURLが指すコンテンツに置き換えられます -->
    data
  </body>
</html>
```


次のサンプルコードは、上記のエフェクトを実現する方法を示しています。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 元のHTMLページをフェッチします。
  const req = await fetch(event.request);

  // CSSセレクターを介して書き換える要素を照合し、HTMLページコンテンツを書き換えます。
  const htmlStream = createHtmlStream(
      req.body,  // パラメーター1：書き換えるReadableStreamオブジェクト。
      undefined, // パラメーター2：ここでは使用されないドキュメントレベルのハンドラー。
      [[
        'fetch', // パラメーター3：CSSセレクター。ここではすべての<fetch>タグに一致します。
        {
          // onElementハンドラー：<fetch>タグが解析されるとトリガーされます。
          async onElement(element) {
            console.assert(element.tagName == 'fetch');
            if (element.hasAttribute('url')) {
              const url = element.getAttribute('url');
              // URLが指すコンテンツを非同期にフェッチします。
              const content = await fetch(url);
              const text = await content.text();
              // フェッチしたコンテンツで<fetch>タグを置き換えます。
              element.replace(text, {isHtml: true});
            }
          }
        }
      ]]);

  // 変更されたReadableStreamオブジェクトをクライアントへの応答として返します。
  return htmlStream;
}
```


<span id="解析イベントハンドラー"></span>
# 解析イベントハンドラー

<span id="documenthandler"></span>
## DocumentHandler

HTMLドキュメントレベルの解析イベントハンドラーで、`<html>`タグ外のコンテンツを含むHTMLドキュメントのすべての解析イベントを処理するために使用されます。

次のコールバック関数を使用できます。各コールバック関数はオプションであり、各コールバック関数は非同期関数にすることができます。HTMLドキュメント解析イベントハンドラーのコールバック関数は、CSSセレクターによってトリガーされません。

<span id="ondoctype-doctype"></span>
### onDoctype(doctype)

HTMLドキュメントのDOCTYPEノードが解析されるときに呼び出されます。

<span id="パラメータ"></span>
#### パラメータ

`doctype`: [HtmlDoctype](https://docs.byteplus.com/en/docs/18/36569#htmldoctype)オブジェクト。

<span id="ondocend-docend"></span>
### onDocend(docend)

HTMLドキュメント全体が解析されたときに呼び出されます。このコールバックの唯一の機能は、HTMLドキュメントにフッターを追加することです。

<span id="パラメータ"></span>
#### パラメータ

`docend`: [HtmlDocend](https://docs.byteplus.com/en/docs/18/36569#htmldocend)オブジェクト。

<span id="oncomment-comment"></span>
### onComment(comment)

HTMLドキュメントのコメントノードが解析されるときに呼び出されます。

<span id="パラメータ"></span>
#### パラメータ

`comment`: [HtmlComment](https://docs.byteplus.com/en/docs/18/36569#htmlcomment)オブジェクト。

<span id="ontext-text"></span>
### onText(text)

HTMLドキュメントのテキストノードが解析されるときに呼び出されます。

テキストノードのコンテンツは、ストリーミング解析中に複数のフラグメントで送信される場合があるため、同じテキストノードに対して`onText()`が複数回呼び出されることがあります。たとえば、HTML `<html>This is long text</html>`の場合、`This is long text`が2つの部分で返されると、`This is long text`はテキストノードですが、`onText()`は2回呼び出されます。[lastInTextNode](https://docs.byteplus.com/en/docs/18/36569#lastintextnode)属性を使用して、最後の呼び出しかどうかを判断できます。

<span id="パラメータ"></span>
#### パラメータ

`text`: [HtmlText](https://docs.byteplus.com/en/docs/18/36569#htmltext)オブジェクト。

<span id="elementhandler"></span>
## ElementHandler

HTML要素レベルの解析イベントハンドラーで、CSSセレクターに一致するDOM要素の解析イベントをリッスンおよび処理するために使用されます。

次のコールバック関数を使用できます。各コールバック関数はオプションであり、各コールバック関数は非同期関数にすることができます。

<span id="oncomment-comment"></span>
### onComment(comment)

このコールバックは、CSSセレクターに一致する要素内のコメントノードが解析されるときに呼び出されます。

<span id="パラメータ"></span>
#### パラメータ

`comment`: [HtmlComment](https://docs.byteplus.com/en/docs/18/36569#htmlcomment)オブジェクト。

<span id="ontext-text"></span>
### onText(text)

このコールバックは、CSSセレクターに一致する要素内のテキストノードが解析されるときに呼び出されます。

テキストノードのコンテンツは、ストリーミング解析中に複数のフラグメントで送信される場合があるため、同じテキストノードに対して`onText()`が複数回呼び出されることがあります。たとえば、HTML `<div>This is long text</div>`の場合、`This is long text`が2つの部分で返されると、`This is long text`はテキストノードですが、`onText()`は2回呼び出されます。[lastInTextNode](https://docs.byteplus.com/en/docs/18/36569#lastintextnode)属性を使用して、最後の呼び出しかどうかを判断できます。

<span id="パラメータ"></span>
#### パラメータ

`text`: [HtmlText](https://docs.byteplus.com/en/docs/18/36569#htmltext)オブジェクト。

<span id="onelement-element"></span>
### onElement(element)

このコールバック関数は、CSSセレクターで選択されたタグが解析されるときに呼び出されます。CSSセレクターが複数のタグに一致する場合、`onElement()`は複数回呼び出されます。


* `element`: [HtmlElement](https://docs.byteplus.com/en/docs/18/36569#htmlelement)オブジェクト。


<span id="htmlノードオブジェクト"></span>
# HTMLノードオブジェクト

<span id="htmldoctype"></span>
## HtmlDoctype

DOCTYPEノードを表します。`name`、`publicId`、および`systemId`属性が含まれます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">たとえば、次のDOCTYPEノードでは、<code>name</code>は<code>HTML</code>、<code>publicId</code>は<code>-//W3C//DTD HTML 4.01 Transitional//EN</code>、<code>systemId</code>は<code>https://www.w3.org/TR/html4/loose.dtd</code>です。</div>


<div data-tips="true" data-tips-type="tip">```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
```
</div>


<span id="name"></span>
### name

DOCTYPEノードの名前を表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。

<span id="publicid"></span>
### publicId

DOCTYPEノードの公開IDを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。

<span id="systemid"></span>
### systemId

DOCTYPEノードのシステムIDを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。

<span id="htmldocend"></span>
## HtmlDocend

HTMLドキュメント解析の終了を表します。次のメソッドが含まれます。

<span id="append-string-contentoption"></span>
### append(String, ContentOption)

HTMLドキュメントにフッターを挿入します。


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


例:

```JavaScript
append("not html", {isHtml: false});
```


<span id="htmlcomment"></span>
## HtmlComment

解析されたコメントノードを表します。次のメソッドと属性が含まれます。

<span id="set-string"></span>
### set(String)

コメントの内容を変更します。

<span id="before-string-contentoption"></span>
### before(String, ContentOption)

コメントノードの前にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

コメントノードの後にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

コメントノードを置き換えます。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、ノードを置き換えるために使用される[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。この文字列はノード全体を置き換えます。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="remove"></span>
### remove()

コメントノードを削除します。

<span id="removed"></span>
### removed

タグが削除されたかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。


* true: タグは削除されました。

* false: タグは削除されていません。


<span id="value"></span>
### value

コメントノードのコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。

<span id="htmltext"></span>
## HtmlText

テキストノードを表します。次のメソッドと属性が含まれます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ストリーミング解析では、同じテキストノードのコンテンツが複数のフラグメントに分割される場合があります。<a href="https://docs.byteplus.com/en/docs/18/36569#lastInTextNode">lastInTextNode</a>属性を使用して、テキストノード全体のコンテンツが完全に解析されたかどうかを判断する必要があります。</div>


<span id="before-string-contentoption"></span>
### before(String, ContentOption)

テキストノードの前にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

テキストノードの後にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

テキストノードを置き換えます。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、ノードを置き換えるために使用される[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。このStringオブジェクトはノード全体を置き換えます。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="remove"></span>
### remove()

テキストノードを削除します。

<span id="value"></span>
### value

テキストノードのコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。現在の`HtmlText`オブジェクトに含まれるフラグメントがテキストノードの最後のフラグメントである場合、この属性は空の文字列を返します。

<span id="removed"></span>
### removed

テキストノードが削除されたかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。


* true: テキストノードは削除されました。

* false: テキストノードは削除されていません。


<span id="lastintextnode"></span>
### lastInTextNode

現在の`HtmlText`オブジェクトに含まれるフラグメントがテキストノードの最後のフラグメントであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。


* true: 現在の`HtmlText`オブジェクトに含まれるフラグメントは、テキストノードの最後のフラグメントです。

* false: 現在の`HtmlText`オブジェクトに含まれるフラグメントは、テキストノードの最後のフラグメントではありません。


`onText()`コールバックは、同じテキストノードに対して複数回トリガーされる場合があります。テキストノード全体のコンテンツを取得する必要がある場合は、テキストノードの`lastInTextNode`属性がtrueになるまでコンテンツをバッファリングできます。

<span id="例"></span>
### 例

次の例は、`onText` コールバックを使用してHTMLドキュメント内のテキストコンテンツをキャプチャして変換する方法を示しています。この例では、すべてのテキストノードのコンテンツが大文字に変換されます。

```javascript
addEventListener('fetch', (event) => {
  event.respondWith(handle(event));
});

async function handle(event) {
  // 元のHTMLページを取得します。
  const req = await fetch(event.request);

  // onTextイベントでテキストチャンクを連結するためのバッファを作成します。
  // onTextは単一のテキストノードで複数回トリガーされる可能性があるため、連結が必要です。
  let buffer = [];
  const htmlStream = createHtmlStream(
      req.body,  // パラメータ1：ReadableStream、つまり元のレスポンスのボディを渡します。
      undefined, // パラメータ2：DocumentHandler、ここではドキュメントレベルのイベントは処理されません。
      [[         // パラメータ3：特定の要素を処理するためのElementHandlerの配列。
        '*',   // CSSセレクタ'*'を使用してすべての要素に一致させます。
        {
          // onTextハンドラ：テキストノードが解析されるときにトリガーされます。
          onText(text) {
            // 現在のテキストチャンクをバッファに保存します。
            buffer.push(text.value);
            // lastInTextNodeがtrueの場合、これが現在のテキストノードの最後のテキストチャンクであることを示します。
            if (text.lastInTextNode) {
              // すべてのテキストチャンクを連結して完全なテキストを形成します。
              const data = buffer.join("");
              // テキストを大文字に変換し、元のテキストを置き換えます。
              text.replace(data.toUpperCase());
              // 次のテキストノードの処理に備えてバッファをリセットします。
              buffer = [];
            }
          }
        }
      ]]);

  // 変更されたReadableStreamオブジェクトをクライアントへのレスポンスとして返します。
  return htmlStream;
}
```


<span id="htmlelement"></span>
## HtmlElement

CSSセレクターによって選択されたタグに対応するHTML要素を表します。次のメソッドと属性が含まれます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">現在のHTML要素がdivノードであると仮定すると、<code>after()</code>、<code>before()</code>、<code>append()</code>、<code>prepend()</code>、および<code>setInnerContent()</code>のコンテンツ挿入位置は、下の図のようになります。</div>


<div data-tips="true" data-tips-type="tip"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_86b8dec24c73c57a2a3731e077b30a1e.jpeg" width="500px" /></div>


<span id="setattribute-string-string"></span>
### setAttribute(String, String)

HTML要素の属性の値を設定します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは属性名です。

* 2番目のパラメータは属性値です。


<span id="after-string-contentoption"></span>
### after(String, ContentOption)

このタグの後にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="append-string-contentoption"></span>
### append(String, ContentOption)

このタグ内のコンテンツの後にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="prepend-string-contentoption"></span>
### prepend(String, ContentOption)

このタグ内のコンテンツの前にコンテンツを挿入します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、挿入するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="setinnercontent-string-contentoption"></span>
### setInnerContent(String, ContentOption)

タグ内のコンテンツを変更します。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、設定するコンテンツを表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツタイプがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツタイプがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="removeandkeepcontent"></span>
### removeAndKeepContent()

タグを削除しますが、その子ノードのコンテンツは保持します。

<span id="replace-string-contentoption"></span>
### replace(String, ContentOption)

タグを置き換えます。

<span id="パラメータ"></span>
#### パラメータ


* 最初のパラメータは、ノードを置き換えるために使用される[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。この文字列はノード全体を置き換えます。

* 2番目のパラメータは`ContentOption`オブジェクトです。このオブジェクトには、一意の属性`isHtml`が含まれています。この属性は、最初のパラメータのコンテンツタイプがHTMLであるかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)です。

   * true: 最初のパラメータのコンテンツがHTMLであることを示します。最初のパラメータのコンテンツはHTMLエスケープされません。

   * false: 最初のパラメータのコンテンツがHTMLでないことを示します。最初のパラメータのコンテンツは、HTMLドキュメントに挿入される前にHTMLエスケープされます。


<span id="remove"></span>
### remove()

ノードを削除します。

<span id="hasattribute-string"></span>
### hasAttribute(String)

属性が存在するかどうかを確認し、[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)を返します。


* true: 属性は存在します。

* false: 属性は存在しません。


パラメータは、属性の名前を表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

<span id="getattribute-string"></span>
### getAttribute(String)

属性の値を表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)を返します。属性が存在しない場合はnullを返します。

パラメータは、属性の名前を表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

<span id="removeattribute-string"></span>
### removeAttribute(String)

属性を削除します。

パラメータは、属性の名前を表す[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)です。

<span id="iterator"></span>
### [@iterator]

[HtmlElement](https://docs.byteplus.com/en/docs/18/36569#htmlelement) オブジェクトのプロパティを反復処理するために使用されます。[HtmlElement](https://docs.byteplus.com/en/docs/18/36569#htmlelement) オブジェクトの各プロパティに対して、反復子は2つの要素を含む配列オブジェクトを返します。ここで、`[0]` はプロパティ名、`[1]` はプロパティの値を表します。

```JavaScript
for (const attribute of element) {
    console.log(attribute[0]);
    console.log(attribute[1]);
}

// 上記の例で<a attr='1', attr2='2'>タグを反復処理する場合
// 次のように出力されます
// attr
// 1
// attr2
// 2
```


<span id="tagname"></span>
### tagName

[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。現在のタグ名を取得または設定します。

<span id="namespaceuri"></span>
### namespaceUri

[Stringオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/String)。タグのXML名前空間を取得します。

<span id="removed"></span>
### removed

タグが削除されたかどうかを示す[Booleanオブジェクト](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Boolean)。


* true: タグは削除されました。

* false: タグは削除されていません。


<span id="cssセレクターの使用方法"></span>
# CSSセレクターの使用方法

&nbsp;

CSSセレクターはHTML要素を照合するために使用されます。一般的な使用方法は次のとおりです。

<span id="指定されたタイプのすべてのタグを選択する"></span>
### 指定されたタイプのすべてのタグを選択する

`"a"`はすべてのaタグを選択します。

<span id="特定のタグの下の子ノードを選択する"></span>
### 特定のタグの下の子ノードを選択する

`"a div"`はaタグの下のdivタグを選択します。

<span id="すべてのタグを選択する"></span>
### すべてのタグを選択する

`"*"`

<span id="特定のタグの下の子ノードを選択する"></span>
### 特定のタグの下の子ノードを選択する

`"a > b"`: bタグを選択します。bタグにはaという名前の親ノードがあります。

<span id="指定された属性とタイプを持つすべてのタグを選択する"></span>
### 指定された属性とタイプを持つすべてのタグを選択する

`"a[x]"`: 属性xを持つすべてのaタグを選択します。

<span id="指定されたクラスとタイプを持つすべてのタグを選択する"></span>
### 指定されたクラスとタイプを持つすべてのタグを選択する

`"a.u"`: クラス属性uを持つすべてのaタグを選択します。

<span id="指定されたidとタイプを持つすべてのタグを選択する"></span>
### 指定されたIDとタイプを持つすべてのタグを選択する

`"a#u"`: ID uを持つすべてのaタグを選択します。

<span id="指定された属性名、属性値、およびタイプを持つすべてのタグを選択する"></span>
### 指定された属性名、属性値、およびタイプを持つすべてのタグを選択する

`"a[y=\"z\"]"`: 属性名がyで属性値がzであるすべてのaタグを選択します。
