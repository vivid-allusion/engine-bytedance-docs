---
title: "nest start"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-start-jp"
---

関数コードを実行します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを実行するためにAccess Key IDとSecret Access Keyを設定する必要はありません。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip"><code>nest debug</code>とは異なり、コードファイルを更新すると、新しいコードファイルは自動的にエッジ関数Debuggerに同期されます。</div>



<span id="概要"></span>
## 概要

```shell
npx nest start <address> --proxyHost <hostname>
```


<span id="説明"></span>
## 説明

`npx nest start`を実行すると、エッジ関数CLIはエッジ関数Debugger用のローカルHTTPプロキシを起動し、wssプロトコルを使用してエッジ関数Debuggerとの接続を確立します。cURLなどのツールを使用してこのアドレスにHTTPリクエストを送信すると、関数のドメイントリガーがfetchイベントをトリガーします。


* `<address>`: *string, optional*

   * ローカルプロキシのIPアドレス。デフォルトは`127.0.0.1`です。

* `<hostname>`: *string, optional*

   * リクエストURLのホスト名。デフォルトは`example.com`です。


```shell
$ npx nest start
==> Setting up debugger...
==> [info]: connection setup successfully!
==> [info]: loading envrionment variables... ✔
==> [info]: building script "default"...
==> [info]: uploading script 'default': **********/output/index.js... ✔
==> Local http proxy running on http://127.0.0.1:18080
```


cURLやブラウザなどのツールを使用して、ローカルプロキシにHTTPリクエストを送信し、関数のレスポンスを受け取ることができます。

```shell
$ curl -s http://127.0.0.1:18080
Hello World!
```
