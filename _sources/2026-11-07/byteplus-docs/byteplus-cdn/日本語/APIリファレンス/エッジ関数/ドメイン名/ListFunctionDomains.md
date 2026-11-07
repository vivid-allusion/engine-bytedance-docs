---
title: "ListFunctionDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunctionDomains_jp"
---

指定した関数に関連付け可能なドメイン名のリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエストの説明"></span>
## リクエストの説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `ListFunctionDomains` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |ドメイン名を関連付ける関数のID。 |
|Page |Integer |はい |ページ番号 |
|Limit |Integer |はい |1ページあたりのレコード数。<br><br>&nbsp;<br><br>現在、1回のリクエストで最大50レコードまで取得可能です。 |
|OrderBy |Integer |いいえ |データクエリの順序を指定するパラメータ。以下の値を受け入れます：<br><br><br>* 1：降順でデータをソート<br><br>* 2（デフォルト）：昇順でデータをソート |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|Domains |Object[] |ドメイン名リスト。 |`["test.example.com"]` |
|Domain |String |ドメイン名。 |`test.example.com` |
|BindStatus |Integer |ドメイン名と指定した関数間の関連付けステータス：<br><br><br>* 1：関連付け済み<br><br>* 2：関連付け可能<br><br>* 3：関連付け不可 |`2` |
|TotalCount |Long |関数の総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunctionDomains&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****&Page=1&Limit=10
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2023050920020063355B94DB6C32617243",
        "Action": "ListFunctionDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domains": [
            {
                "Domain": "123.example.com",
                "BindStatus": 2
            },
            {
                "Domain": "test.example.com",
                "BindStatus": 2
            }
        ],
        "TotalCount": 3
    }
}
```


&nbsp;
