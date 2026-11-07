---
title: "DescribeCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCipherTemplate_jp"
---

暗号化ポリシーの設定詳細を取得します。


* ポリシーが公開されている場合、APIはデフォルトで公開済み（ステータスが`running`）のバージョンの設定詳細を返します。

* ポリシーが公開されていない場合、APIはデフォルトでステータスが`draft`のバージョンの設定詳細を返します。


ポリシー内の特定のバージョンを指定して、そのバージョンの設定詳細を取得することもできます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeCipherTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |クエリ対象の暗号化ポリシーのIDを示します。<br><br>[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp)を使用して、クエリ対象の暗号化ポリシーのIDを取得できます。 |`tpl-c2PRDW` |
|TemplateVersion |String |いいえ |ポリシー内のバージョンを示し、APIはそのバージョンの設定詳細を返します。<br><br>このパラメータのデフォルト値は以下の通りです：<br><br><br>* ポリシーが公開されている場合、このパラメータのデフォルト値はポリシー内の公開済み（ステータスが`running`）のバージョンです。<br><br>* ポリシーが公開されていない場合、このパラメータのデフォルト値は`draft`です。<br><br><br>[DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp)を呼び出して、ポリシー内のすべてのバージョンを取得できます。 |`P-250414.89520`<br><br> |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以下のパラメータリストには、暗号化ポリシーの基本設定パラメータのみが含まれています。他の設定モジュールパラメータの説明については、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp">UpdateCipherTemplate</a>を参照してください。</div>



