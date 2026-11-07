---
title: "CLIを用いて静的ウェブサイトをホスティングする"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/pages_host_webpage_jp"
---

このドキュメントでは、エッジ関数 Pages を使って静的ページをホスティングする方法を説明します。

<span id="エッジ関数-pages-とは"></span>
## エッジ関数 Pages とは

エッジ関数 Pages は、BytePlus エッジ関数が提供する静的ページのホスティングサービスです。開発者が静的サイトをグローバルなエッジノードネットワークへ迅速かつ効率的にデプロイできるようにします。エッジ関数 Pages を使うと、次のような静的コンテンツを簡単にホスティングできます（これらに限定されません）。


* 静的ウェブサイト（HTML/CSS/JavaScript）

* シングルページアプリケーション（SPA）

* ドキュメントサイト

* ブログ

* 静的アセットライブラリ


エッジ関数 Pages は、世界中に分散された BytePlus のエッジノードを活用し、静的アセットをユーザーに最も近いノードへキャッシュすることで、低レイテンシかつ高可用性のコンテンツ配信を実現します。

<span id="基本概念"></span>
## 基本概念

<span id="pages-インスタンス"></span>
### Pages インスタンス

Pages インスタンスは、エッジ関数で静的ページをホスティング・管理するための基本単位です。各 Pages インスタンスには一意の ID が付与されます。Pages インスタンスには複数のアセットを含めることができ、各アセットは静的サイトのバージョンに対応し、独自の一意な ID を持ちます。

Pages インスタンスを使うことで、静的ページのライフサイクルを集中的に管理できます。主な操作は次のとおりです。


* インスタンスの作成・設定・削除

* アセットバージョンのアップロード・デプロイ・管理


<span id="アセット（asset）"></span>
### アセット（Asset）

アセットは、Pages インスタンス内に保存される静的サイトのバージョンです。各アセットには静的サイトのファイル一式が含まれ、アップロード後に一意のアセット ID が生成されます。

<span id="利用制限"></span>
## 利用制限

エッジ関数 Pages の主な利用制限は次のとおりです。


* 各 BytePlus アカウントにつき、作成できる Pages インスタンスは最大 10 個

* 各インスタンスで保持できる履歴アセットは最大 100 個（超過分は自動クリーンアップ）

* 各インスタンスの毎月の最大デプロイ回数は 100 回

* 各アセットの gzip 圧縮済み tar パッケージのサイズは最大 50 MB

* 各アセットに含められるファイル数は最大 500 個

* 各アセット内の単一ファイルサイズは最大 25 MB


<span id="例示シナリオ"></span>
## 例示シナリオ

.html、.css、.js などのファイルを含む静的サイトプロジェクトを、エッジ関数 Pages で迅速にホスティング・公開したいとします。

<span id="実行環境の要件"></span>
## 実行環境の要件

エッジ関数 CLI を実行するデバイスは、次の要件を満たしている必要があります。


* 対応 OS：

   * ARM64 macOS

   * x86\-64 macOS

   * ARM64 Linux

   * x86\-64 Linux

* [Node.js](https://nodejs.org/) と [npm](https://www.npmjs.com/) がインストールされていること。バージョン要件：

   * Node.js：8.17.0+

   * npm：6.13.4+

* [wget](https://www.gnu.org/software/wget/) または [cURL](https://curl.se/) がインストールされていること。


<span id="手順"></span>
## 手順

<span id="手順-1：エッジ関数-cli-をインストールする"></span>
### 手順 1：エッジ関数 CLI をインストールする

エッジ関数 Pages はローカルの関数プロジェクトを必要としないため、CLI をグローバルにインストールできます。

```shell
npm install -g @byteplus/nest
```


<span id="手順-2：access-key-id-と-secret-access-key-を設定する"></span>
### 手順 2：Access Key ID と Secret Access Key を設定する

任意のディレクトリで次のコマンドを実行し、エッジ関数 CLI に BytePlus アカウントの Access Key ID と Secret Access Key を設定します。Access Key ID と Secret Access Key は [BytePlus コンソール](https://console.byteplus.com/iam/keymanage) から取得できます。

```shell
npx nest config set -g cloud.access_key <access_key_id>
npx nest config set -g cloud.secret_key <secret_access_key>
```


<span id="手順-3：pages-インスタンスを作成して公開する"></span>
### 手順 3：Pages インスタンスを作成して公開する


1. 静的アセット用のディレクトリを作成し、サイトのファイルを配置します。

   ```shell
   mkdir -p site
   # .html、.css、.js などの静的ファイルを site ディレクトリに配置します
   ```
   

2. 次のコマンドで Pages インスタンスを作成し、すぐに公開（デプロイ）します。

   ```shell
   npx nest pages create --name demo-site --assets ./site --deploy
   ```
   

   #### パラメータの説明    <span id="パラメータの説明"></span>

   
   |パラメータ |型 |必須 |説明 |
   |---|---|---|---|
   |\-\-name |string |はい |新しい Pages インスタンスの名前 |
   |\-\-assets |string |はい |ローカル静的アセットディレクトリのパス（index.html が必要） |
   |\-\-deploy |flag |いいえ |作成後すぐにインスタンスをデプロイするためのフラグ |
   

   成功すると、次のような出力が表示されます。

   ```shell
   ==> New Pages demo-site created!
   ==> [info]: Compressing given assets directory ./site...✓
   ==> [info]: Uploading assets...✓
   ==> [info]: Deploying pages...✓
   ==> Pages demo-site is publishing, you can visit it by open http://pywahntknjrhcufp.synthopages.bytepluses.com in browser a few minutes later
   ```
   

   公開が反映されるまで通常 1〜5 分かかります。反映後は、出力に表示されたドメインから静的サイトにアクセスできます。

   Pages インスタンスがまだカスタムドメインに関連付けられていない場合、システムはプレビュー用の一時的な公開ドメインを自動的に割り当てます。ドメインのサフィックスは synthopages.bytepluses.com です。なお、このドメインはプレビュー用途のみに使用されます。ブラウザで当該ドメインを開いて静的サイトを確認できます。


<span id="手順-4：静的サイトにカスタムドメインをバインドする"></span>
### 手順 4：静的サイトにカスタムドメインをバインドする

静的サイトへカスタムドメインでアクセスできるよう、Pages インスタンスにドメインを追加します。

```shell
nest pages domain add -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


成功すると、次のような出力が表示されます。

```Plain Text
==> [info]: Adding domain "wow.test.example.com" to pages p-2e9hpae39m2sqksy...✓
==> Domain wow.test.example.com was added successfully.
```


新しく追加したドメインは、正式に使用する前に検証（verify）が必要です。ドメインに CNAME レコードを追加してから、次のコマンドを実行して検証を行ってください。

```shell
nest pages domain verify -p p-2e9hpae39m2sqksy --domain wow.test.example.com
```


HTTPS でアクセスさせるには、該当ドメインの SSL/TLS 証明書をアップロードします。

```shell
# Pages インスタンスの指定ドメインに SSL/TLS 証明書を設定
nest pages domain update \
  -p p-2e9hpae39m2sqksy \
  --domain wow.test.example.com \
  --certificate ~/path/test.example.com.crt \
  --private-key ~/path/test.example.com.key
```
