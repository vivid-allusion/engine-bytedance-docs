---
title: "UpdateTemplateDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateTemplateDomain_jp"
---

ドメイン名リストを指定し、リスト内のドメイン名設定を変更します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip"><code>HTTPSwitch</code>が<code>on</code>のドメイン名については、一度に1つだけ変更できます。つまり、指定するドメイン名リストには1つのドメイン名のみを含めることができます。</div>


* <div data-tips="true" data-tips-type="tip">複数のドメイン名の設定を同時に変更する場合は、以下のすべての条件を満たす必要があります：</div>


   * <div data-tips="true" data-tips-type="tip">これらのドメイン名の現在の設定において、<code>HTTPSSwitch</code>はすべて<code>off</code>です。</div>


   * <div data-tips="true" data-tips-type="tip">変更時に<code>HTTPSSwitch</code>を指定しないか、変更後の設定において<code>HTTPSSwitch</code>は<code>off</code>でなければなりません。</div>


* <div data-tips="true" data-tips-type="tip">このAPIを使用する際、特定のパラメータを指定しない場合、APIリクエストを送信した後も、そのパラメータの既存設定は変更されません。</div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Bodyリスト内のパラメータについて、特定のパラメータを指定しない場合、指定されたドメイン名の対応する設定を変更しないことを表します。</div>


