---
title: "DescribeContentQuota"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeContentQuota_jp"
---

BytePlusアカウントの1日あたりのパージおよびプリフェッチタスクのクォータとクォータ残量を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeContentQuotaです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|BlockLimit |Long |1回あたりにブロックできる最大URL数を示します。 |`100` |
|BlockQuota |Long |1日あたりにブロックできるURL数を示します。 |`3000` |
|BlockRemain |Long |本日ブロックできるURLの残り数を示します。 |`3000` |
|PreloadLimit |Long |1回あたりにプリフェッチできる最大URL数を示します。 |`100` |
|PreloadQuota |Long |1日あたりにプリフェッチできるURL数を示します。 |`1000` |
|PreloadRemain |Long |本日プリフェッチできるURLの残り数を示します。 |`10` |
|RefreshDirLimit |Long |1回あたりにパージできる最大ディレクトリ数を示します。 |`100` |
|RefreshDirQuota |Long |1日あたりにパージできるディレクトリ数を示します。 |`50` |
|RefreshDirRemain |Long |本日パージできるディレクトリの残り数を示します。 |`15` |
|RefreshQuota |Long |1日あたりにパージできるURL数を示します。 |`1000` |
|RefreshQuotaLimit |Long |1回あたりにパージできる最大URL数を示します。 |`100` |
|RefreshRegexLimit |Long |1回あたりに正規表現でパージできる最大URL数を示します。 |`10` |
|RefreshRegexQuota |Long |1日あたりに正規表現でパージできるURL数を示します。 |`20` |
|RefreshRegexRemain |Long |本日正規表現でパージできるURLの残り数を示します。 |`2` |
|RefreshRemain |Long |本日パージできるURLの残り数を示します。 |`200` |
|UnblockLimit |Long |1回あたりにブロック解除できる最大URL数を示します。 |`100` |
|UnblockQuota |Long |1日あたりにブロック解除できるURL数を示します。 |`3000` |
|UnblockRemain |Long |本日ブロック解除できるURLの残り数を示します。 |`3000` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentQuota&Version=2021-03-01
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202310271225559FCEDC662FFE48246DCB",
        "Action": "DescribeContentQuota",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PreloadLimit": 100,
        "PreloadQuota": 1000,
        "PreloadRemain": 1000,
        "RefreshDirLimit": 100,
        "RefreshDirQuota": 50,
        "RefreshDirRemain": 50,
        "RefreshQuota": 10000,
        "RefreshQuotaLimit": 100,
        "RefreshRemain": 1000
    }
}
```


&nbsp;
