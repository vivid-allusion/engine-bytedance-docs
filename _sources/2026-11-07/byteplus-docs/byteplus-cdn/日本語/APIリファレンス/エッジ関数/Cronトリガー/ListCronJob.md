---
title: "ListCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCronJob_jp"
---

Cronトリガーリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `ListCronJob` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|Page |Integer |いいえ |ページ番号。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。デフォルトは50件。最大50件まで。 |
|OrderBy |Integer |いいえ |このパラメータはデータクエリの順序を指定します。以下の値を受け付けます：<br><br><br>* 1：降順でデータを並べ替えます。<br><br>* 2（デフォルト）：昇順でデータを並べ替えます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例値 |
|---|---|---|---|
|Jobs |Object[] |トリガーリスト。 | |
|JobName |String |Cronトリガー名。 |`cron1` |
|CronExpression |String |Cron式。 |`*/1 * * **` |
|Parameter |String |カスタムパラメータ。 |`cron` |
|Description |String |トリガー説明。 |`test` |
|JobState |Long |トリガー状態。<br><br><br>* 1：実行待ち<br><br>* 3：無効<br><br>* 4：キャンセル |`1` |
|CronType |Integer |Cronトリガーの範囲。可能な値は：<br><br>1：グローバル：すべてのエッジノードで実行。<br><br>2：単一ノード：ランダムに任意のエッジノードで実行。 |`1` |
|CreateTime |Long |作成時間。 |`1638326159` |
|UpdateTime |Long |更新時間。 |`1638326159` |
|TotalCount |Long |トリガー総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJob&Version=2021-03-01&FunctionId=3gyz993****&Page=1&Limit=10&OrderBy=2
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJob",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Jobs": [
            {
                "JobName": "cron2",
                "CronExpression": "*/59 * * * *",
                "Parameter": "cron_all",
                "Description": "",
                "JobState": 1,
                "CronType": 2,
                "Operator": "****",
                "CreateTime": 1638871686,
                "UpdateTime": 1638871686
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
