---
title: "初心者向け：CLIでエッジKVを管理する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-cli-kv-quickstart-jp"
---

このチュートリアルでは、簡単な例のシナリオに基づいて、エッジ関数CLIを使用してエッジKVを管理する方法を紹介します。

エッジKVサービスは、BytePlusのグローバルエッジノードに分散されたキーバリューストレージサービスです。エッジ関数コンソール、OpenAPI、またはランタイムAPIを通じてキーバリューペアがエッジKVに書き込まれると、自動的にすべてのエッジノードに同期されます。関数は、ランタイムAPIを通じて同じエッジノード上にあるキーバリューペアを迅速に読み取ることができます。

<span id="例のシナリオ"></span>
## 例のシナリオ

あなたのウェブサイトはA/Bテスト機能をサポートしており、ユーザーの地理的位置に基づいて異なるバージョンのウェブページを返すことができます。バージョン切り替え設定情報はエッジKVに保存されています。関数のコードからバージョン切り替え設定情報を読み取れるようにしたいと考えています。このチュートリアルでは、設定情報が以下のようであると仮定します：

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="実行環境"></span>
## 実行環境

エッジ関数CLIを実行するデバイスは、以下の要件を満たす必要があります：


* オペレーティングシステムは以下のいずれかである必要があります：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/)と[npm](https://www.npmjs.com/)がインストールされていること。バージョン要件は以下の通りです：

   * Node.js: 8.17.0+

   * npm: 6.13.4+

* [wget](https://www.gnu.org/software/wget/)または[cURL](https://curl.se/)がインストールされていること。


<span id="手順"></span>
## 手順

例のシナリオを実装するには、以下の手順を完了する必要があります。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f0c86f80feadb58f6851e217a37dee38.png) </span>


1.  **エッジ関数CLIをインストールする** ：空のNode.jsプロジェクトを作成し、プロジェクト内にエッジ関数CLIをインストールします。

2. **Access Key IDとSecret Access Keyを設定する** ：エッジ関数CLIを使用して、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定します。

3. **名前空間を作成する** ：エッジ関数CLIを使用して名前空間を作成します。

4.  **キーバリューペアを作成する** ：エッジ関数CLIを使用して、名前空間内にキーバリューペアを作成します。

5. **関数コード内でキーバリューペアの値を読み取る** ：関数コード内でキーバリューペアの値を読み取ります。


<span id="ステップ1：エッジ関数cliをインストールする"></span>
### ステップ1：エッジ関数CLIをインストールする

以下の手順に従って、エッジ関数CLIをインストールします。


1. `npm init`を使用して空のNode.jsプロジェクトを作成します。


```shell
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help init` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (test) 
version: (1.0.0) 
description: 
entry point: (index.js) 
test command: 
git repository: 
keywords: 
author: 
license: (ISC) 
About to write to /Users/MyFolder/package.json:

{
  "name": "test",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "description": ""
}


Is this OK? (yes) 
```



2. Node.jsプロジェクトディレクトリで`npm i --save-dev @byteplus/nest`を実行して、エッジ関数CLIをインストールします。


```shell
$ npm i --save-dev @byteplus/nest

added 1 package, and audited 2 packages in 739ms

found 0 vulnerabilities
```


次に、Access Key IDとSecret Access Keyを設定する必要があります。

<span id="ステップ2：access-key-idとsecret-access-keyを設定する"></span>
### ステップ2：Access Key IDとSecret Access Keyを設定する

`HelloWorld`ディレクトリで以下のコマンドを実行して、エッジ関数CLIにAccess Key IDとSecret Access Keyを設定します。Access Key IDとSecret Access Keyは[BytePlusコンソール](https://console.byteplus.com/iam/keymanage)から取得できます。[nest config](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-config-jp)を参照してください。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="ステップ3：名前空間を作成する"></span>
### ステップ3：名前空間を作成する

Node.jsプロジェクトディレクトリで`nest kv namespace create`を実行して、`abtest_config`という名前の名前空間を作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">名前空間の作成はコンソール、OpenAPI、またはCLIを使用してのみ可能です。ランタイムAPIを使用して名前空間を作成することはできません。</div>


```shell
$ npx nest kv namespace create abtest_config
New namespace "abtest_config" created!
```


`nest kv namespace list`を実行して、作成した名前空間を表示できます。

```shell
$ npx nest kv namespace list
+---------------------------------------------------------------+--------------+----------------------+---------------------+
|                            ID:NAME                            |   PROJECT    |     DESCRIPTION      |     CREATETIME      |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
| 25540045541653372777:abtest_config                            | default      |                      | 2025-01-17 17:13:10 |
+---------------------------------------------------------------+--------------+----------------------+---------------------+
```


<span id="ステップ4：名前空間内にキーバリューペアを作成する"></span>
### ステップ4：名前空間内にキーバリューペアを作成する

Node.jsプロジェクトディレクトリで`nest kv set`を実行して、`abtest_config`名前空間の下にキーバリューペアを作成します。キーバリューペアのキーは`config_key`です。キーバリューペアの値は、例のシナリオのJSON値`{"us":"versionA","eu":"versionB","asia":"versionA"}`です。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">キーバリューペアの作成はコンソール、OpenAPI、またはランタイムAPIを使用して可能です。</div>


```shell
$ npx nest kv set --namespace 25540045541653372777:abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```


`nest kv get`を実行して、作成したキーバリューペアを表示できます。

```Plain Text
$ npx nest kv get --namespace 25540045541653372777:abtest_config config_key
+-------+---------------+
| ITEM  |     VALUE     |
+-------+---------------+
| Key   | config_key    |
| Value | us:versionA   |
| DDL   | Never expires |
+-------+---------------+
```


<span id="ステップ5：関数コード内でキーバリューペアの値を読み取る"></span>
### ステップ5：関数コード内でキーバリューペアの値を読み取る

以下の手順に従って、関数コード内でキーバリューペアの値を読み取ります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">キーバリューペアの値の読み取りはコンソール、OpenAPI、またはランタイムAPIを使用して可能です。</div>


関数コードでは、[KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI-jp)を呼び出してキーバリューペアの値を取得します。

```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```


エッジ関数CLIの[nest debug](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-debug-jp)コマンドを使用して、Debuggerコマンドラインで上記のコードをデバッグできます：


1. `setkv`を実行して、Debuggerにキーバリューペアを追加します。


```shell
nest: setkv abtest_config config_key {"us":"versionA","eu":"versionB","asia":"versionA"}
```



2. `query`を実行して、関数の実行をトリガーします。


```shell
nest: query
==> HttpResponse ✓
status: 200

statusText: OK

header:
  content-type => text/plain;charset=UTF-8
  date => Fri, 17 Jan 2025 09:53:26 GMT
  server => Sparrow
  transfer-encoding => chunked

body:
{us:versionA,eu:versionB,asia:versionA}
```
