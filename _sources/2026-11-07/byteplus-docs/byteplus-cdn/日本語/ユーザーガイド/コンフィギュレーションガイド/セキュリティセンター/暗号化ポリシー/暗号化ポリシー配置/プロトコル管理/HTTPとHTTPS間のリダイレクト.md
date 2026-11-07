---
title: "HTTPとHTTPS間のリダイレクト"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/protocol-redirect-jp"
---

本ドキュメントでは、BytePlus CDNでドメイン名のHTTPとHTTPS間のリダイレクトを設定する方法について説明します。

<span id="前提条件"></span>
## 前提条件

この設定を有効にするには、ドメイン名がすでにHTTPS暗号化サービスを有効にしている必要があります。

<span id="操作手順"></span>
## 操作手順


1. **HTTPとHTTPS間のリダイレクト**  設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **HTTPとHTTPS間のリダイレクト** の下で、**状態**を**有効**に設定します。

3. 以下の設定説明を参照してください。



|**設定** |**説明** |
|---|---|
|ポリシー |リダイレクトのポリシーを設定します。この設定には以下のオプションがあります：<br><br><br>*  **リダイレクトなし** ：ユーザーリクエストで使用されているプロトコルをリダイレクトしません。<br><br>* **HTTPをHTTPSへのリダイレクト** ：ユーザーリクエストで使用されているプロトコルがHTTPの場合、HTTPSへリダイレクトします。<br><br>* **HTTPSをHTTPへのリダイレクト** ：ユーザーリクエストで使用されているプロトコルがHTTPSの場合、HTTPへリダイレクトします。 |
|リダイレクト種類 |CDNがリダイレクトに使用するステータスコードを示します。 **ポリシー** が**HTTPをHTTPSへのリダイレクト** または**HTTPSをHTTPへのリダイレクト** の場合に、この設定が表示されます。この設定には以下のオプションがあります：<br><br><br>* **301**：レスポンスステータスコードが301であることを示します。<br><br>* **302**：レスポンスステータスコードが302であることを示します。 |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c6eb5449726cd9631a419608976b04ba.jpeg) </span>


9. 設定が完了したら、**保存**をクリックします。
