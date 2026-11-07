---
title: "ListCdnCertInfo"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp"
---

フィルタリング条件に一致する証明書と、それらの証明書に関連付けられているドメイン名のリストを取得します。

IAMユーザーがこのAPIを呼び出す場合、リスト内のドメイン名はIAMユーザーがアクセス権を持つドメイン名です。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListCdnCertInfoです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|CertId |String |いいえ |証明書のID。このIDの証明書を取得します。<br><br>[ListCertInfo](https://docs.byteplus.com/zh-CN/byteplus-cdn/reference/ListCertInfo_jp)を使用して、指定したい証明書のIDを取得できます。 |`cert-c195f679cecb4f34tj23dd8c54e6c0a2,cert-c195f67945u84fcd9823dd8c53eec0a2` |
|ConfiguredDomain |String |いいえ |ドメイン名のリスト。リスト内の各ドメインに関連付けられている証明書を取得します。複数のドメイン名はコンマ（,）で区切ります。<br><br>リストにはワイルドカードドメインを含めることができます。ただし、ワイルドカードドメインの場合、証明書に関連付けられているドメインにそのワイルドカードドメイン名が含まれている場合にのみ、その証明書は`ConfiguredDomain`フィルタリング条件を満たすと見なされることに注意してください。たとえば、指定した`ConfiguredDomain`が`*.example.com`であるとします。証明書に関連付けられているドメインに`www.example.com`は含まれているが`*.example.com`は含まれていない場合、その証明書はこのフィルタリング条件を満たしません。 |`*.example.com, www.test.com` |
|DnsName |String |いいえ |ドメイン名のリスト。SANフィールドにリスト内のいずれかのドメイン名が含まれている証明書を取得します。複数のドメイン名はコンマ（,）で区切ります。<br><br>リストにはワイルドカードドメインを含めることができます。ただし、ワイルドカードドメインの場合、証明書のSANフィールドにそのワイルドカードドメイン名が含まれている場合にのみ、その証明書は`DnsName`フィルタリング条件を満たすと見なされることに注意してください。たとえば、指定した`DnsName`が`*.example.com`であるとします。証明書のSANフィールドに`www.example.com`は含まれているが`*.example.com`は含まれていない場合、その証明書はこのフィルタリング条件を満たしません。 |`*.example.com, www.test.com` |
|PageNum |Long |いいえ |APIから返される証明書リストの場合、このパラメーターはページ番号を示します。APIが実際に返す証明書リストは、このページ番号で指定されたページ上の証明書です。<br><br>APIから返される証明書は`PageSize`に基づいてページ分割されます。APIから返される証明書の数が100で、指定した`PageSize`が`10`であると仮定すると、返される証明書は10ページに分散されます。`PageNum`を`2`に指定すると、2ページ目の証明書が取得されます。<br><br>指定したページに証明書がない場合、返される結果の`CertInfo`パラメーターの値は`null`になります。<br><br>`PageNum`のデフォルト値は`1`です。 |`1` |
|PageSize |Long |いいえ |各ページに含まれる証明書の数。<br><br>このパラメーターの値の範囲は1〜100で、デフォルト値は`10`です。 |`5` |
|Source |String |いいえ |証明書の保存場所。この場所に保存されている証明書を取得します。現在、このパラメーターの値は`cert_center`のみ可能で、BytePlus証明書センターを示します。 |`cert_center` |
|Status |String |いいえ |証明書ステータスのリスト。リスト内のいずれかのステータスにある証明書を取得します。このパラメーターには次の値を指定できます。<br><br><br>* `running`：証明書の有効期間が30日を超えていることを示します。<br><br>* `expired`：証明書が既に失効していることを示します。<br><br>* `expiring_soon`：証明書の有効期間が30日以下であるが、まだ失効していないことを示します。<br><br><br>複数の証明書ステータスはコンマ（,）で区切ります。 |`running,expired` |
|Configured |Boolean |いいえ |APIから返される`CertInfo`で、どのドメインにも関連付けられていない証明書を削除するかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：どのドメインにも関連付けられていない証明書を削除することを示します。<br><br>* `false`：どのドメインにも関連付けられていない証明書を保持することを示します。<br><br><br>このパラメーターのデフォルト値は`true`です。 |`true` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|PageNum |Long |リクエストパラメーターの`PageNum`の値。 |`1` |
|PageSize |Long |リクエストパラメーターの`PageSize`の値。 |`10` |
|Total |Long |フィルタリング条件に一致する証明書の数。このパラメーターの値は`PageNum`と`PageSize`の影響を受けません。 |`8` |
|CertInfo |Object[] |フィルタリング条件に一致する証明書のリスト。フィルタリング条件に一致する証明書がない場合、このパラメーターの値は`null`です。 | |
|Source |String |返された証明書リスト内の証明書の場合、このパラメーターはその証明書の保存場所を示します。現在、このパラメーターの値は`cert_center`のみ可能で、BytePlus証明書センターを示します。 |`volc_cert_center` |
|CertId |String |この証明書のID。 |`cert-602fc4eb6cbf4b9351b54bedf2bc5dc5` |
|CertName |String |この証明書の`Common Name (CN)`フィールドの内容。 |`www.example.com` |
|Status |String |この証明書のステータス。このパラメーターには次の値を指定できます。<br><br><br>* `running`：証明書の有効期間が30日を超えていることを示します。<br><br>* `expired`：証明書が既に失効していることを示します。<br><br>* `expiring_soon`：証明書の有効期間が30日以下であるが、まだ失効していないことを示します。 |`running` |
|EffectiveTime |Long |この証明書の発行時刻。単位はUnixタイムスタンプです。 |`1655856000` |
|ExpireTime |Long |この証明書の有効期限。単位はUnixタイムスタンプです。 |`1687478399` |
|DnsName |String |この証明書のSANフィールド内のドメイン名。複数のドメイン名はコンマ（,）で区切ります。 |`www.example.com` |
|ConfiguredDomain |String |この証明書に既に関連付けられているドメイン名のリスト。複数のドメイン名はコンマ（,）で区切ります。<br><br>リクエストパラメーター`Configured`が`false`で、この証明書がどのドメインにも関連付けられていない場合、このパラメーターの値は`null`です。 |`www.example.com` |
|Desc |String |この証明書の備考。 |`UploadCert` |
|CertFingerprint |Object |この証明書のフィンガープリント情報。 | |
|Sha1 |String |SHA\-1暗号化アルゴリズムに基づくフィンガープリント。40文字の16進数で構成されます。 |`4f6c4bd5402e8f848837bf1334740ece0671ae4d` |
|Sha256 |String |SHA\-256暗号化アルゴリズムに基づくフィンガープリント。64文字の16進数で構成されます。 |`24e49e0888f91a25f1503b452aa7cf0cf30da637810eaee5309b0be6c3931c9d` |
|ExpiringCount |Long |フィルタリング条件に一致する証明書のうち、ステータスが`expiring_soon`である証明書の数。ただし、現在このパラメーターはまだ有効ではないため、このパラメーターの値は常に`0`です。 |`0` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnCertInfo&Version=2021-03-01
{
    "CertId": "cert-602fc4eb6cbf4b9351b54bedf2bc5dc5",
    "ConfiguredDomain": "www.example.com,*.test.com",
    "DnsName": "*.example.com,www.test.com",
    "Status": "running,expiring_soon",
    "Configured": true
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031811030837EB957CFE06970AC404",
        "Action": "ListCdnCertInfo",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertInfo": [
            {
                "CertId": "cert-602fc4eb6cbf4b9351b54bedf2bc5dc5",
                "CertName": "*.example.com",
                "ConfiguredDomain": "*.example.com",
                "Desc": "Test",
                "DnsName": "*.example.com",
                "EffectiveTime": 1694415266,
                "ExpireTime": 1725951266,
                "Source": "cert_center",
                "Status": "running"
            }
        ],
        "ExpiringCount": 0,
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
