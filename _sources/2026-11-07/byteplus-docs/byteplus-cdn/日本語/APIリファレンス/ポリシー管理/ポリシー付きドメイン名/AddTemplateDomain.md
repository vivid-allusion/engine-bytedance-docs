---
title: "AddTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/AddTemplateDomain_jp"
---

BytePlus CDNに1つ以上のドメイン名を追加します。ドメインを追加する際は、公開済みの配信ポリシーを指定する必要があります。また、オプションで、公開済みの暗号化ポリシーとルールエンジンポリシーも指定できます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はAddTemplateDomainです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |はい |追加するドメイン名を示します。追加するドメイン名は以下のすべての条件を満たす必要があります：<br><br><br>* 長さは100文字以内。<br><br>* 大文字を含まない。<br><br>* 以下のサフィックスを含まない：`zjgslb.com`、`yangyi19.com`、`volcgslb.com`、`veew-alb-cn1.com`、`bplgslb.com`、`bplslb.com`、`ttgslb.com`。<br><br><br>说明<br><br>注意点：ドメイン名を配信ポリシーにバインドする場合、ポリシーで指定されたオリジンサーバーアドレスはドメイン名と同じにできません。 | |
|ServiceTemplateId |String |はい |ドメイン名にバインドする必要がある配信ポリシーを示します。<br><br>[DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/DescribeTemplates_jp)を使用して、バインドしたい配信ポリシーのIDを取得できます。 | |
|CertId |String |いいえ |証明書のIDを示します。この証明書はBytePlus証明書センターに保存され、ドメイン名に関連付けられます。<br><br><br>* `HTTPSSwitch`が`on`の場合、このパラメータは必須です。このAPIを使用する前に、CDNが証明書センターにアクセスする権限を付与する必要があり、その後証明書をBytePlus証明書センターにアップロードして証明書のIDを取得する必要があります。CDNが証明書センターにアクセスする権限を付与することを推奨します。<br><br><br>[ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/ListCertInfo_jp)を使用して、関連付けたい証明書のIDを取得できます。<br><br><br>* `HTTPSSwitch`が`off`の場合、このパラメータは無効です。 | |
|CipherTemplateId |String |いいえ |ドメイン名にバインドする必要がある暗号化ポリシーを示します。<br><br>[DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/DescribeTemplates_jp)を使用して、バインドしたい暗号化ポリシーのIDを取得できます。<br><br>このパラメータを指定しない場合、現在ドメイン名を暗号化ポリシーにバインドしません。 | |
|HTTPSSwitch |String |いいえ |ドメイン名で"HTTPS暗号化サービス"を有効にするかどうかを示します。このパラメータには以下の値があります：<br><br><br>* `on`：サービスを有効にすることを示します。<br><br>* `off`：サービスを有効にしないことを示します。<br><br><br>このパラメータのデフォルト値は`off`です。 | |
|Project |String |いいえ |ドメイン名が属するプロジェクトを示し、デフォルト値は`default`です。 | |
|ServiceRegion |String |いいえ |ドメイン名で有効にするサービス地域を示します。このパラメータには以下の値があります：<br><br><br>* `outside_chinese_mainland`："グローバル（中国本土を除く）"を示します。<br><br>* `chinese_mainland`："中国本土"を示します。<br><br>* `global`："グローバル"を示します。<br><br><br>このパラメータのデフォルト値は`outside_chinese_mainland`です。<br><br>注意点：デフォルトでは`chinese_mainland`と`global`は使用できません。これらのサービス地域を使用可能にするには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。同時に、これらの地域は中国本土を含むため、以下の追加作業を完了する必要があります：<br><br><br>* BytePlusアカウントで[実名認証](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration)を行う<br><br>* ドメイン名のICP届出を行う。 | |
|Tags |Object[] |いいえ |タグリストを示します。これらのタグは`Domain`に追加されます。リストには最大10個のタグを含めることができます。タグはキーバリューペアです。 | |
|Key |String |いいえ |リスト内のタグのkeyを示し、長さは1\-128文字の範囲です。Keyは大文字と小文字を区別し、Unicode文字、Unicode数字、スペース、および以下の任意の文字を含むことができます：<br><br><br>* _./=+\-@ | |
|Value |String |いいえ |タグの値を示し、長さは1\-256文字の範囲です。このパラメータも大文字と小文字を区別し、Unicode文字、Unicode数字、スペース、および以下の任意の文字を含むことができます：<br><br><br>* _./=+\-@ | |
|RuleTemplateIds |String[] |いいえ |ルールポリシーテンプレートIDリスト | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|ResourceIds |String[] |追加されたドメイン名のリスト。 |`["www.example.com","img.example.com"]` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=AddTemplateDomain&Version=2021-03-01
{
    "Domain": "www.example.com,img.example.com",
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2349b4b42c2e80b0aa8c23",
    "Tags": [
        {
            "Key": "myKey1",
            "Value": "myValue1"
        },
        {
            "Key": "myKey2",
            "Value": "myValue2"
        }
    ]
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025082209311384D275C0D56FB6A17884",
        "Action": "AddTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ResourceIds": [
            "www.example.com",
            "img.example.com"
        ]
    }
}
```


&nbsp;
