---
title: "UpdateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCipherTemplate_jp"
---

BytePlus CDNにおいて暗号化ポリシーの設定を更新します。

BytePlus CDNでは、ドメイン名の設定を更新する必要がある場合、以下のいずれかの方法を使用できます：


* 方法1：ドメイン名の設定を直接更新する。

* 方法2：ドメイン名にバインドされているポリシー設定を更新する。


この記事では、APIを使用して方法2における暗号化ポリシーの更新を実現する方法について説明します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">これら2つの方法の違いについては、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp">ドメイン設定</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">APIを使用して方法2における配信ポリシーの更新を実現する方法については、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateServiceTemplate_jp">UpdateServiceTemplate</a>を参照してください。</div>


* <div data-tips="true" data-tips-type="tip">APIを使用して方法1を実現する方法については、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCdnConfig_jp">UpdateCdnConfig</a>を参照してください。</div>



`Title`および`Message`以外のパラメータを更新する場合、`UpdateCipherTemplate`を呼び出す際に`TemplateVersion`を`draft`として指定する必要があります。つまり、更新対象のポリシーにDraftバージョンが既に存在している必要があります。更新対象のポリシーにDraftバージョンが存在することを確認するには、以下の手順に従います：


1. 対象ポリシーに対して`DescribeTemplateReleaseVersions` APIを呼び出します。

2. APIから返されるバージョンリストで、Draftバージョン（`"Version": "draft"`）が存在するか確認します。

* Draftバージョンが存在する場合、対象ポリシーに対して`UpdateCipherTemplate`を呼び出すことができます。

* 存在しない場合は、先に対象ポリシーに対して`CreateTemplateVersion`を呼び出してDraftバージョンを作成し、その後`UpdateCipherTemplate`を呼び出す必要があります。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">このAPIはドメインレベルで設定モジュールを上書きモードで更新します。詳細は以下の通りです：</div>



* <div data-tips="true" data-tips-type="warning">APIリクエストを作成する際、特定のモジュールを指定しない場合、APIリクエストを送信した後も、そのモジュールの既存設定は変更されません。</div>


