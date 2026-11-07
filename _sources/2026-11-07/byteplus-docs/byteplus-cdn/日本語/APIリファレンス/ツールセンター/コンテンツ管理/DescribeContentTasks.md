---
title: "DescribeContentTasks"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeContentTasks_jp"
---

過去7日間に送信されたパージまたはプリフェッチタスクを取得し、これらのタスク内の各URLに細分します。返される結果は、各URLタスクの詳細（タスクの実行結果を含む）を示します。複数のフィルタオプションを使用して、URLタスクリストをフィルタリングできます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeContentTasksです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Url |String |いいえ |1つまたは複数のURLを表し、これらのURLのタスクを取得します。複数のURLは`\n`で区切ります。<br><br>このパラメータを指定しない場合、このパラメータを使用してタスクリストをフィルタリングしません。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg`<br><br> |
|DomainName |String |いいえ |1つのドメイン名を表します。このドメイン名を含むURLについて、これらのURLのタスクを取得します。<br><br>このパラメータを指定しない場合、このパラメータを使用してタスクリストをフィルタリングしません。 |`www.example.com` |
|TaskID |String |いいえ |1つのタスクIDを表し、このIDのすべてのURLタスクを取得します。<br><br>このパラメータを指定しない場合、このパラメータを使用してタスクリストをフィルタリングしません。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031`<br><br> |
|TaskType |String |はい |1つのタスクタイプを表し、このタイプのすべてのURLタスクを取得します。このパラメータには以下の値があります：<br><br><br>* `refresh_file`：URLパージタスクを表します。<br><br>* `refresh_dir`：ディレクトリパージタスクを表します。<br><br>* `preload`：URLプリフェッチタスクを表します。 |`preload` |
|Status |String |いいえ |1つのタスクステータスを表し、このステータスのすべてのURLタスクを取得します。このパラメータには以下の値があります：<br><br><br>* `complete`：完了したタスクを表します。<br><br>* `running`：実行中のタスクを表します。<br><br>* `failed`：実行に失敗したタスクを表します。<br><br><br>このパラメータを指定しない場合、このパラメータを使用してタスクリストをフィルタリングしません。 |`complete` |
|StartTime |Long |いいえ |開始時刻を表し、Unixタイムスタンプ形式で、送信時刻がこの時刻以降または等しいURLタスクを取得します。留意点として、7日前に送信されたURLタスクは照会できません。<br><br>`StartTime`と`EndTime`の両方を同時に指定するか、または両方のパラメータを指定しない必要があります。両方のパラメータを指定しない場合、過去7日間に送信されたURLタスクを取得します。 |`1641844915` |
|EndTime |Long |いいえ |終了時刻を表し、Unixタイムスタンプ形式で、送信時刻がこの時刻以前または等しいURLタスクを取得します。 |`1641845373` |
|PageNum |Long |いいえ |ページ番号を表し、このページ上のURLタスクを取得します。このパラメータのデフォルト値は`1`です。<br><br>CDNは、フィルタ条件に一致するURLタスクをページ分割します。応答本文の`Total`および`PageSize`パラメータの値に基づいてページ数を計算できます。 |`1` |
|PageSize |Long |いいえ |1ページに含まれるURLタスクの数を表します。このパラメータの値の範囲は1\-1000で、デフォルト値は`50`です。 |`10` |
|UrlList |String[] |いいえ |照会URLリストで、Urlより優先度が高いです | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Total |Long |フィルタ条件に一致するURLタスクの総数を表します。 |`2` |
|PageNum |Long |レスポンス本文の`PageNum`を表します。 |`1` |
|PageSize |Long |レスポンス本文の`PageSize`を表します。 |`100` |
|Data |Object[] |`PageNum`上のURLタスクリストを表します。`PageNum`で示されるページ番号が存在しないか、そのページにタスクがない場合、このパラメータの値は`null`です。 | |
|Url |String |リスト内の1つのURLタスクが操作するURLを表します。 |`https://www.example.com/1.jpg`<br><br> |
|Status |String |このURLタスクのステータスを表します。このパラメータには以下の値があります：<br><br><br>* `complete`：タスクが完了したことを表します。<br><br>* `running`：タスクが実行中であることを表します。<br><br>* `failed`：タスクの実行に失敗したことを表します。 |`complete` |
|TaskType |String |このURLタスクのタイプを表します。このパラメータには以下の値があります：<br><br><br>* `refresh_file`：URLパージタスクを表します。<br><br>* `refresh_dir`：ディレクトリパージタスクを表します。<br><br>* `preload`：URLプリフェッチタスクを表します。 |`preload` |
|RefreshPrefix |Boolean |このURLタスクに"プレフィックスパージ"という設定があるかどうかを表します。`TaskType`が`refresh_dir`の場合にのみ、このパラメータは有効です。このパラメータには以下の値があります：<br><br><br>* `true`：このタスクにこの設定があることを表します。<br><br>* `false`：このタスクにこの設定がないことを表します。<br><br><br>`TaskType`が`refresh_dir`でない場合、このパラメータの値は常に`false`です。 |`true` |
|CreateTime |Long |このURLタスクの送信時刻を表し、Unixタイムスタンプ形式です。 |`1601371409` |
|TaskID |String |このURLタスクのIDを表します。 |`url_block_2021112616560901001104903915206` |
|Process |String |このURLタスクの進捗をパーセンテージで表します。 |`70%` |
|Remark |String |このURLタスクが失敗した理由を表します。このパラメータは`Status`が`failed`の場合にのみ有効です。`Status`が`failed`でない場合、`Remark`の値は常に空("")です。 |`origin_error`<br><br> |
|StatusCode |Long |オリジンサーバーの異常ステータスコード | |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021-03-01
{
    "StartTime": 1625587200,
    "EndTime": 1625673600,
    "TaskType": "preload",
    "PageSize": 10,
    "PageNum": 1
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202406301133492C6A5B1ABB315058A120",
        "Action": "DescribeContentTasks",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "origin_error",
                "Status": "failed",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/2.txt"
            },
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "",
                "Status": "complete",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/1.txt"
            }
        ],
        "PageNum": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
