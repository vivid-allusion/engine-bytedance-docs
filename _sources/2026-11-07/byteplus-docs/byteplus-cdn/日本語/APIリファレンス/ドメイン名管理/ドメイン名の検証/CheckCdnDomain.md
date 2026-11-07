---
title: "CheckCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CheckCdnDomain_jp"
---

指定されたドメイン名の所有権を検証します。このAPIを呼び出す前に、CDNコンソールプロンプトに従って、ドメイン名のDNSサービスプロバイダーで対応する TXT レコードが作成されていることを確認してください。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：毎秒最大 20 のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はCheckCdnDomainです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |はい |検証するドメイン名を表し、ワイルドカードドメイン名も使用できます。 |`www.example.com` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Status |String |検証結果を示します。このパラメーターには次の値があります：<br><br><br>* `fail`：検証が失敗したことを示します。<br><br>* `success`：検証が成功したことを示します。 |`fail` |
|ErrorMsg |String |検証が失敗した理由を示します。`Status` が `success` の場合、このパラメーターの値は空（""）です。 |`some reason` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20241206143123375BE43944CA95D1969A",
        "Action": "CheckCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ErrorMsg": "some error",
        "Status": "fail"
    }
}
```


&nbsp;
