---
title: "nest rollback"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-rollback-jp"
---

ローカル関数のコードを指定したバージョンにロールバックします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>


* <div data-tips="true" data-tips-type="tip">ローカル関数のリリース履歴はローカルに保存されません。エッジ関数CLIは、エッジ関数サーバー上でローカル関数のリリース履歴を管理します。そのため、このコマンドを実行する際は、ローカル関数に関数IDが設定されていることを確認してください。</div>



<span id="概要"></span>
## 概要

```shell
npx nest rollback <version> --canary -d <description> -f <function_id> 
```


<span id="説明"></span>
## 説明


* `<version>`: *string, required*

   * 関数コードのバージョン。関数コードのバージョンは[nest versions](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-version-jp)を通じて取得できます。

* `--canary`: *boolean, optional*

   * ロールバックされたコードはカナリア環境にのみ公開されます。デフォルトは本番環境です。

* `<description>`: *string, optional*

   * バージョンの説明。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。これはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。関数名で指定されたローカル関数にまだ関数IDがない場合、エッジ関数 CLIは`Error: function id required`エラーを返します。
