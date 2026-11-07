---
title: "nest envs"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-env-jp"
---

ローカル関数の環境変数を管理します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp">nest init</a>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数の環境変数はローカルに保存されません。エッジ関数CLIは、エッジ関数サーバー上でローカル関数の環境変数を管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="サブコマンド"></span>
## サブコマンド

<span id="list"></span>
### list

```shell
npx nest envs list --function <function_id_or_name> --save-dev
```


ローカル関数の環境変数のリストを取得します。


* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<--save-dev>`: *boolean, optional*

   * デバッグ用に環境変数をローカルに保存するかどうか。デフォルトではローカルに保存されません。


```shell
$ npx nest envs list
+------+--------+
| KEY  | VALUE  |
+------+--------+
| key1 | value1 |
| key2 | value2 |
+------+--------+
```


<span id="set"></span>
### set

```shell
npx nest envs set <key> <value> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">環境変数に対する追加、削除、変更などの操作は、関数が再度公開された後に有効になります。</div>


環境変数の値を設定します。


* `<key>`: *string, required*

   * 環境変数のキー。

* `<value>`: *string, required*

   * 環境変数の値。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。


<span id="delete"></span>
### delete

```shell
npx nest envs set <key> --function <function_id_or_name>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">環境変数に対する追加、削除、変更などの操作は、関数が再度公開された後に有効になります。</div>


環境変数を削除します。


* `<key>`: *string, required*

   * 環境変数のキー。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。
