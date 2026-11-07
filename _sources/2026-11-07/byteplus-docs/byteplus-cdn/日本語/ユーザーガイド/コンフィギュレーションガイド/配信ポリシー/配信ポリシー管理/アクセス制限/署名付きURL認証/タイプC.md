---
title: "タイプC"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/Type-C-jp"
---

このドキュメントでは、BytePlus CDNのURL認証モジュール内のタイプC認証の設定について説明します。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ef58355cd4d31eeee6a05feb751cfd4d.jpeg) </span>

<span id="コンソールでの設定"></span>
##  **コンソールでの設定**

CDNコンソールでは、以下の設定が必要です：


|**設定** |**説明** |
|---|---|
|認証ルール |一つの一致条件を表します。CDNは条件に合致するユーザーリクエストに対して認証を行います。条件には一致タイプ、一致方法、一致値が含まれます。CDNがユーザーリクエストを受信すると、この条件とリクエストを照合します。条件がリクエストと一致する場合、CDNはそのリクエストを認証します。<br><br>&nbsp;<br><br>一致値の総文字数は1,024文字を超えてはならず、以下のいずれの文字も含むことはできません：<br><br><br>* 連続したスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）、Delete（ASCII コード 127）。<br><br><br>また、<br><br><br>* 一致タイプが**URLパス拡張子**の場合、一致値はセミコロン（;）で区切られた1つ以上のURLパス拡張子でなければなりません。URLパス拡張子はピリオド（.）で始める必要はありません。例：`png;txt`。<br><br>* 一致タイプが**URLパスディレクトリ** の場合、一致値と一致タイプはシステムのデフォルト値のみを使用できます。デフォルト値は、すべてのファイルのリクエストが認証を必要とすることを意味します。 |
|プライマリキー |プライマリキーを指定します。キーは6〜40文字で構成され、削除（ASCIIコード127）を除く印刷可能なASCII文字のみを含むことができます。 |
|セカンダリキー |セカンダリキーを指定します。セカンダリキーの入力要件はプライマリキーと同じです。認証が失敗した場合、CDNはセカンダリキーを使用して署名を再計算し、クライアントリクエストの署名とマッチするか試みます。 |
|署名TTL |署名の有効期間を秒単位で指定します。この設定は、クライアントリクエストの`timestamp`パラメータと組み合わせて、署名の有効期限を計算するために使用されます。このパラメータの範囲は0〜315,360,000です。署名の有効期限 = タイムスタンプ + 有効期間。CDNがリクエストを受信したとき、リクエスト内の署名の有効期限が現在時刻よりも早い場合、CDNは署名が期限切れであると判断します。この時点で、CDNはリクエストを拒否し、403応答ステータスコードを返して認証失敗を示します。コンソールのデフォルトの有効期間は`1800`です。 |


<span id="リクエストurlフォーマット"></span>
## リクエストURLフォーマット

```XML
scheme://host/<signature>/timestamp/uri(?query_params)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">timestampの精度は秒単位です。</div>


<span id="リクエストurlの例"></span>
## リクエストURLの例

```XML
https://www.example.com/b1725c0a6120092863001cd8004c4adb/6093AF7D/product/cdn?query1=value1&query2=value2
```


<span id="署名アルゴリズム"></span>
## 署名アルゴリズム

`<SIGNATURE>` の署名アルゴリズムは以下の通りです：

```XML
md5(key + uri + timestamp)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">アルゴリズム内の '+'はパラメータ値の連結を表し、実際の文字ではありません。</div>


* <div data-tips="true" data-tips-type="tip">MD5の値は32文字の16進数で構成されています。</div>



署名アルゴリズムのパラメータの説明は以下の通りです：


| **パラメータ**  |**説明** |
|---|---|
|key |CDNコンソールで設定されたシークレットキーを表します。 |
|uri |[リクエストURL形式](https://docs.byteplus.com/en/docs/18/32315#%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88URL%E5%BD%A2%E5%BC%8F)の`uri`パラメータを表し、スラッシュ（/）で始まり、ドメイン名を含みません。パスに中国語の文字が含まれている場合は、パスをエンコードする必要があります。[リクエストURLの例](https://docs.byteplus.com/en/docs/18/32315#%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88URL%E3%81%AE%E4%BE%8B)では、このパラメータの値は`/product/cdn`です。 |
|timestamp |[リクエストURL形式](https://docs.byteplus.com/en/docs/18/32315#%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88URL%E5%BD%A2%E5%BC%8F)の`timestamp`パラメータを表し、10進数のUnixタイムスタンプ形式です。このパラメータはコンソールの**署名TTL**設定と組み合わせて、署名の有効期限を計算するために使用されます。[リクエストURLの例](https://docs.byteplus.com/en/docs/18/32315#%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88URL%E3%81%AE%E4%BE%8B)では、このパラメータの値は`6093AF7D`です。 |


<span id="認証プロセス"></span>
## 認証プロセス

CDNが署名を含むクライアントリクエストを受信した際の認証プロセスは以下の通りです：


1. リクエストに含まれる認証パラメータとCDNコンソールで設定されたシークレットキーを使用して、[署名アルゴリズム](https://docs.byteplus.com/en/docs/18/32315#%E7%BD%B2%E5%90%8D%E3%82%A2%E3%83%AB%E3%82%B4%E3%83%AA%E3%82%BA%E3%83%A0)に基づいて署名を計算します。

2. CDNが計算した署名がクライアントリクエストに含まれる署名と一致するかどうかを判断します。一致しない場合、CDNはリクエストを無効とみなし、拒否します。

3. リクエストが期限切れかどうかを判断します。以下の条件が満たされた場合、CDNはリクエストを拒否します：

   * （クライアントリクエストのタイムスタンプパラメータ）+（CDNコンソールで設定された署名の有効期限）<（CDNがリクエストを受信した時間）
