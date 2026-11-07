---
title: "nest versions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-version-jp"
---

ローカル関数のリリースされたコードバージョンを取得します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数のリリース履歴はローカルに保存されません。エッジ関数CLIは、エッジ関数サーバー上でローカル関数のリリース履歴を管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="サブコマンド"></span>
## サブコマンド

<span id="list"></span>
### list

```shell
npx nest versions list --function <function_id_or_name> --page <page_number>
```


ローカル関数のリリースされたコードバージョンのリストを表示します。


* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。

* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。


```shell
$ npx nest versions list
+---------+------+------------+-------------+----------------------+------------------+---------------------+
| VERSION | TYPE |   STATUS   | DESCRIPTION |       CREATOR        | PREVIOUS VERSION |     CREATETIME      |
+---------+------+------------+-------------+----------------------+------------------+---------------------+
| 1.0.2   | Full | Publishing |             | ******************** | 1.0.1            | 2025-01-08 17:35:40 |
| 1.0.1   | Full | Success    |             | ******************** |                  | 2025-01-08 00:55:42 |
+---------+------+------------+-------------+----------------------+------------------+---------------------+
```


<span id="view"></span>
### view

```shell
npx nest versions view <version> --function <function_id_or_name>
```


指定されたバージョンの関数コードを表示します。


* `<version>`: *string, required*

   * 関数コードのバージョン。関数コードのバージョンは`npx nest versions list`を通じて取得できます。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。


```shell
$ npx nest versions view 1.0.1
/**
 * Add the necessary event listener
 * @param {Event} fetch event, {Function} async function
 */
addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request));
})

/**
 * Make a response to client
 * @param {Request} request
 */
async function handleRequest(request) {
  return new Response('Hello World!', { status: 200 });
}
```
