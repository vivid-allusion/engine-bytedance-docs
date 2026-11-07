---
title: "ListVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListVersions_jp"
---

指定した関数の公開済みコードバージョンリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListVersions&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `ListVersions` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp) を呼び出して、関数IDを取得できます。 |
|Page |Integer |いいえ |ページ番号。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。デフォルトは50件です。最大50件まで。 |
|OrderBy |Integer |いいえ |このパラメータはデータ照会の順序を指定します。以下の値を受け入れます：<br><br><br>* 1：降順でデータを並べ替えます。<br><br>* 2（デフォルト）：昇順でデータを並べ替えます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|Revisions |Object[] |コードバージョンリスト。 | |
|Id |Long |このバージョンのID。 |`1` |
|VersionTag |String |このバージョンの番号。 |`1.0.1` |
|Description |String |このバージョンの説明。 |`this is a release` |
|Creator |String |バージョンの作成者。 |`example_user` |
|TotalCount |Long |コードバージョンの総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
GET  https://cdn.byteplusapi.com?Action=ListVersions&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310282201022524312506*******",
        "Action": "ListVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Revisions": [
            {
                "Id": 133,
                "VersionTag": "1.0.1",
                "Description": "test publish",
                "Creator": "*****"
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
