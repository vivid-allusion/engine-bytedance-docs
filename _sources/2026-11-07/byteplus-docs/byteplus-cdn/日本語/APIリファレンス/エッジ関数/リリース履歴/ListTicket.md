---
title: "ListTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListTicket_jp"
---

関数のリリース履歴リストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListTicket&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `ListTicket` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|Page |Integer |いいえ |ページ番号。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。デフォルトは50件。最大50件まで。 |
|OrderBy |Integer |いいえ |ソート方法。<br><br><br>* 1は降順を示します。<br><br>* 2は昇順を示します。<br><br><br>デフォルトは関数IDの昇順でソートされます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|Tickets |Object[] |リリース履歴リスト。 | |
|Id |Long |リリース履歴ID。 |`1` |
|FunctionId |String |関数ID。 |`23455331245` |
|Content |String |リリース履歴のコンテンツ |`{&quot;current_traffics&quot;:[{&quot;version_tag&quot;:&quot;1.0.1&quot;}],&quot;origin_traffics&quot;:[]}` |
|Status |Integer |リリースステータス。<br><br><br>* 100：カナリアリリース成功。<br><br>* 200：フルリリース成功。 |`100` |
|Description |String |リリース履歴の説明。 |`this is a release` |
|Creator |String |リリース履歴の作成者。 |`example` |
|CreateTime |Long |作成時刻。Unixタイムスタンプ形式（秒）。 |`1638326159` |
|UpdateTime |Long |更新時刻。Unixタイムスタンプ形式（秒）。 |`1638326159` |
|TotalCount |Long |リリース履歴の数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListTicket&Version=2021-03-01&FunctionId=23455331245&Page=1&Limit=10&OrderBy=2
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tickets": [
            {
                "Id": 133,
                "FunctionId": "23455331245",
                "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
                "Description": "test publish",
                "Creator": "****",
                "CreateTime": 1640077698,
                "UpdateTime": 1640077759
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