* <div data-tips="true" data-tips-type="warning">特定のモジュールを指定したが、そのモジュール内の特定のオプションパラメータを指定しない場合、そのパラメータはデフォルト値を使用します。APIリクエストを送信した後、そのパラメータの既存値はデフォルト値で上書きされます。</div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUpdateCipherTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |更新対象の暗号化ポリシーのIDを示します。<br><br>[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)を使用して、更新したい暗号化ポリシーのIDを取得できます。 | |
|HTTPS |Object |いいえ |HTTPS暗号化サービスの設定モジュールを示します。 | |
|DisableHttp |Boolean |いいえ |CDNがユーザーのHTTPリクエストを受け入れるかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：受け入れません。HTTPリクエストを受信した場合、CDNはそのリクエストを拒否します。<br><br>* `false`：受け入れます。<br><br><br>このパラメータのデフォルト値は`false`です。 | |
|ForcedRedirect |Object |いいえ |"HTTPをHTTPSに強制リダイレクト"機能の設定を示します。<br><br>说明<br><br>`ForcedRedirect`と`HttpForcedRedirect`は相互に排他的です。一方を設定した場合、もう一方を設定することはできません。 | |
|EnableForcedRedirect |Boolean |はい |この機能を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にします。有効にすると、CDNは受信したHTTPリクエストをHTTPSリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にします。CDNはHTTPリクエストをHTTPSリクエストにリダイレクトしません。 | |
|StatusCode |String |はい |HTTPリクエストを受信した際のCDNのリダイレクト応答ステータスコードを示します。このパラメータには以下の値があります：**301**、**302**、**303**、**307**、**308**。<br><br>このパラメータのデフォルト値は`301`です。<br><br>注意点：<br><br><br>* 301および302の場合、元のリクエストがGET以外のメソッドを使用している場合、クライアントが新しいURLにリクエストを送信する際、新しいリクエストのメソッドがGETに変更される可能性があります。<br><br>* 303の場合、新しいリクエストのメソッドはGETです。<br><br>* 307および308の場合、新しいリクエストのメソッドは元のリクエストと同じで、変更されません。 | |
|HTTP2 |Boolean |いいえ |ユーザーリクエストに対してHTTP/2サポートを有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：HTTP/2を有効にします。<br><br>* `false`：HTTP/2を無効にします。<br><br><br>この機能を有効にするには、ドメインでHTTPS暗号化サービスが既に有効になっている必要があります。<br><br>このパラメータのデフォルト値は`false`です。 | |
|Hsts |Object |いいえ |HSTS機能の設定を示します。 | |
|Subdomain |String |いいえ |HSTS設定をドメインのサブドメインにも適用するかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `include`：HSTS設定をサブドメインに適用します。<br><br>* `exclude`：HSTS設定をサブドメインに適用しません。<br><br><br>このパラメータのデフォルト値は`exclude`です。 | |
|Switch |Boolean |いいえ |HSTSを有効にするかどうかを指定します。このパラメータには以下の値があります：<br><br><br>* `true`：HSTSを有効にします。<br><br>* `false`：HSTSを無効にします。<br><br><br>このパラメータのデフォルト値は`false`です。 | |
|Ttl |Long |いいえ |`Strict-Transport-Security`レスポンスヘッダーがブラウザでキャッシュされる期限を秒単位で示します。<br><br>`Switch`が`true`の場合、このパラメータは必須です。このパラメータの値の範囲は0～31,536,000です。31,536,000秒は365日を示します。<br><br>このパラメータの値が`0`の場合、HSTS設定を無効にするのと同じ効果があります。 | |
|OCSP |Boolean |いいえ |OCSPステープリングを有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：OCSPステープリングを有効にします。<br><br>* `false`：OCSPステープリングを無効にします。<br><br><br>このパラメータのデフォルト値は`false`です。 | |
|TlsVersion |String[] |いいえ |ドメインがサポートするTLSバージョンを指定するリストを示します。このパラメータには以下の値があります：<br><br><br>* `tlsv1.0`：TLS 1.0を示します。<br><br>* `tlsv1.1`：TLS 1.1を示します。<br><br>* `tlsv1.2`：TLS 1.2を示します。<br><br>* `tlsv1.3`：TLS 1.3を示します。<br><br><br>このパラメータのデフォルト値は`["tlsv1.1", "tlsv1.2", "tlsv1.3"]`です。 | |
|HttpForcedRedirect |Object |いいえ |"HTTPSをHTTPに強制リダイレクト"機能の設定を示します。<br><br>说明<br><br>`HttpForcedRedirect`と`ForcedRedirect`は相互に排他的です。一方を設定した場合、もう一方を設定することはできません。 | |
|EnableForcedRedirect |Boolean |はい |この機能を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にします。有効にすると、CDNは受信したHTTPSリクエストをHTTPリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にします。CDNはHTTPSリクエストをHTTPリクエストにリダイレクトしません。 | |
|StatusCode |String |はい |HTTPSリクエストを受信した際のCDNのリダイレクト応答ステータスコードを示します。このパラメータには以下の値があります：**301**、**302**、**303**、**307**、**308**。<br><br>このパラメータのデフォルト値は`301`です。<br><br>注意点：<br><br><br>* 301および302の場合、元のリクエストがGET以外のメソッドを使用している場合、クライアントが新しいURLにリクエストを送信する際、新しいリクエストのメソッドがGETに変更される可能性があります。<br><br>* 303の場合、新しいリクエストのメソッドはGETです。<br><br>* 307および308の場合、新しいリクエストのメソッドは元のリクエストと同じで、変更されません。 | |
|Message |String |いいえ |新しいポリシーの説明で、長さは120文字以内にする必要があります。 | |
|Quic |Object |いいえ |QUIC設定を示します。 | |
|Switch |Boolean |はい |ユーザーリクエストに対してQUICサポートを有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `true`：QUICを有効にします。<br><br>* `false`：QUICを無効にします。 | |
|Title |String |いいえ |新しいポリシー名で、長さは100文字以内にする必要があります。 | |
|TemplateVersion |String |いいえ |更新対象のポリシーバージョンを示します。<br><br><br>* 更新対象のパラメータが`Title`または`Message`の場合、このパラメータを指定する必要はありません。これら2つのパラメータはポリシーバージョンとは関係ありません。<br><br>* 更新対象のパラメータが`Title`および`Message`ではない場合、このパラメータを`draft`として指定する必要があります。ドキュメント冒頭の説明を参照してください。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c2vy7q",
    "TemplateVersion": "draft",
    "HTTPS": {
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "302"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 1800
        },
        "OCSP": true,
        "TlsVersion": [
            "tlsv1.2",
            "tlsv1.3"
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "302"
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
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
