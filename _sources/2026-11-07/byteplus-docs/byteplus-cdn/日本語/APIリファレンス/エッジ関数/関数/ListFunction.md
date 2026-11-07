---
title: "ListFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction_jp"
---

関数リストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエストの説明"></span>
## リクエストの説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListFunction&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API 名称。現在のAPIの名前は `ListFunction` です。 |
|Version |String |はい |API バージョン。現在のAPIのバージョンは `2021-03-01` です。 |
|Page |Integer |いいえ |ページ番号。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。デフォルトは100です。1回のリクエストで最大100レコードを取得できます。 |
|OrderBy |Integer |いいえ |このパラメータはデータクエリの順序を指定します。以下の値を受け付けます：<br><br><br>* 1：データを降順でソートします。<br><br>* 2（デフォルト）：データを昇順でソートします。 |
|OrderType |String |いいえ |利用可能なソートタイプ：<br><br><br>* create_time（デフォルト）：作成時間に基づいてデータをソートします。<br><br>* update_time：最終更新時間に基づいてデータをソートします。 |
|Status |String |いいえ |関数のステータス。<br><br><br>* 100：実行中<br><br>* 400：未関連付け<br><br>* 500：設定中 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |サンプル値 |
|---|---|---|---|
|Functions |Object[] |関数リスト。 | |
|AccountIdentity |Long |BytePlus アカウントID。 |`20****` |
|UserIdentity |Long |このパラメータには実質的な意味はありません。このパラメータを無視してください。 | |
|Domain |String[] |関数に関連つけられたドメイン。 |`["example.com"]` |
|Name |String |関数の名前。 |`hello-ve` |
|FunctionId |String |関数のID。 |`3gyz993****` |
|Status |Integer |関数のステータス。<br><br><br>* 100：実行中<br><br>* 400：未関連付け<br><br>* 500：設定中 |`100` |
|Creator |String |関数を作成したユーザー名。 |`example` |
|CreateTime |Long |作成日時。Unixタイムスタンプ（秒）形式。 |`1638326159` |
|UpdateTime |Long |更新日時。Unixタイムスタンプ（秒）形式。 |`1638326159` |
|Remark |String |関数の備考。 |`this is a test` |
|ProjectName |String |関数が属するプロジェクトの名前。 |`default` |
|TotalCount |Long |関数の総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListFunction&Version=2021-03-01
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
  "ResponseMetadata": {
    "RequestId": "202404220913221B87E7D87928AD8F42F8",
    "Action": "ListFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
        "Functions": [
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test1.example.com"
                ],
                "Name": "test1",
                "ClazzName": "Free",
                "BindingType": 200,
                "FunctionId": "54ac587666c148a6b9ffacbb0cb1****",
                "Status": 100,
                "IsPublish": true,
                "IsFullPublish": true,
                "CodeType": "",
                "Creator": "example_user",
                "CreateTime": 1711004239,
                "UpdateTime": 1713270175,
                "Remark": "",
                "ProjectName": "default"
            },
            {
                "AccountIdentity": 300000****,
                "UserIdentity": 0,
                "Domain": [
                    "test2.example.com"
                ],
                "Name": "test",
                "ClazzName": "Free",
                "BindingType": 0,
                "FunctionId": "bc36dc7c58e942f0b9f125d186df****",
                "Status": 400,
                "IsPublish": false,
                "IsFullPublish": false,
                "CodeType": "",
                "Creator": "example_user",
                "CreateTime": 1713776330,
                "UpdateTime": 1713776330,
                "Remark": "",
                "ProjectName": "default"
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
