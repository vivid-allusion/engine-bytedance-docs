---
title: "CLI概要"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-function-cli-overview-jp"
---

コンソールとOpenAPIに加えて、エッジ関数CLIを使用して関数とエッジKVを管理することもできます。コンソールとOpenAPIと比較して、エッジ関数CLIは以下の追加機能もサポートしています：


* 1つまたは複数のローカル関数を作成

* ローカル関数コードの編集とデバッグ

* 1つまたは複数のローカル関数のCRUD操作と公開

* ローカル関数とリモート関数の同期


エッジ関数CLIを使用すると、ローカルで関数コードを作成およびデバッグし、ローカルの関数コードをエッジ関数サーバーに公開することができます。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1babeb58b388df71bb7d2e1a07ee1cc6.png) </span>

<span id="基本概念"></span>
## 基本概念

エッジ関数CLIを使用する前に、以下の基本概念を理解することをお勧めします。

<span id="リモート関数"></span>
### リモート関数

エッジ関数サーバー上で作成された関数。各リモート関数には、識別子として一意の関数IDがあります。

<span id="ローカル関数"></span>
### ローカル関数

関数プロジェクトで作成された関数。ローカル関数をリモート関数のIDに関連付けることができます。

<span id="関数プロジェクト"></span>
### 関数プロジェクト

ローカル関数を管理するための関数プロジェクト設定ファイル（nest.json）を含むNode.jsプロジェクト。[nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp)を使用して関数プロジェクトを作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-jp">nest init</a>は、その関数プロジェクト内にローカル関数も作成します。</div>


関数プロジェクトには1つまたは複数のローカル関数を含めることができますが、デフォルト関数として設定できるのは1つのローカル関数のみです。[nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-jp#create)を使用して、関数プロジェクト内にローカル関数を作成できます。

<span id="プロジェクト設定"></span>
### プロジェクト設定

プロジェクト設定には、関数プロジェクトの作業ディレクトリ、エントリーコードファイルディレクトリ、関数プロジェクト内のすべてのローカル関数に関する情報、およびエッジKVデータに関する情報が含まれます。プロジェクト設定は、関数プロジェクト設定とグローバルプロジェクト設定に分類できます。


* **関数プロジェクト設定**：各関数プロジェクトのルートディレクトリにある`nest.json`ファイルに保存されます。関数プロジェクト設定ファイルは現在のプロジェクトに適用されます。

*  **グローバルプロジェクト設定**：`~/.nest.json`ファイルに保存されます。グローバルプロジェクト設定ファイルはすべての関数プロジェクトに適用されます。


エッジ関数CLIは、まず関数プロジェクト設定ファイルからプロジェクト設定を取得します。プロジェクト設定の取得に失敗した場合、エッジ関数CLIはグローバルプロジェクト設定ファイルからプロジェクト設定を取得します。
