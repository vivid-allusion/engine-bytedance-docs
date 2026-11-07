---
title: "DeleteCdnCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteCdnCertificate_jp"
---

CDNでホストされている証明書を削除します。ドメイン名に関連付けられていない証明書のみを削除できます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：毎秒最大 20 の API リクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DeleteCdnCertificate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDeleteCdnCertificateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|CertId |String |はい |削除する証明書の ID を表します。証明書 ID は `cert_hosting` で始まります。 |`cert_hosting-4041`<br><br> |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteCdnCertificate&Version=2021-03-01
{
    "CertId": "cert_hosting-4041"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202207131500530102120352272280EC8F",
        "Action": "DeleteCdnCertificate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
