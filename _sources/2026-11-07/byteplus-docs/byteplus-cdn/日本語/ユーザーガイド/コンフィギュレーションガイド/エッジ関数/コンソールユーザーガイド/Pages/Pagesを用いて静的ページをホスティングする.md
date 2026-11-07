---
title: "Pagesを用いて静的ページをホスティングする"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/host_static_pages_console_ja"
---

本文書では、コンソールで Pages を使用して静的ページをホスティングする方法について説明します。

<span id="pages-とは"></span>
## Pages とは

Pages は、BytePlus エッジ関数が提供する静的ページホスティングサービスです。静的ウェブサイトを世界中のエッジノードネットワークに迅速かつ効率的にデプロイできるように設計されています。BytePlus Pages を使用すると、以下を含む（ただしこれらに限定されない）さまざまな種類の静的コンテンツを簡単にホスティングできます。


* 静的ウェブサイト（HTML/CSS/JavaScript）

* シングルページアプリケーション（SPA）

* ドキュメントサイト

* ブログ

* 静的アセットライブラリ


Pages は、世界中に分散された BytePlus エッジノード上に構築されており、静的アセットをユーザーに最も近いエッジノードにキャッシュすることで、低遅延かつ高可用性のコンテンツ配信を実現します。

<span id="使用制限"></span>
## 使用制限

Pages の使用制限は以下の通りです。


* 各 BytePlus アカウントは、最大 10 個の Pages インスタンスを作成できます。

* 各 Pages プロジェクトは、最大 100 件の履歴デプロイを保持し、超過したデプロイは自動的に削除されます。

* 各 Pages インスタンスは、1 か月あたり最大 100 回デプロイできます。

* 各 zip パッケージのサイズは 50 MB を超えてはなりません。

* 各 zip パッケージ内のファイル数は 500 個を超えてはなりません。

* 各 zip パッケージ内の単一ファイルのサイズは 25 MB を超えてはなりません。


<span id="操作手順"></span>
## 操作手順

<span id="手順-1：pages-プロジェクトを作成する"></span>
### 手順 1：Pages プロジェクトを作成する


1. [Pages ページ](https://docs.byteplus.com/en/docs/18/(https://console.byteplus.com/cdn/cdn-bp/synthopages/list))で、 **プロジェクトを作成** をクリックします。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aa8eec9ae8e953bb9d1ba0ec895c4968.png) </span>

2.  **プロジェクトを作成** ページで、以下のパラメータを設定し、**作成する**  をクリックします。

   
   |カテゴリ |パラメータ |説明 |
   |---|---|---|
   | |**方法** | **ファイルをアップロード**  を選択します。 |
   | | **ファイルをアップロード**  |静的ウェブサイトの .html、.js、または .css ファイルを含む .zip 形式のファイルパッケージをアップロードします。圧縮前のパッケージ内の単一ファイルのサイズは 25 MB を超えてはなりません。パッケージには index.html エントリファイルを含める必要があります。 |
   |**一般設定** | **プロジェクトページ名** |Pages プロジェクト名を入力します。 |
   || **プロジェクトの説明** （任意） |Pages プロジェクトの説明を入力します。 |
   || **プロジェクト**  |所属する BytePlus プロジェクトを選択します。 |
   || **サービスエリア**  |アクセラレーションリージョンを選択します。**中国本土以外のリージョン**  のみがサポートされています。 |
   | **サービス設定** | **ドメイン** （任意） |カスタムドメインを関連付けることを選択できます。Pages インスタンスにカスタムドメインがまだ関連付けられていない場合、システムはプレビュー用に一時的なパブリックドメインを自動的に割り当てます。 |
   


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e9d3dfead59b548287a5dad5d39fa94f.png) </span>

作成が成功すると、静的ウェブサイトは自動的にデプロイされます。

<span id="手順-2：pages-プロジェクトのドメインを設定する"></span>
### 手順 2：Pages プロジェクトのドメインを設定する


1. **Pages** ページで、手順 1 で作成した Pages プロジェクトを見つけ、プロジェクト名をクリックして詳細ページに入ります。

    **プレビューリンク**  の下のリンクからデプロイをプレビューできます。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_eab7d3394fb85b70615755b031c89109.png) </span>


2. プロジェクト作成時にカスタムドメインをすでに追加している場合、または新しいカスタムドメインをバインドする必要がある場合は、カスタムドメインの DNS サービスプロバイダーのコンソールに移動し、CNAME レコードを追加して、カスタムドメインを BytePlus Pages が提供する CNAME アドレスに向けてください。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">GoDaddy を例にとると、CNAME レコードを追加する手順は以下の通りです。   </div>
   

   1. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">GoDaddy の <strong>Domain Portfolio</strong> にログインします。   </div>
   

   2. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">設定するドメインを選択し、<strong>DNS Management</strong> ページに入ります。   </div>
   

   3. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Add New Record</strong> をクリックし、<strong>Type</strong> として <strong>CNAME</strong> を選択します。   </div>
   

   4. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">以下の情報を入力します。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Name</strong>：サブドメインを入力します（例：<code>www</code>）。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Value</strong>：Pages プロジェクトが提供する CNAME アドレスを入力します（例：<code>your-project.synthopages.bytepluses.com</code>）。   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>TTL</strong>：デフォルト値を使用するか、必要な時間に設定できます（例：<code>1 Hour</code>）。   </div>
   

   5. <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Save</strong> をクリックして設定を保存します。   </div>
   

3. 設定が完了したら、**検証** をクリックします。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0a6a12b18c0a18a17c802237396f898b.png) </span>

   検証が完了すると、カスタムドメインを介して静的ウェブサイトにアクセスできるようになります。


<span id="その他の操作"></span>
## その他の操作

<span id="ドメインを追加する"></span>
### ドメインを追加する

Pages プロジェクト詳細ページの  **ドメイン管理** エリアで、 **ドメインを追加** をクリックすると、プロジェクトにさらにカスタムドメインを追加できます。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_67a83fe023f10c360bb8c9dd74eac13a.png) </span>

<span id="デプロイをダウンロードする"></span>
### デプロイをダウンロードする

Pages プロジェクト詳細ページの  **デプロイメント**  エリアで、ダウンロードする必要があるデプロイを見つけ、**操作** 列の  **ダウンロード**  をクリックします。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_68bf9949b1411695de3e505615171021.png) </span>

<span id="デプロイを更新する"></span>
### デプロイを更新する

Pages プロジェクト詳細ページの  **デプロイメント**  エリアで、**新しいデプロイ**  をクリックします。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e5f2d8bfa25a9f72fed2e1a3233e30c6.png) </span>

デプロイの作成ページで静的ウェブサイトの zip パッケージを再アップロードすると、デプロイを更新できます。
