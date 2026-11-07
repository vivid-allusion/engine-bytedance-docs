---
title: "AIアシスタントで関数コードを編集する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use_ai_ide_for_code_jp"
---

このドキュメントでは、エッジ関数コンソールが提供するAIアシスタントを使用して関数コードを編集する方法について説明します。

AIアシスタントには、エッジ関数ランタイムAPIのサンプルコードが組み込まれており、大規模言語モデルの助けを借りて、関数コードの生成、修正、説明を行うことができます。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">AIアシスタントが生成したコードは参照用です。使用前に、その正確性と適用性を注意深く確認してください。</div>


* <div data-tips="true" data-tips-type="warning">AIアシスタントが提供するコードの説明は参照用です。エッジ関数の公式ドキュメントを参照してください。</div>



<span id="使用制限"></span>
## 使用制限

毎日の使用制限は次のとおりです。


*  **セッション数**：最大10セッションまで開始できます。

*  **メッセージ数**：各セッションで最大100メッセージまで送信できます。

*  **メッセージ長**：各メッセージは、全角250文字または半角500文字を超えることはできません。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">メッセージ長の制限には、コンテキストとして追加されたコードは含まれません。   </div>
   

<span id="デモ動画"></span>
## デモ動画

以下の動画では、AIアシスタントを使用して関数コードを生成、修正、説明する方法を素早くご理解いただけます。

<span id="コードを作成する"></span>
### コードを作成する

<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_abe07fda854e1fd2e7a9754d3d8e28f8.mp4" controls></video>


<span id="コードを修正する"></span>
### コードを修正する

<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1d6550971ceda26543f92ac36e684711.mp4" controls></video>


<span id="コードを説明する"></span>
### コードを説明する

<video src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3b5c6728c190d9d56aa1822c95642e23.mp4" controls></video>


<span id="手順"></span>
## 手順

AIアシスタントを使用するには、次の手順に従います。

<span id="ステップ1：aiアシスタントパネルを開く"></span>
### ステップ1：AIアシスタントパネルを開く

エッジ関数コンソールで、コードエディターの右上隅にあるAIアシスタントアイコンをクリックして、AIアシスタントパネルを開きます。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_99b73d83ef747dfc54d6562a294d4690.png) </span>

<span id="ステップ2：aiアシスタントでコードを生成する"></span>
### ステップ2：AIアシスタントでコードを生成する

AIアシスタントでコードを生成するには、次の手順に従います。


1. AIアシスタントパネルのダイアログボックスに要件を入力し、**送信** アイコンをクリックします。AIアシスタントは、要件を満たす関数コードを生成します。たとえば、次の要件を入力できます。


```text
ユーザーからのリクエストのHTTPリクエストヘッダーとユーザーに返されるレスポンスのレスポンスヘッダーを変更するコードを生成します。
- リクエストヘッダーにカスタムリクエストヘッダー「x-via-function-start」を現在のタイムスタンプを値として追加します。
- レスポンスヘッダーにカスタムレスポンスヘッダー「x-via-function-done」を現在のタイムスタンプを値として追加します。
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0d2e476699a7e3b6712757588735d7a7.png) </span>

2. 生成されたコードの右上隅にある  **コードを適用** アイコンをクリックして、コードをエディターに適用します。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_be7f45dbf48340d94e84c76ed895bf68.png) </span>

次に、コードをデバッグできます。[関数コードの編集とデバッグ](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-develop-and-test-function-jp) を参照してください。

<span id="その他の操作"></span>
## その他の操作

<span id="aiアシスタントでコードを修正する"></span>
### AIアシスタントでコードを修正する

デバッグ中に問題が見つかり、コードを修正する必要がある場合は、次の手順に従います。


1. コードエディターでコードの一部またはすべてを選択し、 **コードを修正** をクリックします。AIアシスタントがコードを修正します。

2. 生成されたコードの右上隅にある  **コードを適用** アイコンをクリックして、最適化または修正されたコードをエディターに適用します。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_27f678658df7bce26806bf794126e2d2.png) </span>

<span id="aiアシスタントでコードを説明する"></span>
### AIアシスタントでコードを説明する

AIアシスタントを使用してコードスニペットまたはコードファイル全体のロジックを理解したい場合は、コードエディターでコードの一部またはすべてを選択し、 **コードを説明** をクリックします。AIアシスタントがコードを説明します。

<span id="コードをセッションコンテキストとして追加する"></span>
### コードをセッションコンテキストとして追加する

コードスニペットまたはコードファイル全体をチャットのコンテキストとして追加する必要がある場合は、コードエディターでコードの一部またはすべてを選択し、 **チャットに追加** をクリックします。自然言語を使用して、コードの変更、コードの最適化などのニーズを説明できます。
