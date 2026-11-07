---
title: "ListCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCertInfo_jp"
---

フィルタリング条件に一致する証明書情報を取得します。このAPIが取得する証明書は、BytePlus証明書センターに保存されており、お客様のアカウントのドメイン名に関連付けることができる、または既に関連付けられている証明書です。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Body内のオプションパラメータを指定しない場合、そのパラメータを使用して証明書をフィルタリングしないことを示します。</div>


<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListCertInfoです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Source |String |はい |証明書の保存場所を示します。現在、このパラメータの値は`cert_center`のみで、BytePlus証明書センターを指します。 |`cert-center` |
|CertId |String |いいえ |証明書ID。このIDの証明書を取得します。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|ConfiguredDomain |String |いいえ |ドメイン名のリスト。リスト内のいずれかのドメインにバインドされている証明書を取得します。 |`www.example.com,www.test.com` |
|FuzzyMatch |Boolean |いいえ |`Name`を指定した場合、`FuzzyMatch`は`Name`を使用して証明書をフィルタリングする際にCDNが使用するマッチング方法を示します。このパラメータには次の値を指定できます。<br><br><br>* `true`：あいまい一致。<br><br>* `false`：完全一致。<br><br><br>`Name`を指定しない場合、`FuzzyMatch`は無効です。<br><br>`FuzzyMatch`のデフォルト値は`false`です。 |`true` |
|Name |String |いいえ |SANフィールドにそのドメインが含まれている証明書を取得するためのドメイン名。このドメイン名はワイルドカードドメインにすることができます。たとえば、`*.example.com`を指定すると、SANフィールドに`img.example.com`や`www.example.com`など、そのワイルドカードドメインに一致する証明書が取得されます。 |`*.example.com` |
|PageNum |Long |いいえ |フィルタリング条件に一致する証明書のリストについて、このパラメータはページ番号を示し、APIが実際に表示する証明書はそのページ番号で指定されたページ上の証明書です。<br><br>このAPIから返される証明書は`PageSize`に基づいてページ分割されます。このAPIから返される証明書の数が100で、指定した`PageSize`が`10`であると仮定すると、返される証明書は10ページに分散されます。`PageNum`を`2`に指定すると、2ページ目の証明書が取得されます。<br><br>指定したページに証明書がない場合、返される結果の`CertInfo`パラメータの値は`null`になります。<br><br>`PageNum`のデフォルト値は`1`です。 |`1` |
|PageSize |Long |いいえ |各ページに含まれる証明書の数。<br><br>このパラメータの値の範囲は1〜100で、デフォルト値は`10`です。 |`5` |
|Status |String |いいえ |ステータスのリスト。リスト内のいずれかのステータスにある証明書を取得します。複数のステータスはコンマ（,）で区切ります。このパラメータには次の値を指定できます。<br><br><br>* `running`：有効期間が30日を超える証明書。<br><br>* `expired`：有効期限が切れた証明書。<br><br>* `expiring_soon`：有効期間が30日以下で、まだ有効期限が切れていない証明書。 |`running,expired` |
|SortRule |Object |いいえ |このAPIから返される証明書をソートするためのソート規則。デフォルトの規則では、応答の`ExpireTime`パラメータに基づいて返される証明書を昇順にソートします。 | |
|Asc |Boolean |いいえ |ソート方法。このパラメータには次の値を指定できます。<br><br><br>* `false`：リスト内の証明書を降順に並べ替えます。<br><br>* `true`：リスト内の証明書を昇順に並べ替えます。<br><br><br>このパラメータのデフォルト値は`true`です。 |`false` |
|OrderBy |String |いいえ |返される証明書をどのフィールドでソートするかを示します。SortRuleを指定した場合、`OrderBy`は必須です。現在、`OrderBy`の値は`ExpireTime`である必要があり、証明書の有効期限でソートすることを示します。 |`ExpireTime` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|PageNum |Long |リクエストパラメータで指定した`PageNum`。 |`1` |
|PageSize |Long |リクエストパラメータで指定した`PageSize`。 |`10` |
|Total |Long |フィルタリング条件に一致する証明書の数。このパラメータの値は`PageSize`と`PageNum`の影響を受けません。 |`2` |
|CertInfo |Object[] |このAPIから返される証明書のリスト。<br><br>リスト内の証明書は、リクエストパラメータ`PageNum`が表すページ上の証明書であり、必ずしもフィルタリング条件に一致するすべての証明書ではないことに注意してください。 | |
|Source |String |返された証明書リスト内の証明書について、このパラメータは証明書の保存場所を示し、次の値をとります。<br><br><br>* `cert_center`：BytePlus証明書センター。 |`cert_center` |
|CertId |String |この証明書のID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |この証明書の`Common Name (CN)`フィールドの内容。 |`*.example.com` |
|Status |String |この証明書のステータス。このパラメータには次の値を指定できます。<br><br><br>* `running`：証明書の有効期間が30日を超えています。<br><br>* `expired`：証明書は既に失効しています。<br><br>* `expiring_soon`：証明書の有効期間が30日以下ですが、まだ失効していません。 |`running` |
|EffectiveTime |Long |この証明書の発行時刻。単位はUnixタイムスタンプです。 |`1655856000` |
|ExpireTime |Long |この証明書の有効期限。単位はUnixタイムスタンプです。 |`1687478399` |
|DnsName |String |この証明書の`SAN`フィールドに含まれるドメイン名。複数のドメイン名はコンマ（,）で区切ります。 |`abc.example.com,www.example.com` |
|Desc |String |この証明書の備考。 |`UploadCert` |
|ConfiguredDomain |String |この証明書に既に関連付けられているドメイン名のリスト。この証明書がまだどのドメインにも関連付けられていない場合、このパラメータの値は`null`です。 |`test.example.com` |
|CertFingerprint |Object |この証明書のフィンガープリント情報。 | |
|Sha1 |String |SHA\-1暗号化アルゴリズムに基づくフィンガープリント。40文字の16進数で構成されます。 |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |SHA\-256暗号化アルゴリズムに基づくフィンガープリント。64文字の16進数で構成されます。 |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |フィルタリング条件に一致する証明書のうち、ステータスが`expiring_soon`である証明書の数。ただし、現在このパラメータはまだ有効ではないため、このパラメータの値は常に`0`です。 |`0` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListCertInfo&Version=2021-03-01
{
    "Source": "cert_center",
    "Name": "www.example.com",
    "Status": "running,expired",
    "SortRule": {
        "Asc": false,
        "OrderBy": "ExpireTime"
    }
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240315094304D1302166C42C534627B0",
        "Action": "ListCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-7b94354335aa424993ce48fa355f1e5e",
                "CertName": "www.example.com",
                "ConfiguredDomain": "www.example.com",
                "Desc": "Test",
                "DnsName": "www.example.com",
                "EffectiveTime": 1708992000,
                "ExpireTime": 1740700799,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
