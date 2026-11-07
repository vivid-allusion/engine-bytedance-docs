---
title: "nest config"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-config-jp"
---

プロジェクト設定ファイルを表示および変更します。

<span id="概要"></span>
## 概要

```shell
npx nest config

npx nest config set <parameter> <value>

npx nest config set -g <parameter> <value>
```


<span id="説明"></span>
## 説明

プロジェクト設定には、関数プロジェクトの作業ディレクトリ、エントリーコードファイルディレクトリ、関数プロジェクト内のすべてのローカル関数に関する情報、およびエッジKVデータに関する情報が含まれます。プロジェクト設定は、関数プロジェクト設定とグローバルプロジェクト設定に分類できます。エッジ関数CLIは、関数プロジェクト設定から優先的に設定を取得します。見つからない場合は、グローバルプロジェクト設定から取得します。


* `npx nest config set`は、関数プロジェクト設定ファイルのパラメータを設定するために使用されます。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">グローバルパラメータ<code>-c <config_file_path></code>を使用して、現在のコマンドの関数設定ファイルを指定できます。   </div>
   

* `npx nest config set -g`は、グローバルプロジェクト設定ファイルのパラメータを設定するために使用されます。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">グローバルプロジェクト設定ファイルには、<code>cloud</code>で始まるパラメータ（例：<code>cloud.access_key</code>や<code>cloud.secret_key</code>）のみを設定することをお勧めします。これらのパラメータは、エッジ関数OpenAPIサービスに関連する設定であり、同じBytePlusアカウントの下にあるすべての関数に適用されます。   </div>
   

`npx nest config`を使用して、現在の関数プロジェクトで有効なエッジ関数CLI設定を表示できます。

<span id="サブコマンド"></span>
## サブコマンド

<span id="set"></span>
### set

エッジ関数CLI設定のパラメータを変更します。例：`npx nest config set name example-function`

`-g`を使用して、エッジ関数CLIのグローバルプロジェクト設定ファイルを変更できます。

<span id="パラメータの説明"></span>
#### パラメータの説明


|パラメータ |説明 |
|---|---|
|work_dir |関数プロジェクトの作業ディレクトリ。 |
|src_dir |関数エントリーコードファイルのディレクトリ。 |
|output_dir |関数実行コードファイルのディレクトリ。nest debugまたはnest startを使用してローカル関数を実行する際、エッジ関数CLIは関数エントリーコードファイルに基づいて、`output_dir`で指定されたディレクトリに関数実行コードファイルを生成します。関数実行コードファイルには、関数エントリーコードファイルと比較して、即時実行関数式（IIFE）が追加されます。 |
|cloud.api_server |エッジ関数OpenAPIサービスのURL。このパラメータは固定であり、変更する必要はありません。 |
|cloud.debug_server |エッジ関数DebuggerサービスのURL。このパラメータは固定であり、変更する必要はありません。 |
|cloud.api_version |エッジ関数OpenAPIサービスのバージョン。このパラメータは固定であり、変更する必要はありません。 |
|cloud.api_region |エッジ関数OpenAPIサービスのリージョン。このパラメータは固定であり、変更する必要はありません。 |
|cloud.api_timeout |エッジ関数OpenAPIのタイムアウト。デフォルトは5000ミリ秒です。 |
|cloud.key_manager_url |BytePlusコンソールのAPIアクセスキーページのURL。このパラメータは固定であり、変更する必要はありません。 |
|cloud.product |エッジ関数OpenAPI製品タイプ。このパラメータは固定であり、変更する必要はありません。 |
|cloud.access_key |BytePlusアカウントのAccess Key ID。[BytePlusコンソール](https://console.byteplus.com/iam/keymanage)からAccess Key IDを取得できます。 |
|cloud.secret_key |BytePlusアカウントのSecret Access Key。[BytePlusコンソール](https://console.byteplus.com/iam/keymanage)からSecret Access Keyを取得できます。 |
|functions.[N].id |プロジェクトリスト内のN番目のローカル関数のID。 |
|functions.[N].name |プロジェクトリスト内のN番目のローカル関数の名前。 |
|functions.[N].type |プロジェクトリスト内のN番目のローカル関数のエントリーコードファイルタイプ。 |
|functions.[N].entry |プロジェクトリスト内のN番目のローカル関数のエントリーコードファイル名。 |
