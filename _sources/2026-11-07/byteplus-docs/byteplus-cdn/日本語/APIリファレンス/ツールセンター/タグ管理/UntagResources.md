---
title: "UntagResources"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UntagResources_jp"
---

1つまたは複数のドメイン名から、指定された1つまたは複数のタグを削除します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUntagResourcesです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ResourceIds |String[] |はい |指定されたタグを削除する必要があるドメイン名のリスト。リストには最大50個のドメイン名を含めることができます。 |`["www.example.com","img.example.com"]` |
|ResourceType |String |はい |リソースのタイプ。このパラメーターの値は `domain` のみです。 |`domain` |
|TagKeys |String[] |はい |Key のリスト。リストには最大50個のタグ Key を含めることができます。この API は、`ResourceIds` からこれらの Key に対応するタグを削除します。<br><br>说明<br><br>ドメイン名からタグを削除する場合、この API は `TagKeys` に存在する Key を持つタグのみを削除します。`TagKeys` 内の特定の Key について、`ResourceIds` 内のドメイン名にその Key に対応するタグが存在しない場合、この API はその Key をスキップします。 |`["key1","key2"]` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=UntagResources&Version=2021-03-01
{
        "ResourceType": "domain",
        "ResourceIds": ["www.example.com","img.example.com"],
    "TagKeys": [
        {
            "myKey1",
            "myKey2"
        }
    ]
}
```


&nbsp;
