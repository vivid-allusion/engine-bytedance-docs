---
title: "URLを書き換え"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-rewrite-jp"
---

本ドキュメントでは、BytePlus CDNでオリジンパスの書き換えを設定する方法について説明します。この設定により、CDNのオリジンリクエストのパスを書き換えることができます。

オリジンサーバー上で、ユーザーが頻繁にアクセスするファイルのパスが変更された場合、以下のような解決策があります：


* オリジンサーバーで301または302リダイレクトを設定し、コンテンツの元のURLを新しいURLにリダイレクトします。同時に、CDNで[リダイレクトフォロー](https://docs.byteplus.com/en/docs/byteplus-cdn/redirect-follow-jp)機能を有効にします。

* オリジンサーバーでは変更を行わず、CDNで[URLリダイレクト](https://docs.byteplus.com/en/docs/byteplus-cdn/url-redirect-jp)機能を設定します。ユーザーが元のURLをリクエストした場合、CDNは301または302ステータスコードを返し、ユーザーのブラウザに新しいURLへのリクエストを指示します。

* オリジンサーバーでは変更を行わず、CDNで**URLを書き換え** を設定します。ユーザーが元のURLをリクエストした場合、CDNはオリジンリクエストで新しいURLを使用します。


本ドキュメントでは、3番目の解決策について説明します。

<span id="リクエストフロー"></span>
##  **リクエストフロー** 

あるファイルにオリジンパス書き換えを設定した後のリクエストフローは以下の通りです：


1. ユーザーがファイルをリクエストします。

2. そのファイルがキャッシュされていない場合、CDNは設定に基づいて、オリジンリクエストでユーザーリクエストURLのパスを新しいパスに書き換えます。

3. CDNがファイルを取得した後、そのファイルをユーザーに返し、キャッシュします。注意すべき点は、そのファイルのキャッシュキーのURLはユーザーリクエストのURLであることです。


<span id="操作手順"></span>
## 操作手順


1. **URLを書き換え** 設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **URLを書き換え** の下で、 **ルールを追加**をクリックします。

   最大50個のルールを追加できます。

3. 以下の設定説明を参照してください。

4. 設定が完了したら、**保存**をクリックします。



|**設定** |**説明** |
|---|---|
|優先度 |ルールの優先度を表します。数字1のルールが最も優先度が高くなります。リクエストを受信すると、CDNはルールの優先度に従って、高いものから低いものへとリクエストとルールのマッチングを試みます。リクエストがあるルールにマッチした場合、CDNは残りのルールのマッチングを停止します。ドラッグアンドドロップでルールの優先度を調整できます。 |
|リクエストパス |ユーザーからのリクエストURLのパスを表し、長さは1,024文字を超えないようにします。パスにはプロトコル、ドメイン名、パラメータは含まれません。<br><br>&nbsp;<br><br>この設定で正規表現を使用できます。この場合、この設定はマッチングルールを表します。同時に、正規表現内でグループを指定できます。グループは`()`で囲まれます。これらのグループは **パスの書き換え** 設定で参照できます。例えば、`^/aaa/bbb/(.*)`は`/aaa/bbb/`以下のすべてのディレクトリとファイルを表します。この例には1つのグループが含まれています。 |
|パスの書き換え |オリジンパスで **リクエストパス** を置き換えるパスを表します。この設定の要件は以下の通りです：<br><br><br>* 長さは1,024文字を超えないこと。<br><br>* スラッシュ（/）で始まること。<br><br>* 連続したスラッシュ（//）、パーセント記号（%）、スペース、疑問符（?）を含まないこと。<br><br>* プロトコル、ドメイン名、クエリ文字列を含まないこと。<br><br><br>デフォルトでは、CDNはリクエストURLのクエリ文字列を実際のオリジンURLに追加します。<br><br> **リクエストパス** 設定に正規表現が含まれ、その正規表現に1つ以上のグループが含まれている場合、 **パスの書き換え** 設定で`$<n>`を使用して使用するグループを指定できます。`$1`は最初のグループ、`$2`は2番目のグループを表し、以降も同様です。この場合、この設定はマッチングルールを表します。<br><br>&nbsp;<br><br> **リクエストパス** 設定の例に基づいて、オリジンパスを`/ccc/$1`と指定したとします。`/ccc/$1`は`/ccc/`で始まるパスを表します。パスの残りの部分は **リクエストパス** の`.*`で表される部分になります。ユーザーリクエストURLが`https://www.example.com/aaa/bbb/test/myfile.png`の場合、オリジンパスは`https://www.example.com/ccc/test/myfile.png`に書き換えられます。 |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_05e31ea0edadd980844d6f5fdb1684e7.jpeg) </span>

<span id="設定例"></span>
## 設定例

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">正規表現のテストツールを使用して正規表現をテストすることをお勧めします。たとえば、検索エンジンでキーワード <code>オンライン正規表現テスト</code> を使用してオンラインのテストツールを検索できます。</div>


<span id="パス書き換え設定例"></span>
### パス書き換え設定例


| **ユーザーからのリクエスト**  |**設定** |**設定** |**設定結果** |**説明** |
|---|---|---|---|---|
| **リクエスト URL のパス**  | **ユーザーからのリクエストパス（グループ **  **`(.*)`**  ** を含む）**  | **オリジンパス**  | **リダイレクトパス**  ||
|/a/bbb/image.png |^/a{1,2}(.\*)g$<br><br>&nbsp;<br><br>`/` で始まり `g` で終わるパスを一致させるために使用されます。 |/food/$1 |/food//bbb/image.pn |正規表現がリクエストパスに一致しました。`(.*)` が表す文字列は `/bbb/image.pn` です。<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">リダイレクトパスに <code>//</code> が含まれているため、このパスは無効です。また、ファイル拡張子も正しくありません。</div><br> |
|||/food$1g |/food/bbb/image.png |正規表現がリクエストパスに一致しました。`(.*)` が表す文字列は `/bbb/image.pn` です。 |
|/aaa/bbb/image.png |/a{1,2}(.\*)g<br><br>&nbsp;<br><br>リクエストパス内の特定の文字列を一致させるために使用されます。 |/food/$1g |/food/a/bbb/image.png |* 正規表現がリクエストパスに一致しました。<br><br>* `(.*)` が表す文字列は `a/bbb/image.pn` です。 |
|/food/aaa/pngs/image.png |||/food/a/pngs/image.png |* 正規表現がリクエストパスに一致しました。<br><br>* `(.*)` が表す文字列は `a/pngs/image.pn` です。 |
|/aaa/bbb/image.png |aaa(.\*)<br><br>&nbsp;<br><br>リクエストパス内の特定の文字列を一致させるために使用されます。 ||/food//bbb/image.pngg |* 正規表現がリクエストパス内の `aaa/bbb/image.png` に一致しました。<br><br>* `(.*)` が表す文字列は `/bbb/image.png` です。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">リダイレクトパスに <code>//</code> が含まれているため、このパスは無効です。また、ファイル拡張子も正しくありません。</div><br> |
|/aaa/bbb/image.png |aaa/(.\*)<br><br>&nbsp;<br><br>リクエストパス内の特定の文字列を一致させるために使用されます。 |/food/$1 |/food/bbb/image.png |* 正規表現がリクエストパス内の `aaa/bbb/image.png` に一致しました。<br><br>* `(.*)` が表す文字列は `bbb/image.png` です。 |
