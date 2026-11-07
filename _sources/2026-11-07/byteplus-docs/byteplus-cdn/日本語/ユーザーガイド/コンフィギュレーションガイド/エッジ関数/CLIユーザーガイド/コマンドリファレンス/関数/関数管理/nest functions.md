---
title: "nest functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-jp"
---

ローカルまたはリモート関数に対して作成、読み取り、更新、削除の操作を実行します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>



<span id="サブコマンド"></span>
## サブコマンド

<span id="get"></span>
### get

```shell
npx nest functions get <function_id_or_name> 

npx nest functions get --remote <function_id> 
```


ローカルまたはリモート関数の情報を取得します。


* `<function_id_or_name>`: *string, required*

   * ローカル関数のIDまたは名前。

* `--remote`: *boolean, optional*

   * リモート関数の情報を取得します。デフォルトでは、ローカル関数の情報を取得します：

      * ローカル関数の情報を取得するには、`<function_id>`または`<function_name>`を使用できます。

      * リモート関数の情報を取得するには、`<function_id>`のみを使用できます。


<span id="list"></span>
### list

```shell
npx nest functions list --page <page_number> --desc -s <status> --remote
```


関数のリストを取得します。


* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。

* `--desc`: *boolean, optional*:

   * 関数IDを降順でソートします。デフォルトは昇順です。

* `<status>`: *string, optional*

   * 関数のステータス。

      * running: 実行中。

      * unassociated: ドメインに関連付けられていません。

      * configuring: 設定中。

* `--remote`: *boolean, optional*:

   * リストにはリモート関数のみが含まれます。デフォルトでは、ローカル関数のみが含まれます。


```shell
npx nest functions list
+----+------+------+--------------+--------------------------+---------+-------------+---------+
| ID | NAME | TYPE |    ENTRY     |          REGION          | PROJECT | DESCRIPTION | DEFAULT |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
|    | test | js   | src/index.js | Outside Chinese Mainland |         |             | true    |
+----+------+------+--------------+--------------------------+---------+-------------+---------+
```


<span id="create"></span>
### create

```shell
npx nest functions create --name <function_name> --description <function_description> --entry <path_to_entry_file> --project <project> --sync
```


関数プロジェクトに関数を作成します。このコマンドを実行すると、エッジ関数CLIは関数名の入力、関数テンプレートの選択、エントリーファイルの場所と名前の指定、関連するBytePlusプロジェクトの選択、関数の説明の提供、その他の情報の入力を促します。その後、エッジ関数CLIは入力された情報に基づいてローカル関数を作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">BytePlusアカウントごとに関数名は一意である必要があります。名前の規則は以下の通りです：</div>


   * <div data-tips="true" data-tips-type="tip">英字、数字、ハイフン（\-）が使用可能です。</div>


   * <div data-tips="true" data-tips-type="tip">長さは128文字以内である必要があります。</div>


* <div data-tips="true" data-tips-type="tip">使用可能な関数テンプレートは、Access Key IDとSecret Access Keyを設定しているかどうかによって異なります：</div>


   * <div data-tips="true" data-tips-type="tip">Access Key IDとSecret Access Keyを設定していない場合、HelloWorldテンプレートのみ使用可能です。</div>


   * <div data-tips="true" data-tips-type="tip">Access Key IDとSecret Access Keyを設定している場合、エッジ関数がサポートするすべてのテンプレートを使用できます。</div>


* `<function_name>`: *string, required*

   * 関数名。

* `<function_description>`: *string, optional*

   * 関数の説明。

* `<path_to_entry_file>`: *string, required*

   * エントリーファイルへのパス。エントリーファイルはローカル関数の実行開始点です。このパラメータで指定されたエントリーファイルが存在する必要があります。

* `<project>`: *string, optional*

   * 関数が属するプロジェクト。デフォルトは`default`です。

* `--sync`: *boolean, optional*

   * 同時に対応するリモート関数を作成します。デフォルトでは、対応するリモート関数は作成しません。


```shell
$ npx nest functions create --name test0111 --entry src/index.js
==> [info]: Creating a new function test0111 locally.✔
```


<span id="update"></span>
### update

```shell
npx nest functions update <function_id_or_name> --new-name <new_function_name> --new-description <new_function_description> --new-id <new_function_id> --new-entry <path_to_entry_file> --sync
```


関数IDまたは名前で関数名と説明を変更します。


* `<function_id_or_name>`: *string, required*

   * ローカル関数のIDまたは名前。

* `<new_function_name>`: *string, optional*

   * 新しい関数名。

* `<new_function_description>`: *string, optional*

   * 新しい関数の説明。

* `<path_to_entry_file>`: *string, optional*

   * エントリーファイルへのパス。エントリーファイルはローカル関数の実行開始点です。デフォルトはプロジェクト設定ファイルのエントリーファイルパスです。

* `--sync`: *boolean, optional*

   * 同時に対応するリモート関数を更新します。デフォルトでは、対応するリモート関数は更新しません。

* `--default`: *boolean, optional*

   * この関数をデフォルト関数として設定します。デフォルトでは、この関数をデフォルト関数として設定しません。関数プロジェクトでは、デフォルト関数は1つだけ設定できます。

* `<new_function_id>`: *boolean, optional*

   * 新しい関数ID。


<span id="pull"></span>
### pull

```shell
npx nest functions pull <function_id> --env
```


リモート関数のコードをローカル関数に同期します。


* `<function_id>`: *string, required*

   * 関数ID。

* `--env`: *boolean, optional*

   * リモート関数の環境変数をローカル関数に同期します。デフォルトでは、環境変数は同期しません。


<span id="delete"></span>
### delete

```shell
npx nest functions delete <function_id> --sync
```


関数IDでローカル関数を削除します。このコマンドは、プロジェクト設定ファイルの`functions`フィールド下の指定された関数IDに関する設定情報を削除しますが、ローカル関数のコードは削除しません。


* `<function_id>`: *string, required*

   * 関数ID。

* `--sync`: *boolean, optional*

   * 同時に対応するリモート関数を削除します。デフォルトでは、対応するリモート関数は削除しません。
