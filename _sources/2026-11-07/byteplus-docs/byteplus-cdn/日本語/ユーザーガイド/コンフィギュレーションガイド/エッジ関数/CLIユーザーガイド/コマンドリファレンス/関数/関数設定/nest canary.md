---
title: "nest canary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-canary-jp"
---

ローカル関数のカナリア環境を管理します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp">nest init</a>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数の環境変数はローカルに保存されません。エッジ関数CLIは、エッジ関数サーバー上でローカル関数の環境変数を管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="サブコマンド"></span>
## サブコマンド

<span id="list"></span>
### list

```shell
npx nest canary list --canary --continents <continent1,continent2,...> --countries <country1,country2,...> --function <function_id_or_name>
```


カナリア環境のエッジノードを取得します。


* `--canary`: *boolean, optional*

   * カナリア環境のエッジノードのみを表示するかどうか。デフォルトはfalseです。

* `<continent1,continent2,...>`: *string, optional*

   * エッジノードが位置する大陸。複数の大陸名をカンマで区切ります。例：`Asia,Europe`。

* `<country1,country2,...>`: *string, optional*

   * エッジノードが位置する国または地域。複数の国または地域名をカンマで区切ります。例：`China,France`。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。


```shell
$ npx nest canary list
+---------+-----------+--------+
| COUNTRY | CONTINENT | CANARY |
+---------+-----------+--------+
| China   | Asia      | NO     |
+---------+-----------+--------+
```


<span id="add"></span>
### add

```shell
npx nest canary add --countries <country1,country2,...> --function <function_id_or_name>
```


指定した国または地域に位置するエッジノードをカナリア環境に追加します。


* `<country1,country2,...>`: *string, optional*

   * エッジノードが位置する国または地域。複数の国または地域名をカンマで区切ります。例：`China,France`。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。


<span id="delete"></span>
### delete

```shell
npx nest canary delete --countries <country1,country2,...> --function <function_id_or_name>
```


指定した国または地域に位置するエッジノードをカナリア環境から削除します。


* `<country1,country2,...>`: *string, optional*

   * エッジノードが位置する国または地域。複数の国または地域名をカンマで区切ります。例：`China,France`。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数CLIは`Error: function id required`エラーを返します。
