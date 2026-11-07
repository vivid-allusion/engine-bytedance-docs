---
title: "nest domain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-jp"
---

ローカル関数に関連付けられたドメイン名を管理します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数に関連付けられたドメイン名情報はローカルに保存されません。エッジ関数 CLIは、エッジ関数サーバー上でローカル関数に関連付けられたドメイン名を管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="説明"></span>
## 説明

ユーザーが関数に関連付けられたドメイン名にHTTPまたはHTTPSリクエストでアクセスし、ユーザーリクエストがドメイン名の転送ルールに一致すると、ドメイン名トリガーが関数コード内のfetchイベントをトリガーします。コード内でfetchイベントをリッスンし、処理する必要があります。

1つの関数は1つ以上のドメイン名に関連付けることができます。各ドメイン名も複数の関数に関連付けることができます。[使用制限](https://docs.byteplus.com/docs/byteplus-cdn/usage-limits-jp)を参照してください。

<span id="サブコマンド"></span>
## サブコマンド

<span id="list"></span>
### list

```shell
npx nest domain list --all --function <function_id> -page <page_number> --desc
```


ローカル関数に関連付けられたドメイン名を表示します。


* `--all`: *boolean, optional*

   * すべてのドメイン名を表示します。デフォルトでは、ローカル関数に関連付けられたドメイン名のみが表示されます。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。

* `--desc`: *boolean, optional*:

   * ドメイン名を降順でソートします。デフォルトは昇順です。


`npx nest domain list`を実行すると、ドメイン名、ステータス、転送ルールに関する情報を表示できます。

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| a.example.com               | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


`npx nest domain list --all`を実行すると、STATUSカラムでドメイン名が関数に関連付け可能かどうかを確認できます。

```shell
$ npx nest domain list --all

+--------------------------------------+-----------------+
|                DOMAIN                |     STATUS      |
+--------------------------------------+-----------------+
| a.example.com                        | Can be Bound    |
| a.example.org                        | Cannot be Bound |
+--------------------------------------+-----------------+
```


<span id="bind"></span>
### bind

```shell
npx nest domain bind <domain_name> --function <function_id> --url-directory <url_directory> --ignore-case

npx nest domain bind <domain_name> --function <function_id> --url-ext <url_ext> --ignore-case

npx nest domain bind <domain_name> --function <function_id> --url-match <url> --ignore-case
```


ドメイン名をローカル関数に関連付けます。

以下のパラメータを使用して、ドメイン名の転送ルールを設定できます。転送ルールに一致するユーザーリクエストのみがエッジ関数に転送されます。転送ルールの設定方法については、[ドメイン名トリガー](https://docs.byteplus.com/docs/byteplus-cdn/docs-domain-triggers-jp)を参照してください。


* `<domain_name>`: *string, required*

   * ドメイン名名。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。

* `<url_directory>`: *string, optional*

   * ルールタイプはURLディレクトリです。ルールは指定されたディレクトリ内のすべてのファイルに適用されます。`<url_directory>`、`<url_ext>`、`<url>`のいずれか1つを設定する必要があります。

* `<url_ext>`: *string, optional*

   * ルールタイプはファイル拡張子です。ルールは指定された拡張子を持つすべてのファイルに適用されます。`<url_directory>`、`<url_ext>`、`<url>`のいずれか1つを設定する必要があります。

* `<url>`: *string, optional*

   * ルールタイプは完全URLパスです。ルールは指定されたファイルに適用されます。`<url_directory>`、`<url_ext>`、`<url>`のいずれか1つを設定する必要があります。

* `--ignore-case`: *boolean, optional*

   * 大文字小文字を無視します。デフォルトでは大文字小文字を区別します。


例えば、以下のコマンドはドメイン名www.example.comをローカル関数に関連付け、転送ルールタイプをURLディレクトリに設定します。ユーザーリクエストのURLディレクトリが`/welcome/`の場合（例：`https://www.example.com/welcome/a.png`）、リクエストは転送ルールに一致します。

```shell
npx nest domain bind www.example.com --url-directory /welcome/
```


`npx nest domain list`を実行して、ドメイン名が関連付けられたかどうかを確認できます。

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
| www.example.com             | Online | directory | /welcome/ | false      |
+-----------------------------+--------+-----------+-----------+------------+
```


<span id="unbind"></span>
### unbind

```shell
npx nest domain unbind <domain_name> --function <function_id>
```


ドメイン名をローカル関数から解除します。


* `<domain_name>`: *string, required*

   * 解除するドメイン名。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。


`npx nest domain list`を実行して、ドメイン名が解除されたかどうかを確認できます。

```Plain Text
$ npx nest domain list

+-----------------------------+--------+-----------+-----------+------------+
|           DOMAIN            | STATUS |   TYPE    |  PATTERN  | IGNORECASE |
+-----------------------------+--------+-----------+-----------+------------+
+-----------------------------+--------+-----------+-----------+------------+
```
