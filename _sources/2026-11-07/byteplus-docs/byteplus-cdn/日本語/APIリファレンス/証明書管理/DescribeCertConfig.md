---
title: "DescribeCertConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCertConfig_jp"
---

指定された証明書に関連付け可能なドメイン名の証明書設定を取得します。これらのドメインは、指定された証明書のSANフィールドにあり、CDN に追加されています。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeCertConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|CertId |String |はい |照会する証明書のID。<br><br>証明書IDを取得するには、[ListCdnCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnCertInfo_jp)を呼び出します。 |`cert-5dc4bfa90c1048778abf036b03ffabf2` |
|Status |String |いいえ |このAPIから返されるドメインをフィルタリングするために使用されるドメイン名のステータス。複数のステータスを指定でき、コンマ（,）で区切ります。<br><br>このパラメーターには次の値を指定できます。<br><br><br>* `online`：ステータスが「実行中」であることを示します。<br><br>* `offline`：ステータスが「オフライン」であることを示します。<br><br>* `configuring`：ステータスが「設定中」であることを示します。<br><br><br>このパラメーターを指定しない場合、ドメインはフィルタリングされません。 |`online,configuring` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|CertNotConfig |Object[] |`CertId` に関連付けることができるが、まだどの証明書にも関連付けられていないドメイン名のリスト。 | |
|Domain |String |リスト内のドメイン名。 |`img.example.com` |
|Status |String |ドメイン名のステータス。次の値を指定できます。<br><br><br>* `online`：ステータスが「実行中」であることを示します。<br><br>* `offline`：ステータスが「オフライン」であることを示します。<br><br>* `configuring`：ステータスが「設定中」であることを示します。 |`offline` |
|DomainLock |Object |ドメイン名がロックされているかどうかを示します。ドメイン名がロックされている場合、その設定を変更することはできません。 | |
|Remark |String |ドメイン名がロックされている理由。<br><br><br>* `DomainLock`構造体の`Status`が`on`の場合、このパラメーターはドメイン名がロックされている理由を示します。<br><br>* `Status`が`off`の場合、このパラメーターの値は空（""）です。 |`域名锁定，不允许自助配置操作，代运维配置中` |
|Status |String |ドメイン名のロック状態。このパラメーターには次の値を指定できます。<br><br><br>* `on`：ドメイン名がロックされていることを示します。<br><br>* `off`：ドメイン名がロックされていないことを示します。 |`off` |
|SpecifiedCertConfig |Object[] |`CertId` に既に関連付けられているドメイン名のリスト。 | |
|Domain |String |リスト内のドメイン名。 |`abc.example.com` |
|Status |String |ドメイン名のステータス。このパラメーターには次の値を指定できます。<br><br><br>* `online`：ステータスが「実行中」であることを示します。<br><br>* `offline`：ステータスが「オフライン」であることを示します。<br><br>* `configuring`：ステータスが「設定中」であることを示します。 |`configuring` |
|CerStatus |String |ドメインに関連付けられている証明書のステータス。このパラメーターには次の値を指定できます。<br><br><br>* `running`：証明書の有効期間が30日を超えていることを示します。<br><br>* `expired`：証明書が既に失効していることを示します。<br><br>* `expiring_soon`：証明書の有効期間が30日以下であるが、まだ失効していないことを示します。 |`expiring_soon` |
|DomainLock |Object |ドメイン名がロックされているかどうかを示します。ドメイン名がロックされている場合、その設定を変更することはできません。 | |
|Remark |String |ドメイン名がロックされている理由。<br><br><br>* `DomainLock`構造体の`Status`が`on`の場合、このパラメーターはドメイン名がロックされている理由を示します。<br><br>* `Status`が`off`の場合、このパラメーターの値は空（""）です。 |`some reason` |
|Status |String |ドメイン名のロック状態。このパラメーターには次の値を指定できます。<br><br><br>* `on`：ドメイン名がロックされていることを示します。<br><br>* `off`：ドメイン名がロックされていないことを示します。 |`on` |
|OtherCertConfig |Object[] |`CertId` に関連付けることができるが、既に他の証明書に関連付けられているドメイン名のリスト。 | |
|Domain |String |リスト内のドメイン名。 |`www.example.com` |
|Status |String |ドメイン名のステータス。次の値を指定できます。<br><br><br>* `online`：ステータスが「実行中」であることを示します。<br><br>* `offline`：ステータスが「オフライン」であることを示します。<br><br>* `configuring`：ステータスが「設定中」であることを示します。 |`online` |
|CerStatus |String |ドメインに関連付けられている証明書のステータス。このパラメーターには次の値を指定できます。<br><br><br>* `running`：証明書の有効期間が30日を超えていることを示します。<br><br>* `expired`：証明書が既に失効していることを示します。<br><br>* `expiring_soon`：証明書の有効期間が30日以下であるが、まだ失効していないことを示します。 |`running` |
|DomainLock |Object |ドメイン名がロックされているかどうかを示します。ドメイン名がロックされている場合、その設定を変更することはできません。 | |
|Remark |String |ドメイン名がロックされている理由。<br><br><br>* `DomainLock`構造体の`Status`が`on`の場合、このパラメーターはロックの理由を示します。<br><br>* `Status`が`off`の場合、このパラメーターの値は空（""）です。 | |
|Status |String |ドメイン名のロック状態。このパラメーターには次の値を指定できます。<br><br><br>* `on`：ドメイン名がロックされていることを示します。<br><br>* `off`：ドメイン名がロックされていないことを示します。 |`off` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCertConfig&Version=2021-03-01
{
    "CertId": "cert-5dc4bfa90c1048778abf036b03ffabf2",
    "Status": "online,configuring"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403181420252BCF8FD4581E1A5AAA4E",
        "Action": "DescribeCertConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertNotConfig": [
            {
                "Domain": "abc.example.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            },
            {
                "Domain": "img.example.com.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            }
        ],
        "OtherCertConfig": [
            {
                "CerStatus": "running",
                "Domain": "doc.example.com",
                "DomainLock": {
                    "Remark": "",
                    "Status": "off"
                },
                "Status": "online"
            }
        ],
        "SpecifiedCertConfig": [
            {
                "CerStatus": "expiring_soon",
                "Domain": "www.example.com",
                "DomainLock": {
                    "Remark": "Domain locked against unauthorized changes. Acting administration on behalf of customer",
                    "Status": "on"
                },
                "Status": "online"
            }
        ]
    }
}
```


&nbsp;
