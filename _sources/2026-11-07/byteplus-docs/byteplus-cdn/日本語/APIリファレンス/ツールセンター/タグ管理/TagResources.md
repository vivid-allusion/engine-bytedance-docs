---
title: "TagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/TagResources_jp"
---

1つまたは複数のタグを、指定された1つまたは複数のドメイン名に追加します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=TagResources&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はTagResourcesです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ResourceIds |String[] |はい |タグを追加する必要があるドメイン名のリストを表します。リストには最大50個のドメイン名を含めることができます。 |`["www.example.com","img.example.com"]` |
|ResourceType |String |はい |リソースのタイプを表します。このパラメータの値は `domain` のみです。 |`domain` |
|Tags |Object[] |はい |タグループを表します。リストには最大50個のタグを含めることができます。タグはキーと値のペアです。 | |
|Key |String |いいえ |リスト内のタグのキーを表し、長さは1～128文字です。キーでは大文字と小文字が区別され、Unicode文字、Unicode数字、スペース、および次のいずれかの文字を含めることができます：<br><br><br>* _./=+\-@ |`myKey` |
|Value |String |いいえ |タグの値を表し、長さは1～256文字です。このパラメータでは大文字と小文字も区別され、Unicode文字、Unicode数字、スペース、および次のいずれかの文字を含めることができます：<br><br><br>* _./=+\-@ |`myValue` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=TagResources&Version=2021-03-01
{
    "ResourceType": "domain",
    "ResourceIds": [
        "www.example.com",
        "img.example.com"
    ],
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


&nbsp;
