---
title: "ListCronJobTaskLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCronJobTaskLog_jp"
---

指定されたCronトリガーのタスク実行ログを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCronJobTaskLog&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `ListCronJobTaskLog` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|JobName |String |はい |トリガー名。 |
|TaskId |String |はい |タスクID。 |
|Page |Integer |いいえ |ページ番号。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。デフォルトは50件。最大50件まで。 |
|OrderBy |Integer |いいえ |このパラメータはデータクエリの順序を指定します。以下の値を受け付けます：<br><br><br>* 1：降順でデータを並べ替えます。<br><br>* 2（デフォルト）：昇順でデータを並べ替えます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例値 |
|---|---|---|---|
|Logs |Object[] |タスク実行ログリスト。 | |
|Log |String |ログ内容。 |`Hello World` |
|Time |String |ログ時間。 |`2022-09-01T16:00:00Z` |
|TotalCount |Long |ログの総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCronJobTaskLog&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron1&TaskId=2xl2****&Page=1&Limit=10&OrderBy=2
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "20211207213413010225146063****",
        "Action": "ListCronJobTaskLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Logs": [
            {
                "Log": "Hello World",
                "Time": "2022-09-01T16:00:00Z"
            }
        ],
        "TotalCount": 1
    }
}
```


&nbsp;
