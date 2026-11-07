---
title: "nest deploy"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-deploy-jp"
---

ローカル関数をエッジノードにデプロイします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>



<span id="概要"></span>
## 概要

```shell
npx nest deploy --canary --message <message> --function <function_id_or_name> --all --create
```


<span id="説明"></span>
## 説明

カナリアリリースまたはフルリリースを選択できます。


* `--canary`: *boolean、optional*

   * カナリアリリース。カナリアリリースを実行する前に、カナリアリリースノードを設定していることを確認してください。カナリアリリースノードは[nest canary](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-canary-jp)を使用して設定できます。デフォルトはフルリリースです。

* `<message>`: *string、optional*

   * このリリースに関連する説明。

* `<function_id_or_name>`: *string、optional*

   * ローカル関数IDまたは関数名。このパラメータはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。名前で指定したローカル関数にまだ関数IDがない場合、エッジ関数CLIは新しいリモート関数を作成するよう促します。

* `--all`: *boolean、optional*

   * 現在のプロジェクト下のすべてのローカル関数をデプロイします。デフォルトでは、`--function`グローバルパラメータで指定されたローカル関数または[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数のみがデプロイされます。

* `--create`: *boolean、optional*

   * 対応するリモート関数を作成します。デフォルトでは、対応するリモート関数は作成されません。


<span id="nest-jsonファイルに手動で追加された関数設定またはエッジkvデータのデプロイ"></span>
## nest.jsonファイルに手動で追加された関数設定またはエッジKVデータのデプロイ

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>nest.json</code>ファイルを直接変更することにはリスクがあります。<code>nest.json</code>ファイルの構造に精通しており、大量の関数を頻繁にバッチ処理する必要がある場合にこの方法を使用できます。</div>


`nest.json`ファイルにローカル関数のCronトリガー設定、環境変数、関連ドメインを手動で追加できます。さらに、エッジKVのデータを手動で追加することもできます。nest deployを実行してローカル関数をデプロイする際、`--cron`、`--env`、`--kv`、`--domain`を使用して、これらの手動で追加された設定またはデータを同時にデプロイできます。


* `--cron`: *boolean、optional*

   * nest.jsonで手動で編集されたCronタスクをデプロイします。

* `--env`: *boolean、optional*

   * nest.jsonで手動で編集された環境変数をデプロイします。

* `--kv`: *boolean、optional*

   * nest.jsonで手動で編集されたエッジKVのデータをデプロイします。

* `--domain`: *boolean、optional*

   * nest.jsonで手動で編集された関数に関連付けられたドメインをデプロイします。


以下は手動で変更された`nest.json`ファイルの例です。

```json
{
  "work_dir": "/Users/HelloWorld",
  "src_dir": "src",
  "output_dir": "output",
  "cloud": {
    "api_server": "https://open.byteplusapi.com",
    "debug_server": "wss://byteplusef-debugger.byteintlapi.com",
    "api_version": "2021-03-01",
    "api_region": "ap-singapore-1",
    "api_timeout": 5000,
    "key_manager_url": "https://console.byteplus.com/iam/keymanage",
    "product": "CDN",
    "access_key": "xxx",
    "secret_key": "xxx"
  },
  "kv": {
      "24629043532424120990:ns": {
          "ENV": "boe",
          "port": "8383",
          "DEBUG": "true"
      }
  },
  "functions": [
    {
      "id": "10c5a0e*********1b8d90896",
      "name": "function1",
      "description": "",
      "type": "js",
      "entry": "index.js",
      "format": "",
      "project": ""
    },
    {
      "id": "",
      "name": "function2",
      "description": "",
      "type": "js",
      "entry": "test.js",
      "format": "",
      "envs": {
          "ENV": "boe",
          "port": "8383",
          "DEBUG": "true"
      },
      "domains": [
          {
              "names": [
                  "test.example.com"
              ],
              "type": "directory",
              "pattern": "/a/"
          }
      ],
      "crons": [
          {
              "name": "cron job name",
              "cron": "*/10 * * * *"
              "params": "",
              "global": false,
              "description": "description for this cron job",
          }
      ],
      "project": ""
    },
    {
      "id": "02581*********8247b5",
      "name": "function3",
      "description": "",
      "type": "js",
      "entry": "index.js",
      "format": "",
      "domains": [
          {
              "domains": [
                  "www.example.com"
              ],
              "type": "directory",
              "pattern": "/hello/"
          }
      ],
      "project": ""
    }
  ],
  "debugger": {}
}
```
