---
title: "nest upload"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-upload-jp"
---

ローカル関数のコードをリモート関数にアップロードします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">このコマンドを使用するには、BytePlusアカウントのAccess Key IDとSecret Access Keyを設定する必要があります。<a href="https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-cli-login-jp">Access Key IDとSecret Access Keyを設定する</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">このコマンドは関数プロジェクトのルートディレクトリで実行する必要があります。<code>nest init</code>を使用して関数プロジェクトを作成する必要があります。</div>



<span id="概要"></span>
## 概要

```shell
npx nest upload --no-build --create --function <function_id_or_name>
```


<span id="説明"></span>
## 説明


* `--no-build`: *boolean, optional*

   * 圧縮を無効にします。デフォルトでは、エッジ関数CLIは自動的にコードを圧縮します。

* `--create`: *boolean, optional*

   * 新しいリモート関数を作成します。デフォルトでは、新しいリモート関数は作成されません。

* `<function_id_or_name>`: *string, optional*

   * 関数IDまたは関数名。このパラメータはグローバルパラメータです。[--function](https://docs.byteplus.com/docs/byteplus-cdn/edge-functions-global-f-jp)を参照してください。デフォルトは[ローカル関数リスト](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#list)のデフォルト関数です。名前で指定した関数にまだ関数IDがない場合、エッジ関数CLIは新しいリモート関数を作成するよう促します。