|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|BoundDomains |Object[] |`TemplateId`で指定された暗号化ポリシーに対して、このパラメータはその暗号化ポリシーにバインドされたドメイン名リストを示します。<br><br>ポリシーがドメイン名にバインドされていない場合、このパラメータ値は`null`です。 | |
|BoundTime |Long |暗号化ポリシーが`Domain`で指定されたドメイン名にバインドされた時間を示し、形式はUnixタイムスタンプです。 |`1709174039` |
|Domain |String |暗号化ポリシーにバインドされたドメイン名を示します。 |`www.example.com`<br><br> |
|CreateTime |Long |このドメイン名の作成時間を示し、形式はUnixタイムスタンプです。 |`1709519412`<br><br> |
|HTTPS |Object |HTTPS暗号化サービスの設定を示します。 | |
|DisableHttp |Boolean |リクエストURLのスキームが`HTTP`であるリクエストを許可するかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：スキームが`HTTP`のリクエストを許可することを示します。<br><br>* `false`：スキームが`HTTP`のリクエストを許可しないことを示します。 |`false` |
|ForcedRedirect |Object |「HTTPをHTTPSに強制リダイレクト」機能の設定を示します。<br><br>说明<br><br>CDNは2種類のプロトコルリダイレクト機能を提供しています。<br><br><br>* HTTPからHTTPSへのリダイレクト、つまり`ForcedRedirect`機能。<br><br>* HTTPSからHTTPへのリダイレクト、つまり`HttpForcedRedirect`機能。<br><br><br>これら2つのプロトコルリダイレクト機能は相互に排他的です。つまり、一方の機能が有効になっている場合、もう一方は有効にできません。 | |
|EnableForcedRedirect |Boolean |この機能を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にすることを示します。有効にすると、CDNは受信したHTTPリクエストをHTTPSリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にすることを示します。無効にすると、CDNはHTTPリクエストをHTTPSリクエストにリダイレクトしません。 |`true` |
|StatusCode |String |HTTPSリクエストを受信したときのCDNのリダイレクトレスポンスステータスコードを示します。このパラメータには以下の値があります：<br><br><br>* `301`：返されるステータスコードが301であることを示します。<br><br>* `302`：返されるステータスコードが302であることを示します。 |`301` |
|HTTP2 |Boolean |ユーザーリクエストでHTTP/2サポートを有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：HTTP/2を有効にすることを示します。<br><br>* `false`：HTTP/2を無効にすることを示します。 |`true` |
|Hsts |Object |HSTS機能の設定を示します。 | |
|Subdomain |String |HSTS設定をドメインのサブドメインにも適用するかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `include`：HSTS設定をサブドメインサイトに適用することを示します。<br><br>* `exclude`：HSTS設定をサブドメインサイトに適用しないことを示します。 |`include` |
|Switch |Boolean |この機能を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|Ttl |Long |ブラウザでの`Strict-Transport-Security`レスポンスヘッダーのキャッシュ有効期限を示し、単位は秒です。<br><br>このパラメータ値が`0`の場合、HSTS設定を無効にするのと同じ効果があります。 |`300` |
|OCSP |Boolean |「OCSPステープリング」機能を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|TlsVersion |String[] |「TLSバージョン」機能の設定を示します。このパラメータはユーザーリクエストで使用できるTLSバージョンを指定し、以下の値があります：<br><br><br>* `tlsv1.0`：TLS 1.0を示します。<br><br>* `tlsv1.1`：TLS 1.1を示します。<br><br>* `tlsv1.2`：TLS 1.2を示します。<br><br>* `tlsv1.3`：TLS 1.3を示します。 |`["tlsv1.1","tlsv1.2"]` |
|HttpForcedRedirect |Object |「HTTPSをHTTPに強制リダイレクト」機能の設定を示します。 | |
|EnableForcedRedirect |Boolean |この機能を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にすることを示します。有効にすると、CDNは受信したHTTPSリクエストをHTTPリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にすることを示します。CDNはHTTPSリクエストをHTTPリクエストにリダイレクトしません。 |`true` |
|StatusCode |String |HTTPSリクエストを受信したときに、CDNが返すリダイレクトステータスコードを示します。このパラメータには以下の値があります：**301**、**302**、**303**、**307**、**308**。<br><br>注意すべき点：<br><br><br>* 301および302の場合、元のリクエストで使用されたメソッドがGETでない場合、クライアントが新しいURLにリクエストを送信するとき、新しいリクエストで使用されるメソッドはGETになる可能性があります。<br><br>* 303の場合、新しいリクエストで使用されるメソッドはGETです。<br><br>* 307および308の場合、新しいリクエストで使用されるメソッドは元のリクエストと同じで、変更されません。 |`302` |
|Message |String |暗号化ポリシーの説明を示します。 |`This is a test` |
|Quic |Object |QUIC設定を示します。 | |
|Switch |Boolean |ユーザーリクエストでQUICを有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：QUICを有効にすることを示します。<br><br>* `false`：QUICを無効にすることを示します。 |`true` |
|Status |String |このドメインのステータスを示します。このパラメータには以下の値があります：<br><br><br>* `online`：ステータスが正常に実行中であることを示します。<br><br>* `configuring`：ステータスが設定中であることを示します。<br><br>* `offline`：ステータスがオフラインであることを示します。 |`editing` |
|TemplateId |String |暗号化ポリシーのIDを示します。 |`tpl-c2PRDW` |
|Title |String |暗号化ポリシーの名前を示します。 |`standard` |
|Type |String |暗号化ポリシーのタイプを示します。このパラメータ値は常に`cipher`です。 |`cipher` |
|UpdateTime |Long |このドメイン設定の最新更新時間を示し、形式はUnixタイムスタンプです。このドメイン設定が作成後に更新されていない場合、このパラメータ値は`CreateTime`の値と同じです。 |`1709519412` |
|Exception |Boolean |暗号化ポリシーが特殊設定を含むかどうかを示します。特殊設定とは、ユーザーではなくBytePlusエンジニアによって操作される設定を指します。このパラメータには以下の値があります：<br><br><br>* `true`：特殊設定を含むことを示します。<br><br>* `false`：特殊設定を含まないことを示します。 |`false` |
|Project |String |このドメインが属するプロジェクトを示します。 |`default` |
|ProdVersion |String |ポリシー内で公開済み（ステータスが`running`）のバージョンを示します。ステータスが`running`のバージョンが存在しない場合、このパラメータ値は空（""）です。 |`P-250414.89520`<br><br> |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c2PRDW"
}
```


<span id="レスポンス例"></span>
### レスポンス例

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">以下は、「レスポンスパラメータ」リストに記載されているパラメータの例です。他のモジュールのパラメータの例については、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp">UpdateCipherTemplate</a> のリクエスト例を参照してください。</div>


```json
{
    "ResponseMetadata": {
        "RequestId": "20240304034932E622246DA960291AEC51",
        "Action": "DescribeCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "BoundDomains": [
            {
                "BoundTime": 1709174039,
                "Domain": "www.example.com"
            }
        ],
        "CreateTime": 1709519412,
        "Exception": false,
        "Message": "Trying Fix Cipher",
        "Project": "default",
        "Status": "editing",
        "TemplateId": "tpl-c2PRDW",
        "Title": "Standard",
        "Type": "cipher",
        "UpdateTime": 1709519412,
        "ProdVersion": "P-250414.89520"
    }
}
```


&nbsp;
