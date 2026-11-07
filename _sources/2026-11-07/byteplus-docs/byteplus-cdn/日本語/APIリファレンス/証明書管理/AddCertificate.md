---
title: "AddCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/AddCertificate_jp"
---

BytePlus CDNにサーバー証明書をアップロードし、ドメインのHTTPSを設定するために使用します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はAddCertificateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Source |String |いいえ |証明書の保存場所を示します。このパラメータの値は`cert_center`のみで、BytePlus証明書センターを指します。 |`cert_center` |
|Certificate |String |はい |証明書ファイルの内容を示します。完全な証明書チェーンを含めることをお勧めします。内容の改行はに置き換える必要があります。証明書ファイルの拡張子は.crtまたは.pemです。 |`-----BEGIN CERTIFICATE-----\r\n......\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\n.......\r\n-----END CERTIFICATE-----` |
|PrivateKey |String |はい |証明書の秘密キーファイルの内容を示します。内容の改行はに置き換える必要があります。証明書の秘密キーファイルの拡張子は.keyまたは.pemです。 |`-----BEGIN RSA PRIVATE KEY-----\r\n.....\r\n-----END RSA PRIVATE KEY-----` |
|Desc |String |いいえ |この証明書の備考を示します。 |`Note` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|CertId |String |アップロード後、この証明書の`Source`でのIDを示します。 |`cert-17f1d965a11342eb80d9a0ecfef35713` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021-03-01
{
    "Source": "cert_center",
    "Certificate": "-----BEGIN CERTIFICATE-----\r\nMIGrhI\r\nmg==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIIE ==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIID \r\nMrY=\r\n-----END CERTIFICATE-----",
    "PrivateKey": "-----BEGIN RSA PRIVATE KEY-----\r\nMIIjQVx9Q==\r\n-----END RSA PRIVATE KEY-----"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240402082809CAFB8B06254524ECDFF3",
        "Action": "AddCertificate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertId": "cert-c6424725984f4c69b671e119aa0ffa69"
    }
}
```


&nbsp;
