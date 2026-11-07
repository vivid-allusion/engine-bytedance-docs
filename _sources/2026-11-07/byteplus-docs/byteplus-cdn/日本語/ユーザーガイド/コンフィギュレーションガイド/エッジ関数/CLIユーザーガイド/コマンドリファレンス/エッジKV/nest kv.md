---
title: "nest kv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-jp"
---

エッジKVを管理します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">エッジKVデータはローカルに保存されません。エッジ関数CLIは、エッジ関数サーバー上でKVデータを管理します。</div>



<span id="nest-kv-namespace"></span>
# nest kv namespace

名前空間を管理します。

<span id="サブコマンド"></span>
## サブコマンド

<span id="list"></span>
### list

```shell
npx nest kv namespace list --page <page_number> --desc
```


名前空間のリストを取得します。


* `<page_number>`: *integer, optional*

   * ページ分割表示のページ番号。デフォルトは1です。

* `--desc`: *boolean, optional*:

   * 名前空間IDを降順でソートします。デフォルトは昇順です。


```shell
$ npx nest kv namespace list
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
|                   ID:NAME                   |          REGION          |             PROJECT              |                            DESCRIPTION                            |     CREATETIME      |
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
| 24629043532424120990:ns                     | Outside Chinese Mainland | default                          | more updates                                                      | 2024-12-30 15:21:07 |
| 25540045541653372777:abtest_config          | Outside Chinese Mainland | default                          | testq                                                             | 2025-01-17 17:13:10 |
| 7758139412787918608:gochina                 | Outside Chinese Mainland | default                          |                                                                   | 2025-06-13 18:45:07 |
+---------------------------------------------+--------------------------+----------------------------------+-------------------------------------------------------------------+---------------------+
```


<span id="create"></span>
### create

```shell
npx nest kv namespace create <name> -d <description> -p <project>
```


名前空間を作成します。


* `<name>`: *string, required*

   * 名前空間の名前。

* `<description>`: *string, optional*

   * 名前空間の説明。

* `<project>`: *string, optional*:

   * 名前空間が属するプロジェクト。デフォルトは`default`です。


```shell
$ npx nest kv namespace create new12345
New namespace "new12345" created!
```


<span id="update"></span>
### update

```shell
npx nest kv namespace update <id:name> -d <description> 
```


指定された名前空間の説明を更新します。


* `<id:name>`: *string, required*

   * 名前空間のIDと名前。形式は`<id:name>`です。例：`24629*********120990:namespace_name`。名前空間のIDと名前は`npx nest kv namespace list`で取得できます。

* `<description>`: *string, optional*

   * 名前空間の説明。


```shell
$ npx nest kv namespace update 1677061481998840412:new12345  -d "more updates"
[1677061481998840412:new12345]
>>> the desc is more updates
Namespace 1677061481998840412:new12345 updated!
```


<span id="delete"></span>
### delete

```shell
npx nest kv namespace delete <id:name>
```


指定された名前空間を削除します。


* `<id:name>`: *string, required*

   * 名前空間のIDと名前。形式は`<id:name>`です。例：`24629*********120990:namespace_name`。名前空間のIDと名前は`npx nest kv namespace list`で取得できます。


<span id="nest-kv-keys"></span>
# nest kv keys

指定された名前空間のキーと値のペアのリストを取得します。

```shell
nest kv keys --namespace <id:name>
```



* `<id:name>`: *string, required*

   * 名前空間のIDと名前。形式は`<id:name>`です。例：`24629*********120990:namespace_name`。名前空間のIDと名前は`npx nest kv namespace list`で取得できます。


<span id="nest-kv-set"></span>
# nest kv set

```shell
nest kv set --namespace <id:name> <key> <value> --ttl <ttl>

nest kv set --namespace <id:name> <key> --file <file_path> --ttl <ttl>
```


キーと値のペアを追加または更新します。


* `<id:name>`: *string, required*

   * 名前空間のIDと名前。形式は`<id:name>`です。例：`24629*********120990:namespace_name`。名前空間のIDと名前は`npx nest kv namespace list`で取得できます。

* `<key>`: *string, required*

   * キーと値のペアのキー。

* `<value>`: *string, optional*

   * キーと値のペアの値。`<value>`または`<file_path>`のいずれかを設定する必要があります。

* `<ttl>`: *string, optional*

   * キーと値のペアの有効期限（秒単位）。デフォルトは期限切れなしです。

* `<file_path>`: *string, optional*

   * ファイルパス。このファイルの内容がキーと値のペアの値として使用されます。`<value>`または`<file_path>`のいずれかを設定する必要があります。


<span id="nest-kv-delete"></span>
# nest kv delete

```shell
nest kv delete --namespace <id:name> <key>
```


指定されたキーと値のペアを削除します。


* `<id:name>`: *string, required*

   * 名前空間のIDと名前。形式は`<id:name>`です。例：`24629*********120990:namespace_name`。名前空間のIDと名前は`npx nest kv namespace list`で取得できます。

* `<key>`: *string, required*

   * キーと値のペアのキー。


<span id="nest-kv-get"></span>
# nest kv get

```shell
nest kv get --namespace <id:name> <key> --save-dev --no-decode
```


キーと値のペアの値を取得します。


* `<id:name>`: *string, required*

   * 名前空間のIDと名前。形式は`<id:name>`です。例：`24629*********120990:namespace_name`。名前空間のIDと名前は`npx nest kv namespace list`で取得できます。

* `<key>`: *string, required*

   * キーと値のペアのキー。

* `--save-dev`: *boolean, optional*

   * デバッグ用にキーと値のペアをローカルに保存します。デフォルトでは保存しません。

* `--no-decode`: *boolean, optional*

   * キーと値のペアの値をbase64エンコードされたフォーマットで直接出力します。デフォルトではbase64デコードされた値を出力します。キーと値のペアの値がバイナリの場合、文字化けを避けるために`--no-decode`を使用してbase64エンコードされた値を出力できます。