<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUpdateTemplateDomainです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domains |String[] |はい |ドメイン名リストを表し、それらの設定を変更します。<br><br>以下のいずれかの条件を満たす場合、リストには1つのドメイン名のみを指定できます。<br><br><br>* 変更対象のドメイン名の中に、`HTTPSSwitch`設定が`on`のドメイン名が存在する。<br><br>* このAPIを呼び出す際、`HTTPSSwitch`パラメータを指定しないか、`HTTPSSwitch`を`on`に指定する。 |`["www.example.com","abc.test.com"]` |
|CertId |String |いいえ |`Domains`内のドメイン名に関連付ける証明書の情報を表します。<br><br><br>* `HTTPSSwitch`が`on`の場合、このパラメータは必須であり、`Domains`内のドメイン名に関連付ける証明書のIDを表します。この証明書はBytePlus証明書センターに保存されています。<br><br>&nbsp;<br><br>   [ListCertInfo](https://docs.byteplus.com/byteplus-cdn/reference/ListCertInfo_jp)を使用して、関連付けたい証明書のIDを取得できます。<br><br>* `HTTPSSwitch`が`off`の場合、このパラメータは無効です。 |`cert-044833503b2349b4b42c2e80b0aa8c23` |
|CipherTemplateId |String |いいえ |暗号化ポリシーを表します。この暗号化ポリシーは`Domains`内のドメイン名にバインドされます。このAPIを呼び出す際、`Domains`内のドメイン名が既に暗号化ポリシーにバインドされている場合、これらのドメイン名は既にバインドされている暗号化ポリシーから一旦解除され、それから`CipherTemplateId`で指定された暗号化ポリシーにバインドされます。<br><br>[DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/DescribeTemplates_jp)を使用して、バインドしたい暗号化ポリシーのIDを取得できます。 |`tpl-cqgRvW` |
|HTTPSSwitch |String |いいえ |`Domains`内のドメイン名に対して"HTTPS暗号化サービス"を有効にするかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `on`：このサービスが有効であることを表します。<br><br>* `off`：このサービスが無効であることを表します。<br><br><br>`Domains`に複数のドメイン名が含まれる場合、`HTTPSSwitch`は`off`でなければなりません。 |`on` |
|ServiceRegion |String |いいえ |`Domains`内のドメイン名に対して有効にするサービスエリアを表します。このパラメータには以下の値があります：<br><br><br>* `outside_chinese_mainland`："中国本土を除くグローバル"を表します。<br><br>* `chinese_mainland`："中国本土"を表します。<br><br>* `global`："グローバル"を表します。<br><br><br>注意すべき点は、`chinese_mainland`と`global`はデフォルトでは使用できません。これら2つのサービスエリアを使用するには、[チケットを提出](https://console.byteplus.com/workorder/create)してください。同時に、これらのエリアは中国本土を含むため、以下の追加操作を完了する必要があります：<br><br><br>* BytePlusアカウントで[実名認証](https://docs.byteplus.com/en/byteplus-platform/docs/real-name-registration)を完了する。<br><br>* ドメイン名のICP届出を完了する。 |`outside_chinese_mainland` |
|ServiceTemplateId |String |いいえ |配信ポリシーを表します。この配信ポリシーは`Domains`内のドメイン名にバインドされます。このAPIを呼び出す際、`Domains`内のドメイン名が既に配信ポリシーにバインドされている場合、これらのドメイン名は既にバインドされている配信ポリシーから一旦解除され、それから`ServiceTemplateId`で指定された配信ポリシーにバインドされます。<br><br>[DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/DescribeTemplates_jp)を使用して、バインドしたい配信ポリシーのIDを取得できます。 |`tpl-s2Q4mq` |
|SparrowRules |Object[] |いいえ |エッジ関数の転送ルールのセットを表します。各ルールはフィルタリング条件設定と操作設定を含みます。 | |
|Condition |Object |いいえ |現在のルール内のフィルタリング条件設定を表します。 | |
|ConditionRule |Object[] |はい |ユーザーリクエストをフィルタリングするためのフィルタリング条件のセットを表します。現在、1つのフィルタリング条件のみを指定できます。 | |
|Object |String |はい |フィルタリングタイプを表します。このパラメータには以下の値があります：<br><br><br>* `filetype`：リクエストURL内の拡張子を表します。<br><br>* `Directory`：リクエストURL内の特定のディレクトリを表します。<br><br>* `path`：完全なリクエストURLを表します。 | |
|Operator |String |はい |比較タイプを表します。このパラメータの値は`match`のみ可能であり、`Value`がリクエスト内の`Object`と同じ場合、このリクエストはこのフィルタリング条件を満たすことを表します。 | |
|Type |String |はい |`Object`が属するオブジェクトを表します。現在、このパラメータの値は`url`のみ可能であり、"リクエストURL"を表します。 | |
|Value |String |はい |1つまたは複数のフィルタリング値を表し、総長は1,024文字を超えることはできません。複数のフィルタリング値はセミコロン（;）で区切られます。フィルタリング値には以下の文字を含めることはできません：<br><br><br>* 連続するスラッシュ（//）、スペース、ドル記号（$）、クエスチョンマーク（?）、Delete（ASCIIコード127）。<br><br><br>また、<br><br><br>* `Object`が`filetype`の場合、各フィルタリング値はリクエストURLのサフィックスを表し、ピリオド（.）で開始する必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object`が`directory`の場合、各フィルタリング値はディレクトリパスを表し、スラッシュ（/）で開始および終了します。例：`/chs/foods/;/us/birds/`。<br><br>* `Object`が`path`の場合、各フィルタリング値はURLパスを表し、スラッシュ（/）で開始します。各フィルタリング値には1つまたは複数の文字を表すワイルドカード（\*）を含めることができます。例：`/chs/foods/local*sets;/us/birds/chickadee`。 | |
|SparrowAction |Object |いいえ |ユーザーリクエストが`Condition`を満たす場合、CDNが実行する操作の設定を表します。 | |
|IgnoreCase |Boolean |いいえ |`ConditionRule`内の`Value`が大文字小文字を区別するかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：`Value`が大文字小文字を区別しないことを表します。<br><br>* `false`：`Value`が大文字小文字を区別することを表します。<br><br><br>このパラメータのデフォルト値は`true`です。 | |
|SparrowID |String |いいえ |ユーザーリクエストを処理する関数のIDを表します。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction_jp)を呼び出してIDを取得できます。 | |
|SparrowSwitch |String |いいえ |"エッジ関数"機能を有効にするかどうかを表します。このパラメータを設定する場合、`Domains`には1つのドメイン名のみを指定できます。<br><br>このパラメータには以下の値があります：<br><br><br>* `on`：この機能を有効にすることを表します。<br><br>* `off`：この機能を有効にしないことを表します。<br><br><br>このパラメータのデフォルト値は`off`です。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateTemplateDomain&Version=2021-03-01
{
    "Domains": [
        "www.example.com"
    ],
    "CipherTemplateId": "tpl-cqgRvW",
    "HTTPSSwitch": "on",
    "ServiceRegion": "outside_chinese_mainland",
    "ServiceTemplateId": "tpl-s2Q4mq",
    "CertId": "cert-044833503b2345b4b42c2e81z0aa5c23",
    "SparrowRules": [
        {
            "Condition": {
                "ConditionRule": [
                    {
                        "Object": "filetype",
                        "Operator": "match",
                        "Type": "url",
                        "Value": "asp;php;jsp;ashx;aspx;do"
                    }
                ],
                "Connective": "OR"
            },
            "SparrowAction": {
                "Action": "bypass",
                "IgnoreCase": true,
                "SparrowID": "96ec5429956c42f79a717a4649f3d455"
            }
        }
    ],
    "SparrowSwitch": "on"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateTemplateDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
