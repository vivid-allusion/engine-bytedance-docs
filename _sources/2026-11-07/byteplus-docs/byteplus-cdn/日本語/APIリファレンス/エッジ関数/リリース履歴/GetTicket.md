---
title: "GetTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetTicket_jp"
---

リリース履歴を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetTicket&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `GetTicket` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|TicketId |Long |はい |リリース履歴ID。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例値 |
|---|---|---|---|
|Ticket |Object |リリース履歴の詳細。 | |
|Id |Long |リリース履歴ID。 |`1` |
|FunctionId |String |関数ID。 |`23455331245` |
|Content |String |リリース履歴のコンテンツ。 |`{&quot;current_traffics&quot;:[{&quot;version_tag&quot;:&quot;1.0.1&quot;}],&quot;origin_traffics&quot;:[]}` |
|Status |Integer |リリースステータス。<br><br><br>* 100：カナリアリリース成功。<br><br>* 200：フルリリース成功。 |`100` |
|Description |String |リリース履歴の説明。 |`this is a release` |
|Creator |String |リリース履歴の作成者。 |`test_user` |
|CreateTime |Long |リリース履歴の作成時刻。Unixタイムスタンプ形式（秒）。 |`1638326159` |
|UpdateTime |Long |リリース履歴の更新時刻。Unixタイムスタンプ形式（秒）。 |`1638326159` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
GET  https://cdn.byteplusapi.com?Action=GetTicket&Version=2021-03-01&FunctionId=3gyz993****&TicketId=28
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "GetTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Ticket":
         {
            "Id": 133,
            "FunctionId": "3gyz993****",
            "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
            "Description": "test publish",
            "Creator": "****",
            "CreateTime": 1640077698,
            "UpdateTime": 1640077759
        }
    }
}
```


&nbsp;
