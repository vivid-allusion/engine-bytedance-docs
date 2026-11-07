---
title: "DescribeOriginStatusCodeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginStatusCodeRanking_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNがオリジンサーバーから受信した応答ステータスコードに基づき、このAPIはドメイン名ごとに一連のメトリックデータを集計し、これらの集計データを降順にソートします。

このAPIを呼び出すには、ステータスコードメトリック、統計期間、および時間粒度を指定する必要があります。また、オリジンリクエストをフィルタリングするために複数のフィルタリング条件を指定することもできます。最大で過去92日間のデータを照会できます。

データの安定性：ネットワークの変動により、リージョナルノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。

データの適時性：メトリックデータには約5分の遅延が生じる場合があります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計APIを初めて使用する場合は、まず以下のドキュメントを読むことを強くお勧めします。これにより、このAPIドキュメントの理解が深まります。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeOriginStatusCodeRanking&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeOriginStatusCodeRankingです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Item |String |はい |グループ化条件を表します。現在、このパラメータ値は`domain`のみ可能で、`Domain`に従って`Metric`データを集計することを表します。 |`domain` |
|Metric |String |はい |CDNが受信したオリジンサーバーの応答について、このパラメータは次のいずれかのカテゴリのステータスコードの数を表します：<br><br><br>* `status_2xx`：2xxステータスコードの数を表します。<br><br>* `status_3xx`：3xxステータスコードの数を表します。<br><br>* `status_4xx`：4xxステータスコードの数を表します。<br><br>* `status_5xx`：5xxステータスコードの数を表します。 |`status_4xx` |
|StartTime |Long |はい |統計期間の開始時刻をUnixタイムスタンプ（秒精度）で表します。`StartTime`は`EndTime`以前である必要があります。また、`StartTime`と`EndTime`で表される統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻をUnixタイムスタンプ（秒精度）で表します。 |`1710836303` |
|Interval |String |いいえ |時間粒度を表します。このAPIは、`Interval`に基づいて`StartTime`と`EndTime`で表される統計期間を一連の時間間隔に分割し、各時間間隔の`Metric`データを統計します。<br><br>`Interval`パラメータが統計期間をどのように分割するために使用されるかについては、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメータには次の値があります：<br><br><br>* `1min`：時間粒度が1分であることを表します。<br><br>* `5min`：時間粒度が5分であることを表します。<br><br><br>指定できる時間粒度は、`StartTime`と`EndTime`で表される時間範囲の影響を受けます。<br><br><br>* 時間範囲が1日以内の場合、指定できる時間粒度は`1min`、`5min`です。<br><br>* 時間範囲が1日を超え31日以内の場合、指定できる時間粒度は`5min`のみです。<br><br><br>このパラメータのデフォルト値は`5min`です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 | |
|Project |String |いいえ |プロジェクトを表します。<br><br><br>* `Domain`を指定した場合、APIは指定されたすべてのドメイン名の`Metric`データを統計します。<br><br>* `Project`を指定し、`Domain`を指定しない場合、APIは指定されたプロジェクトの`Metric`データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63628#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95)を参照してください。<br><br>* `Project`も`Domain`も指定しない場合、APIはすべてのドメイン名の`Metric`データを統計します。 |`my_project` |
|Domain |String |いいえ |ユーザーからのリクエストをフィルタリングするための1つ以上のドメイン名を表します。APIは指定された各ドメイン名の`Metric`データを統計します。最大50個のドメイン名を指定できます。複数のドメイン名はカンマ（,）で区切ります。`Domain`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしません。<br><br>`Project`を指定した場合、指定するドメイン名はその`Project`に属している必要があります。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出す場合、次の点に注意してください：<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)を呼び出して、アクセス権のあるドメイン名を取得できます。<br><br>* このパラメータを指定しない場合、IAMユーザーがアクセス権を持つすべてのドメイン名を表します。 |`www.example.com,www.test.com,img.example.com` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Item |String |リクエストパラメータ`Item`で指定されたグループ化条件を表します。 |`domain` |
|Metric |String |リクエストパラメータ`Metric`で指定されたメトリックを表します。 |`status_4xx` |
|TopDataDetails |Object[] |`Item`によって集計された`Metric`データの詳細を含むデータオブジェクトのセットを表します。各データオブジェクトには、各カテゴリのステータスコードの数と割合が含まれます。これらのデータオブジェクトは、指定された`Metric`の降順にソートされます。 | |
|ItemKey |String |`Domain`リスト内のドメイン名を表します。 |`www.example.com` |
|Status2xx |Double |この`ItemKey`について、2xxステータスコードの数を表します。 |`45678` |
|Status2xxRatio |Double |この`ItemKey`について、2xxステータスコードの数の割合を表します。 |`0.47` |
|Status3xx |Double |この`ItemKey`について、3xxステータスコードの数を表します。 |`0` |
|Status3xxRatio |Double |この`ItemKey`について、3xxステータスコードの数の割合を表します。 |`0` |
|Status4xx |Double |この`ItemKey`について、4xxステータスコードの数を表します。 |`3` |
|Status4xxRatio |Double |この`ItemKey`について、4xxステータスコードの数の割合を表します。 |`0.0001` |
|Status5xx |Double |この`ItemKey`について、5xxステータスコードの数を表します。 |`0` |
|Status5xxRatio |Double |この`ItemKey`について、5xxステータスコードの数の割合を表します。 |`0` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeOriginStatusCodeRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Metric": "status_2xx",
    "Item": "domain",
    "Project": "my_project",
    "Domain": "www.example.com,www.test.com,img.example.com"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403200014241036C312826267DE2108",
        "Action": "DescribeOriginStatusCodeRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "Metric": "status_2xx",
        "TopDataDetails": [
            {
                "ItemKey": "www.example.com",
                "Status2xx": 2933327,
                "Status2xxRatio": 0.814,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 0,
                "Status4xxRatio": 0,
                "Status5xx": 0,
                "Status5xxRatio": 0
            },
            {
                "ItemKey": "www.test.com",
                "Status2xx": 635508,
                "Status2xxRatio": 0.1764,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 80665,
                "Status4xxRatio": 0.3138,
                "Status5xx": 185105,
                "Status5xxRatio": 1
            },
            {
                "ItemKey": "img.example.com",
                "Status2xx": 8153,
                "Status2xxRatio": 0.0023,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 0,
                "Status4xxRatio": 0,
                "Status5xx": 0,
                "Status5xxRatio": 0
            }
        ]
    }
}
```


&nbsp;
