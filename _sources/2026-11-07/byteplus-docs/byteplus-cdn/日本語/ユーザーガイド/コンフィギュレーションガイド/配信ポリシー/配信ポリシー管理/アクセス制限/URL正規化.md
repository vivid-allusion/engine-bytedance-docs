---
title: "URL正規化"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/url-normalization_jp"
---

このドキュメントでは、BytePlus CDNが提供するURL正規化機能について説明します。この機能により、ユーザーからのリクエストURLが仕様に準拠していないためにリクエストが失敗する可能性を低減できます。

<span id="機能概要"></span>
## 機能概要

ユーザーからのリクエストURLに非標準のコンテンツが含まれている場合、CDNはオリジンリクエストで同じURLを使用するため、オリジンサーバーはそのオリジンリクエストを処理できない可能性があります。同様に、CDNでパージまたはプリフェッチ操作を実行するときに、送信したURLに非標準のコンテンツが含まれている場合、パージおよびプリフェッチ操作の結果が期待どおりにならないことがあります。

この機能は、リクエストURLに含まれる以下の非標準コンテンツを正規化できます。


|**非標準コンテンツ**  |**正規化方法** |**例：非正規URL** |**例：正規化後のURL** |
|---|---|---|---|
|バックスラッシュ（\） |単一のスラッシュ（/）に置換 |https://www.example.com/img\test |https://www.example.com/img/test |
|連続するスラッシュ（//） |単一のスラッシュ（/）に置換 |https://www.example.com//img///test |https://www.example.com/img/test |
|/./ |単一のスラッシュ（/）に置換 |https://www.example.com/./img/test |https://www.example.com/img/test |
|/../ |* `/../` の前に別のディレクトリがある場合、`/../` とそのディレクトリを削除します。<br><br>* `/../` の前にディレクトリがない場合、元のURLを保持します。 |https://www.example.com/all/img/../test |https://www.example.com/all/test |
|||https://www.example.com/../test |https://www.example.com/../test |



* URL正規化は、ユーザーからのリクエストURLを正規化後のURLにリダイレクトしません。したがって、ユーザーのブラウザのアドレスバーのURLは変更されません。

* ユーザーからのリクエストを受信すると、URL 正規化設定が他の設定よりも優先されます。「URL 認証」機能は、正規化後のURLに基づいて動作します。


<span id="操作手順"></span>
## **操作手順**


1. **URL正規化** 設定ページを開きます。手順については、[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp) を参照してください。

2. **状態** を有効に設定します。

3. **設定** で、有効にするURL正規化オプションを選択します。

4. 設定が完了したら、**保存** をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d22e8909ae5249615eadbac60f9f59c0.jpg) </span>
