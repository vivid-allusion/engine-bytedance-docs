---
title: "エッジKVを使い始める"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-EdgeKV-overview-jp"
---

このチュートリアルでは、簡単な例のシナリオに基づいて、エッジ関数でエッジKVを使用する方法を紹介します。

エッジKVサービスは、BytePlusのグローバルエッジノード上の分散キーバリューストレージサービスです。エッジ関数コンソール、OpenAPI、またはランタイムAPIを通じてキーバリューペアがエッジKVに書き込まれると、自動的にすべてのエッジノードに同期されます。関数は、ランタイムAPIを通じて同じエッジノード上にあるキーバリューペアを迅速に読み取ることができます。

<span id="例のシナリオ"></span>
## 例のシナリオ

あなたのウェブサイトはA/Bテスト機能をサポートしており、ユーザーの地理的位置に基づいて異なるバージョンのウェブページを返すことができます。バージョン切り替えの設定情報はエッジKVに保存されています。関数のコードからバージョン切り替えの設定情報を読み取りたいとします。このチュートリアルでは、設定情報が以下のようであると仮定します：

```json
{
  "us": "versionA",
  "eu": "versionB",
  "asia": "versionA"
}
```


<span id="操作手順"></span>
## 操作手順

例のシナリオを実装するには、以下の手順を完了する必要があります。


1. 名前空間を作成する。

2. 名前空間内にキーバリューペアを作成する。

3. 関数コードでキーバリューペアから値を読み取る。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0d1c8fcccb3a3cf1266d9043df2d253c.png) </span>

<span id="ステップ1：名前空間を作成する"></span>
### ステップ1：名前空間を作成する

以下の手順に従って名前空間を作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">名前空間の作成はコンソールまたはOpenAPIを使用してのみ可能です。ランタイムAPIを使用して名前空間を作成することはできません。</div>



1. [エッジKV](https://console.byteplus.com/cdn/edge-function/list)ページを開きます。

2.  **エッジKV**ページで、**名前空間を作成**をクリックします。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bb75b73e2b740c439dc5ad20537ceefb.png) </span>

3. **名前空間を作成**ダイアログボックスで、以下のパラメータを設定し、**保存**をクリックします。

   
   |パラメータ |説明 |
   |---|---|
   |名前 |`abtest_config`に設定します。 |
   |説明 |`demo`に設定します。 |
   |プロジェクト |`default`に設定します。 |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_293f16320831a4bb6a66b2d6bad1d789.png) </span>


<span id="ステップ2：名前空間内にキーバリューペアを作成する"></span>
### ステップ2：名前空間内にキーバリューペアを作成する

以下の手順に従って名前空間内にキーバリューペアを作成します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">キーバリューペアの作成は、コンソール、OpenAPI、またはランタイムAPIを使用して行うことができます。</div>



1. [エッジKV](https://console.byteplus.com/cdn/edge-function/list)ページを開きます。

2. 作成した`abtest_config`名前空間を見つけ、名前空間の名前をクリックします。

3.  **データを追加**をクリックします。

4. 表示される **データを追加**ダイアログボックスで、データの関連パラメータを設定し、**保存**をクリックします。

   
   |パラメータ |説明 |
   |---|---|
   |キー |`config_key`に設定します。 |
   |値 |例のシナリオのJSON値に設定します：`{"us":"versionA","eu":"versionB","asia":"versionA"}` |
   |TTL |**無期限**に設定します。 |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_20d45e3ff01bb50d21bd15f575a71310.png) </span>


<span id="ステップ3：関数コードでキーバリューペアから値を読み取る"></span>
### ステップ3：関数コードでキーバリューペアから値を読み取る

以下の手順に従って、関数コードでキーバリューペアから値を読み取ります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">キーバリューペアの値の読み取りは、コンソール、OpenAPI、またはランタイムAPIを使用して行うことができます。</div>


関数コードで、[KV.get()](https://docs.byteplus.com/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI-jp)を呼び出してキーバリューペアの値を取得します。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">エッジ関数のデバッグ環境は現在、<a href="https://docs.byteplus.com/docs/byteplus-cdn/docs-EdgeKV-RuntimeAPI-jp">エッジKVランタイムAPI</a>の実行をサポートしていません。エッジKVランタイムAPIは本番環境でのみ実行できます。</div>


```JavaScript
const config = await KV.get("abtest_config","config_key",{type:"string"});
```
