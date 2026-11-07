---
title: "nest tickets"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-ticket-jp"
---

ローカル関数のコードリリース履歴を取得します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数のリリース履歴はローカルに保存されません。エッジ関数CLIは、エッジ関数サーバー上でローカル関数のリリース履歴を管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="概要"></span>
## 概要

```shell
npx nest tickets -d <description> --function_id <function_id_or_name> --page <page_number> --desc
```


関数コードのリリースレコードのリストを取得します。


* `<description>`: *string, optional*

   * バージョンの説明。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。

* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。

* `--desc`: *boolean, optional*:

   * バージョン番号を降順でソートします。デフォルトは昇順です。


```shell
$ npx nest tickets
+---------+------------+----------------------+-------------+
| VERSION | SCRIPTNAME |       CREATOR        | DESCRIPTION |
+---------+------------+----------------------+-------------+
| 1.0.2   | default    | ******************** |             |
| 1.0.1   | default    | ******************** |             |
+---------+------------+----------------------+-------------+
```


<span id="サブコマンド"></span>
## サブコマンド

<span id="get"></span>
### get

```shell
npx nest tickets get <version> --function <function_id_or_name>
```



* `<version>`: *string, required*

   * 関数コードのバージョン。関数コードのバージョンは`npx nest versions list`を通じて取得できます。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。


```shell
$ npx nest versions get 1.0.2
(() => {
  // src/index.js
  addEventListener("fetch", (event) => {
    event.respondWith(upgradeToSSL(event));
  });
  async function upgradeToSSL(event) {
    const incommingRequest = event.request;
    const url = new URL(incommingRequest.url);
    if (url.protocol == "http:") {
      url.protocol = "https";
      return fetch(url.toString(), {
        method: incommingRequest.method,
        headers: incommingRequest.headers,
        body: incommingRequest.body
      });
    } else {
      return fetch(incommingRequest);
    }
  }
})();
```
