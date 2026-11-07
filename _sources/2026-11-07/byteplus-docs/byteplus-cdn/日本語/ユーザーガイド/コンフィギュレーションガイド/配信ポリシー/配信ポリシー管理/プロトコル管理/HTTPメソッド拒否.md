---
title: "HTTPメソッド拒否"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/unsupported-http-method-jp"
---

本ドキュメントでは、BytePlus CDNで拒否されるHTTPトメソッドを指定する方法について説明します。

<span id="httpメソッドについて"></span>
## HTTPメソッドについて

HTTPメソッドは、リソースリクエストの方法を指定します。異なるHTTPトメソッドには特定の使用シーンがあります。デフォルトでは、CDNはユーザーが以下のHTTPトメソッドを使用してドメイン名にアクセスすることを許可しています。


* GET

* POST

* HEAD

* DELETE

* PUT

* PATCH

* CONNECT

* OPTIONS


必要に応じて、CDNが拒否されるHTTPメソッドを設定できます。ユーザーリクエストが拒否されるHTTPメソッドを使用した場合、CDNはそのリクエストを拒否し、405レスポンスステータスコードを返します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">GETとPOSTは、ユーザーがCDNにアクセスする際に一般的に使用されるHTTPトメソッドであるため、無効にすることはお勧めしません。</div>


* <div data-tips="true" data-tips-type="tip">CDNがオブジェクトストレージにオリジンリクエストを送信する際、オリジンリクエストはユーザーリクエストと同じHTTPメソッドを使用します。デフォルトでは、CDNはDELETE、GET、HEAD、POST、PUT、PATCH、CONNECT、OPTIONSのHTTPトメソッドをユーザーリクエストでサポートしています。特定のHTTPトメソッドを使用したオリジンリクエストがオリジンサーバーにアクセスすることを望まない場合（例えば、DELETEメソッドを使用したリクエストがオリジンサーバー上のファイルを削除することを望まない場合）、以下のすべての操作を実行することをお勧めします：</div>


   * <div data-tips="true" data-tips-type="tip">提供されたAK/SKに対応するクラウドベンダーアカウントについて、クラウドベンダーで権限を設定し、そのアカウントがオブジェクトストレージオリジンサーバー上で特定の操作を実行することを禁止します。</div>


   * <div data-tips="true" data-tips-type="tip">「HTTPメソッド拒否」設定で、CDNが拒否されるユーザーリクエストのHTTPメソッドを指定します。</div>



<span id="操作手順"></span>
## 操作手順


1. **HTTPメソッド拒否**設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **HTTPメソッド拒否**の下で、**状態**を**有効**に設定します。

3. 拒否されるHTTPメソッドにチェックを入れ、**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6fdf7e71a21f4211a75c2ad71ab9bf48.jpeg) </span>
