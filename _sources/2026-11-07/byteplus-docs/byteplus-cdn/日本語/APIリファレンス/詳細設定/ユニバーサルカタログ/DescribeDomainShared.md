---
title: "DescribeDomainShared"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_jp"
---

ユニバーサルカタログを指定し、そのユニバーサルカタログに関連付けられているドメイン名を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeDomainSharedです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConfigName |String |いいえ |ユニバーサルカタログの名前を表し、そのユニバーサルカタログに関連付けられているドメイン名を照会します。 |`my_whitelist` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|ConfigName |String |このユニバーサルカタログの名前を表します。 |`my_whitelist` |
|Domain |String[] |このユニバーサルカタログに関連付けられているドメイン名のリストを表します。このユニバーサルカタログがまだどのドメイン名とも関連付けられていない場合、このパラメータの値は空の配列になります。<br><br>このAPIを呼び出す際、IAMユーザーがこのユニバーサルカタログに関連付けられている特定のドメイン名にアクセスする権限がない場合、そのドメイン名は`Domain`リストに表示されません。 |`["example.com","www.example.com"]` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021-03-01
{
    "ConfigName": "test11"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209063311CB50419F0326B7CA55A4",
        "Action": "DescribeDomainShared",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigName": "test11",
        "Domain": [
            "www.example.com"
        ]
    }
}
```


&nbsp;
