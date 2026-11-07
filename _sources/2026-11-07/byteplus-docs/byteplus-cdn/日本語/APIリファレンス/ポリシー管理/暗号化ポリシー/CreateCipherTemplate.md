---
title: "CreateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateCipherTemplate_jp"
---

暗号化ポリシーを作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=CreateCipherTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このAPIを呼び出す際、Bodyリスト内のパラメータに加えて、他の設定モジュール内のパラメータを指定することもできます。他のモジュール内のパラメータの説明については、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp">UpdateCipherTemplate</a>を参照してください。</div>


<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はCreateCipherTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Title |String |はい |作成する暗号化ポリシーの名前を示します、長さは100文字を超えてはいけません。 |`TestPolicy` |
|HTTPS |Object |いいえ |HTTPS暗号化サービスの設定を示します。 | |
|DisableHttp |Boolean |いいえ |リクエスト URL のスキームが `HTTP` のリクエストを許可するかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：スキームが `HTTP` のリクエストを許可することを示します。<br><br>* `false`：スキームが `HTTP` のリクエストを許可しないことを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`false` |
|ForcedRedirect |Object |いいえ |「HTTP から HTTPS への強制リダイレクト」機能の設定モジュールを示します。この機能はデフォルトで無効になっています。<br><br>说明<br><br>CDN は 2 種類のプロトコルリダイレクト機能を提供します。<br><br><br>* HTTP から HTTPS へのリダイレクト、つまり `ForcedRedirect` モジュール。<br><br>* HTTPS から HTTP へのリダイレクト、つまり `HttpForcedRedirect` モジュール。<br><br><br>これらの 2 つのプロトコルリダイレクト機能は相互に排他的です。つまり、一方を有効にすると、もう一方は有効にできません。 | |
|EnableForcedRedirect |Boolean |はい |この機能を有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。有効にすると、CDN は受信した HTTP リクエストを HTTPS リクエストにリダイレクトします。<br><br>* `false`：この機能を無効にすることを示します。無効にすると、CDN は HTTP リクエストを HTTPS リクエストにリダイレクトしません。<br><br><br>この機能を有効にするには、アクセラレーションドメインで HTTPS を有効にする必要があります。 |`true` |
|StatusCode |String |はい |HTTPS リクエストを受信したときの CDN のリダイレクト応答ステータスコードを示します。このパラメータには次の値があります。<br><br><br>* `301`：返されるステータスコードが 301 であることを示します。<br><br>* `302`：返されるステータスコードが 302 であることを示します。<br><br><br>このパラメータのデフォルト値は `301` です。 |`301` |
|HTTP2 |Boolean |いいえ |HTTP/2 機能を有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>この機能を有効にするには、アクセラレーションドメインで HTTPS 暗号化サービスを有効にしている必要があります。<br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|Hsts |Object |いいえ |HSTS 機能の設定モジュールを示します。この機能はデフォルトで無効になっています。 | |
|Subdomain |String |いいえ |HSTS 設定がドメインのサブドメインにも適用されるかどうかを示します。このパラメータには次の値があります。<br><br><br>* `include`：HSTS 設定がサブドメインサイトに適用されることを示します。<br><br>* `exclude`：HSTS 設定がサブドメインサイトに適用されないことを示します。<br><br><br>このパラメータのデフォルト値は `exclude` です。 |`include` |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|Ttl |Long |いいえ |ブラウザがリクエストされたファイルをキャッシュする時間（秒単位）を示します。CDNは、この値をヘッダー値として、レスポンスに「Cache\-Control: max\-age」ヘッダーを含めます。 |`300` |
|OCSP |Boolean |いいえ |「OCSP ステープリング」機能を有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>この機能を有効にするには、アクセラレーションドメインで HTTPS を有効にする必要があります。このパラメータのデフォルト値は `false` です。 |`true` |
|TlsVersion |String[] |いいえ |「TLS バージョン」機能の設定モジュールを示します。このパラメータは、ユーザーリクエストが使用できる TLS バージョンを指定します。次の値があります。<br><br><br>* `tlsv1.0`：TLS 1.0 を示します。<br><br>* `tlsv1.1`：TLS 1.1 を示します。<br><br>* `tlsv1.2`：TLS 1.2 を示します。<br><br>* `tlsv1.3`：TLS 1.3 を示します。<br><br><br>このパラメータのデフォルト値は `["tlsv1.1", "tlsv1.2", "tlsv1.3"]` です。 |`["tlsv1.1","tlsv1.2"]` |
|HttpForcedRedirect |Object |いいえ |「HTTPSからHTTPへのリダイレクト」機能の設定。 | |
|EnableForcedRedirect |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。有効にすると、CDNは受信したHTTPSリクエストをHTTPリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にすることを示します。CDNはHTTPSリクエストをHTTPリクエストにリダイレクトしません。<br><br><br>この機能を有効にするには、アクセラレーションドメインでHTTPSが有効になっている必要があります。 |`true` |
|StatusCode |String |はい |HTTPS リクエストを受信したときに CDN から返されるリダイレクト ステータス コードを示します。このパラメータには、**301**、**302**、**303**、**307**、**308** のいずれかの値を指定できます。<br><br>デフォルト値は `301` です。<br><br>注:<br><br><br>* 301 および 302 の場合、元のリクエスト メソッドが GET でなかった場合、クライアントが新しい URL にリクエストを送信する際に使用するメソッドは GET になることがあります。<br><br>* 303 の場合、新しいリクエストで使用されるメソッドは GET です。<br><br>* 307 および 308 の場合、新しいリクエストで使用されるメソッドは元のリクエストと同じであり、変更されません。 |`302` |
|Message |String |いいえ |この暗号化ポリシーの説明を示します、長さは120文字を超えてはいけません。 |`This is a test.` |
|Quic |Object |いいえ |QUIC機能の設定。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>この機能を有効にするには、アクセラレーションドメインでHTTPSが有効になっている必要があります。 |`true` |
|Project |String |いいえ |この暗号化ポリシーが所属するプロジェクトを示します。このパラメータのデフォルト値は `default` で、Defaultプロジェクトを示します。 |`default` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TemplateId |String |作成された暗号化ポリシーのIDを示します。 |`tpl-cqwYjZ` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=CreateCipherTemplate&Version=2021-03-01
{
    "Title": "My Policy",
    "Message": "This is a test.",
    "Project": "default",
    "HTTPS": {
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "303"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 50
        },
        "OCSP": true,
        "TlsVersion": [
            "tlsv1.1",
            "tlsv1.2"
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "301"
    },
    "Quic": {
        "Switch": true
    }
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403060948229866691E7BB9DDCF6DAF",
        "Action": "CreateCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-cqwYjZ"
    }
}
```


&nbsp;
