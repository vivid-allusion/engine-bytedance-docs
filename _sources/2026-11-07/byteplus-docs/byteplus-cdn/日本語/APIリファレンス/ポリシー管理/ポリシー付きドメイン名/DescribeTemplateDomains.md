---
title: "DescribeTemplateDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp"
---

フィルタリング条件に一致するドメイン名のリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeTemplateDomainsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Filters |Object[] |いいえ |フィルタリング条件のセットを表し、条件に一致するドメイン名のリストを取得します。フィルタリング条件を指定しない場合、このAPIはアカウント配下のすべてのドメイン名を返します。<br><br>複数のフィルタリング条件間はAND関係であり、すべてのフィルタリング条件を満たした場合のみ、ドメイン名がこのAPIの返すリストに含まれます。<br><br>このAPIのレスポンスでは、実際に返されるドメイン名リストは`PageNum`と`PageSize`の影響を受けます。 | |
|Fuzzy |Boolean |いいえ |マッチング方法を表します。このパラメータには以下の値があります：<br><br><br>* `true`：あいまいマッチングを表します。ドメイン名のマッチングプロセスにおいて、`Name`の対応する値が`Value`配列内の任意の値を含む場合、そのドメイン名はフィルタリング条件に一致したと見なされます。<br><br>* `false`：完全一致を表します。`Name`の対応する値が`Value`配列内の値と同じ場合、そのドメイン名はフィルタリング条件に一致したと見なされます。<br><br><br>同時に、指定可能な`Fuzzy`の値は`Name`の値の影響を受けます。`Name`の説明を参照してください。<br><br>このパラメータのデフォルト値は`false`です。 |`false` |
|Name |String |いいえ |フィルタリングタイプを表します。このパラメータには以下の値があります：<br><br><br>* `TemplateTitle`：バインドされているポリシーの名前でドメイン名をフィルタリングします。<br><br>* `TemplateId`：バインドされているポリシーのIDでドメイン名をフィルタリングします。このパラメータ値の場合、`Fuzzy`の値は`false`のみ可能です。<br><br>* `TemplateType`：バインドされているポリシーのタイプでドメイン名をフィルタリングします。このパラメータ値の場合、`Fuzzy`の値は`false`のみ可能です。<br><br>* `Domain`：名前でドメイン名をフィルタリングします。<br><br>* `Status`：ステータスでドメイン名をフィルタリングします。このパラメータ値の場合、`Fuzzy`の値は`false`のみ可能です。<br><br>* `HTTPSSwitch`："HTTPS暗号化サービス"のステータスでドメイン名をフィルタリングします。このパラメータ値の場合、`Fuzzy`の値は`false`のみ可能です。<br><br>* `WAFStatus`："WAF保護"のステータスでドメイン名をフィルタリングします。このパラメータ値の場合、`Fuzzy`の値は`false`のみ可能です。<br><br><br>複数のフィルタリング条件を同時に指定できますが、異なるフィルタリング条件の`Name`は同じにできません。 |`TemplateTitle` |
|Value |String[] |いいえ |`Name`に対応する値を表し、配列です。配列内の値はオブジェクト値とのマッチングに使用されます。オブジェクト値が配列内の任意の値とマッチした場合、マッチングと見なされます。パラメータ値はマッチング時に大文字小文字を区別します。<br><br><br>* `Name`が`TemplateTitle`または`Domain`の場合、`Value`内の各値の長さは100文字以内である必要があります。また、<br><br>   * `Fuzzy`が`false`の場合、`Value`には複数の値を含めることができます。<br><br>   * `Fuzzy`が`true`の場合、`Value`には1つの値のみ含めることができます。<br><br>* `Name`が`TemplateId`の場合、`Value`には1つの値のみ含めることができます。<br><br>* `Name`が`TemplateType`の場合、`Value`には以下の1つまたは複数の値を含めることができます：<br><br>   * `cipher`：暗号化ポリシーを表します。<br><br>   * `service`：配信ポリシーを表します。<br><br>* `Name`が`Status`の場合、`Value`には以下のいずれかの値を含めることができます：<br><br>   * `online`：ドメイン名のステータスが"オンライン"であることを表します。<br><br>   * `offline`：ドメイン名のステータスが"オフライン"であることを表します。<br><br>   * `configuring`：ドメイン名のステータスが"設定中"であることを表します。<br><br>* `Name`が`HTTPSSwitch`の場合、`Value`には以下のいずれかの値を含めることができます：<br><br>   * `on`："HTTPS暗号化サービス"のステータスが有効であることを表します。<br><br>   * `off`："HTTPS暗号化サービス"のステータスが無効であることを表します。<br><br>* `Name`が`WAFStatus`の場合、`Value`には以下のいずれかの値を含めることができます：<br><br>   * `on`："WAF保護"のステータスが有効であることを表します。<br><br>   * `off`："WAF保護"のステータスが無効であることを表します。 |`["TestPolicy"]` |
|PageNum |Long |いいえ |返される結果セットに対して、このパラメータはページ番号を表し、このAPIが実際に返すドメイン名はこのページ番号で指定されたページ上のものです。<br><br>このAPIが返すドメイン名は`PageSize`によってページ分割されます。このAPIが返すドメイン名の数が100で、指定した`PageSize`が`10`の場合、返されるドメイン名は10ページに分散されます。指定した`PageNum`が`2`の場合、2ページ目のドメイン名を取得することを表します。<br><br>指定したページにドメイン名がない場合、返される結果の`Domains`パラメータの値は`null`です。<br><br>`PageNum`のデフォルト値は1です。 |`1` |
|PageSize |Long |いいえ |各ページに含まれるドメイン名の数を表します。<br><br>このパラメータの値の範囲は1\-200で、デフォルト値は`10`です。 |`10` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Domains |Object[] |このAPIが返すドメイン名リストを表します。<br><br>注意すべき点は、リスト内のドメイン名はリクエストパラメータ`PageNum`で示されるページ上のものであり、必ずしもフィルタリング条件に一致するすべてのドメイン名ではないことです。 | |
|CertInfo |Object |`Domain`で指定されたドメイン名に関連付けられた証明書の情報を表します。<br><br>`HTTPSSwitch`が`off`の場合、このパラメータの値は`null`です。 | |
|CertId |String |ドメイン名に関連付けられた証明書のIDを表します。この証明書はBytePlus証明書センターで管理されています。 | |
|Cname |String |CDNがこのドメイン名に割り当てたCNAMEを表します。 |`www.example.com.bplslb.com` |
|Domain |String |`Domains`リスト内の1つのドメイン名を表します。 |`www.example.com` |
|HTTPSSwitch |String |このドメイン名が"HTTPS暗号化サービス"を有効にしているかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `on`：このサービスが有効であることを表します。<br><br>* `off`：このサービスが無効であることを表します。 |`off` |
|LockStatus |String |このドメイン名がロックされているかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `on`：このドメイン名がロックされていることを表します。この場合、[UpdateTemplateDomain](https://docs.byteplus.com/byteplus-cdn/reference/UpdateTemplateDomain_jp)を使用してこのドメイン名の設定を変更することはできません。<br><br>* `off`：このドメイン名がロックされていないことを表します。 |`off` |
|Remark |String |このドメイン名がロックされた理由を表します。<br><br><br>* `LockStatus`が`on`の場合、このパラメータはロックの理由を表します。<br><br>* `LockStatus`が`off`の場合、このパラメータの値は空（""）です。 |`This is a test` |
|ServiceRegion |String |このドメイン名が有効にしている加速エリアを表します。このパラメータには以下の値があります<br><br><br>* `outside_chinese_mainland`："中国本土を除くグローバル"を表します。<br><br>* `chinese_mainland`："中国本土"を表します。<br><br>* `global`："グローバル"を表します。 |`outside_chinese_mainland` |
|Status |String |このドメイン名のステータスを表します。このパラメータには以下の値があります：<br><br><br>* `online`：ステータスが"オンライン"であることを表します。<br><br>* `offline`：ステータスが"オフライン"であることを表します。<br><br>* `configuring`：ステータスが"設定中"であることを表します。 |`online` |
|Templates |Object[] |このドメイン名にバインドされているポリシーリストを表します。<br><br>ドメイン名は1つの配信ポリシーに必ずバインドする必要があり、オプションで1つの暗号化ポリシーにバインドできます。 | |
|TemplateId |String |ポリシーのIDを表します。 |`tpl-s2DVaW` |
|Title |String |このポリシーの名前を表します。 |`NetTVPlayer002` |
|Type |String |このポリシーのタイプを表します。このパラメータには以下の値があります：<br><br><br>* `cipher`：暗号化ポリシーを表します。<br><br>* `service`：配信ポリシーを表します。 |`service` |
|Exception |Boolean |このポリシーが特殊な設定を含むかどうかを表します。特殊な設定とは、ユーザーではなくBytePlusエンジニアが操作する設定を指します。このパラメータには以下の値があります：<br><br><br>* `true`：特殊な設定を含むことを表します。<br><br>* `false`：特殊な設定を含まないことを表します。 |`false` |
|ProdVersion |String |このポリシーに基づいてリリースされたバージョン、つまり「実行中」状態のバージョンを示します。「実行中」状態のバージョンがない場合、このパラメータ値は空（""）になります。 |`P-250414.89520` |
|WAFStatus |String |このドメイン名が"WAF保護"を有効にしているかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `on`："WAF保護"が有効であることを表します。<br><br>* `off`："WAF保護"が無効であることを表します。 |`off` |
|Project |String |このドメイン名が属するプロジェクトを表します。 |`default` |
|Tags |Object[] |`Domain`に追加されたタグリストを表します。タグはキーバリューペアです。`Domain`にタグがない場合、このパラメータの値は`null`です。 | |
|Key |String |リスト内の1つのタグのkeyを表します。 |`myKey` |
|Value |String |このタグの値を表します。 |`myValue` |
|TotalCount |Long |フィルタリング条件に一致するドメイン名の数を表します。このパラメータの値は`PageSize`と`PageNum`の影響を受けません。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomains&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Domain",
            "Value": [
                "example"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateTitle",
            "Value": [
                "NetTVPlayer"
            ],
            "Fuzzy": true
        },
        {
            "Name": "TemplateId",
            "Value": [
                "tpl-s2DVaW"
            ],
            "Fuzzy": false
        },
        {
            "Name": "TemplateType",
            "Value": [
                "service",
                "cipher"
            ],
            "Fuzzy": false
        },
        {
            "Name": "HTTPSSwitch",
            "Value": [
                "off"
            ],
            "Fuzzy": false
        },
        {
            "Name": "WAFStatus",
            "Value": [
                "off"
            ]
        },
        {
            "Name": "Status",
            "Value": [
                "online"
            ],
            "Fuzzy": false
        }
    ]
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240305044725DD2386782EADAD775440",
        "Action": "DescribeTemplateDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "CertInfo": null,
                "Cname": "www.example.com.bplslb.com",
                "Domain": "www.example.com",
                "HTTPSSwitch": "off",
                "LockStatus": "off",
                "Project": "default",
                "Remark": "",
                "ServiceRegion": "outside_chinese_mainland",
                "Status": "online",
                "Templates": [
                    {
                        "Exception": false,
                        "TemplateId": "tpl-s2DVaW",
                        "Title": "NetTVPlayer002",
                        "Type": "service"
                    }
                ],
                "WAFStatus": "off",
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
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
