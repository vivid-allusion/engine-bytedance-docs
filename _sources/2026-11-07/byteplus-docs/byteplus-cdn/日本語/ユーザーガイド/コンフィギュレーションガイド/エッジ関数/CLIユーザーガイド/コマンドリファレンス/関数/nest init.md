---
title: "nest init"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-jp"
---

現在のディレクトリに関数プロジェクトを作成し、その関数プロジェクト内にローカル関数を作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このコマンドを実行するためにAccess Key IDとSecret Access Keyを設定する必要はありません。</div>


<span id="概要"></span>
## 概要

```shell
npx nest init <dir> --env --sync --function <function_id>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以下のコマンドを直接実行して、エッジ関数CLIをすばやくインストールし、ローカル関数を作成することもできます。このコマンドを実行する前にエッジ関数CLIをインストールする必要はありません。</div>


<div data-tips="true" data-tips-type="tip">```shell
npx @byteplus/nest init --env --sync --function <function_id>
```
</div>


<div data-tips="true" data-tips-type="tip">このコマンドは以下の操作を順番に実行します：</div>



1. <div data-tips="true" data-tips-type="tip">現在のディレクトリにNode.jsプロジェクトを作成します。</div>


2. <div data-tips="true" data-tips-type="tip">Node.jsプロジェクトにエッジ関数CLIをインストールします。</div>


3. <div data-tips="true" data-tips-type="tip">エッジ関数CLIを実行して、現在のディレクトリに関数プロジェクトを作成し、その関数プロジェクト内にローカル関数を作成します。</div>



<span id="説明"></span>
## 説明

npxコマンドは、`npx nest init`を実行したディレクトリに関数プロジェクトを作成し、関数名の入力、関数テンプレートの選択、エントリーファイルの場所と名前の指定、関連するBytePlusプロジェクトの選択、関数の説明などの情報の入力を促します。その後、エッジ関数CLIは入力された情報に基づいてローカル関数を作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">BytePlusアカウントごとに関数名は一意である必要があります。名前の規則は以下の通りです：</div>


   * <div data-tips="true" data-tips-type="tip">英字、数字、ハイフン（\-）が使用可能です。</div>


   * <div data-tips="true" data-tips-type="tip">長さは128文字以内である必要があります。</div>


* <div data-tips="true" data-tips-type="tip">使用可能な関数テンプレートは、Access Key IDとSecret Access Keyを設定しているかどうかによって異なります：</div>


   * <div data-tips="true" data-tips-type="tip">Access Key IDとSecret Access Keyを設定していない場合、HelloWorldテンプレートのみ使用可能です。</div>


   * <div data-tips="true" data-tips-type="tip">Access Key IDとSecret Access Keyを設定している場合、エッジ関数がサポートするすべてのテンプレートを使用できます。</div>


* `<dir>`: *string, optional*

   * 関数プロジェクトを作成するディレクトリ。デフォルトは現在のディレクトリです。

* `--sync`: *boolean, optional*

   * 現在のプロジェクトに関連付けられたリモート関数を作成します。デフォルトでは、リモート関数は作成されません。

* `<function_id>`: *string, optional*

   * リモート関数の関数IDです。ローカル関数をリモート関数に関連付ける必要がある場合、このパラメータを使用してリモート関数の関数IDを設定できます。

* `--env`: *boolean, optional*

   * `<function_id>`に対応するリモート関数の環境変数をローカル環境に同期します。デフォルトでは、リモート関数の環境変数は同期されません。


関数プロジェクトには複数のローカル関数を持つことができます。関数プロジェクトに新しいローカル関数を作成する必要がある場合は、[nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#create)コマンドを使用できます。
