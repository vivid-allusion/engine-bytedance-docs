---
title: "CLIリリースノート"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-release-notes-jp"
---

本ドキュメントにはエッジ関数CLIのリリースノートが含まれています。

<span id="v1-3-0"></span>
## v1.3.0

本バージョンは 2025 年 11 月 28 日にリリースされました。

<span id="新機能"></span>
### 新機能

<span id="pages-cli-のサポート"></span>
#### Pages CLI のサポート

エッジ関数PagesはBytePlusエッジ関数が提供する静的ページのホスティングサービスで、開発者が静的サイトをグローバルなエッジノードネットワークに迅速かつ効率的にデプロイできるよう設計されています。現在、エッジ関数CLIを通じてエッジ関数Pages を利用できます。[nest pages](https://docs.byteplus.com/en/docs/byteplus-cdn/nest_pages_jp) を参照してください。

<span id="v1-2-0"></span>
## v1.2.0

このバージョンは2025年7月16日にリリースされました。

<span id="新機能"></span>
### 新機能

<span id="opa対応関数プロジェクトのサポート"></span>
#### OPA対応関数プロジェクトのサポート

OPA関数テンプレートを使用して、[Open Policy Agent (OPA)](https://www.openpolicyagent.org/) に対応する関数プロジェクトを作成できます。詳細については、[OPA関数プロジェクトを作成する](https://docs.byteplus.com/en/docs/byteplus-cdn/create_function_project_with_opa_jp)を参照してください。

<span id="バグ修正"></span>
#### バグ修正

[nest debug](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-jp#query)の `-X` パラメータが効かない問題を修正しました。

<span id="v1-1-1"></span>
## v1.1.1

このバージョンは2025年6月23日にリリースされました。

<span id="新機能"></span>
### 新機能

<span id="mcpサーバー"></span>
#### MCPサーバー

エッジ関数CLIは、大規模言語モデルによってMCPサーバーとして呼び出すことができます。詳細は[MCPサーバー概要](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-mcp-server-overview-jp)をご参照ください。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aea6754b6ccb417ef1ba7c66be43ab6f.png) </span>

<span id="関数プロジェクトのディレクトリを指定"></span>
#### 関数プロジェクトのディレクトリを指定

[nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-jp) コマンドに、関数プロジェクトを作成するディレクトリを指定するための `<dir>` パラメータが追加されました。

<span id="新しいsimple-page関数テンプレート"></span>
#### 新しいSimple Page関数テンプレート

組み込み関数テンプレートにSimple Pageテンプレートが追加されました。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_087b92ded847576a99e3af520edd0d6a.png) </span>

Simple Pageテンプレートは、簡単なWebページを返す方法を示します。このテンプレートを使用するために、アクセスキーIDとシークレットアクセスキーを設定する必要はありません。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_28b2ac5593a80a359f39296478e033ef.png) </span>

<span id="地域制限機能の追加"></span>
#### 地域制限機能の追加

関数またはストレージスペースを作成する際に、関数の公開地域またはKVデータのストレージ地域を中国本土に限定するかどうかを設定できます。

以下のコマンドに \-\-cn パラメータが追加されました：


* [nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-jp)：\-\-cn パラメータは、関数の公開地域を中国本土に限定するかどうかを設定するために使用されます。

* [nest functions create](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-jp#create)：\-\-cn パラメータは、関数の公開地域を中国本土に限定するかどうかを設定するために使用されます。

* [nest kv namespace create](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-jp#create)：\-\-cn パラメータは、KVデータのストレージ地域を中国本土に限定するかどうかを設定するために使用されます。


以下のコマンドの戻り値にREGION列が追加されました：

\- [nest functions list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-function-jp#list)：戻り値にREGION列が追加され、関数の公開地域が中国本土に限定されているかどうかを表示します。

\- [nest kv namespace list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-kv-jp#list)：戻り値にREGION列が追加され、KVデータのストレージ地域が中国本土に限定されているかどうかを表示します。

また、関数設定ファイルnest.jsonのfunctionsオブジェクトとkvオブジェクトにもRegionフィールドが追加されました。

<span id="バグ修正"></span>
### バグ修正


* [nest init](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-init-jp) コマンドで生成されたpackage.jsonファイル内の `devDependencies` 下にある `@byteplus/nest` の名前が間違っていた問題を修正しました。

* [nest domain list](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-jp) が表示するドメインの状態がコンソールと一致しない問題を修正しました。


<span id="最適化"></span>
### 最適化


* 新しいバージョンのエッジ関数OpenAPIと連携しました。

* [nest domain bind](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-domain-jp) コマンドに、転送ルールの可用性チェックロジックが追加されました。

* [nest debug source](https://docs.byteplus.com/en/docs/byteplus-cdn/cli-ref-nest-debug-jp) コマンドは、任意のディレクトリ内の.jsファイルをデバッグできるようになりました。

* nest.jsonで手動編集したエッジKVデータを公開する際、`@`記号を使用してローカルファイルをKVキーバリューペアの値として参照できるようになりました。


<span id="v1-0-0"></span>
## v1.0.0

このバージョンは2025年3月13日にリリースされました。これはエッジ関数CLIの最初のバージョンです。
