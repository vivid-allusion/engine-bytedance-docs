---
title: "DescribeOriginData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginData_jp"
---

<span id="api-説明"></span>
## API 説明

CDN がオリジンサーバーに送信するリクエスト（オリジンリクエスト）に基づき、この API は、指定されたメトリックの各時点における内訳データを統計します。

この API を呼び出すには、メトリック、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件を指定して、オリジンリクエストをフィルタリングすることもできます。過去 92 日間のデータを照会できます。

データの安定性：ネットワークの変動により、リージョナルノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは 12 時間以内に徐々に安定します。したがって、この API が返すメトリックデータは、請求書に表示される使用量ではなく、参照用です。実際の使用量については、請求書を参照してください。

データの適時性：メトリックデータには約 5 分の遅延がある場合があります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計 API を初めて使用する場合は、この API ドキュメントを理解するのに役立つため、まず次のドキュメントをお読みください。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp">指標の定義と計算方法</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1 秒あたり最大 20 件の API リクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeOriginData&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeOriginDataです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Metric |String |はい |メトリックを表します。このパラメータには次の値があります。<br><br><br>* `in_traffic`：オリジンサーバーから CDN に転送されるデータ量（単位：バイト）。<br><br>* `in_bandwidth`：オリジンサーバーから CDN に転送されるデータ量に基づいて計算された帯域幅（単位：bps）。<br><br>* `out_traffic`：CDN からオリジンサーバーに転送されるデータ量（単位：バイト）。<br><br>* `out_bandwidth`：CDN からオリジンサーバーに転送されるデータ量に基づいて計算された帯域幅（単位：bps）。<br><br>* `requests`：オリジンリクエストの数。<br><br>* `qps`：オリジンリクエストの QPS。<br><br>* `response_time`：CDN がオリジンサーバーの応答を受信するのにかかった時間（単位：ミリ秒）。<br><br>* `status_all`：CDN が受信したオリジンサーバーの応答において、このパラメータは次のカテゴリのステータスコードの数を表します。<br><br>   * すべてのステータスコードの数。<br><br>   * すべての 2xx ステータスコードの数。<br><br>   * すべての 3xx ステータスコードの数。<br><br>   * すべての 4xx ステータスコードの数。<br><br>   * すべての 5xx ステータスコードの数。<br><br>   * 各ステータスコードの数。<br><br>* `status_2xx`：すべての 2xx ステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_3xx`：すべての 3xx ステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_4xx`：すべての 4xx ステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_5xx`：すべての 5xx ステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br><br>各メトリックの詳細と統計方法については、[指標の定義と計算方法](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp) を参照してください。 |`traffic` |
|StartTime |Long |はい |統計期間の開始時刻を表します。形式は Unix タイムスタンプで、精度は秒です。`StartTime` は `EndTime` より前または同じである必要があります。また、`StartTime` と `EndTime` で表される統計期間は 31 日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻を表します。形式は Unix タイムスタンプで、精度は秒です。 |`1710836303` |
|Interval |String |いいえ |時間粒度を表します。この API は、`Interval` に基づいて `StartTime` と `EndTime` で表される統計期間を一連の時間間隔に分割し、各時間間隔の `Metric` データを統計します。<br><br>`Interva` パラメータが統計期間を分割する方法については、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp) を参照してください。<br><br>このパラメータには次の値があります。<br><br><br>* `1min`：時間粒度が 1 分であることを示します。<br><br>* `5min`：時間粒度が 5 分であることを示します。<br><br>* `hour`：時間粒度が 1 時間であることを示します。<br><br>* `day`：時間粒度が 1 日であることを示します。<br><br><br>指定できる時間粒度は、`StartTime` と `EndTime` で表される時間範囲の影響を受けます。<br><br><br>* 時間範囲が 1 日以下の場合、指定できる時間粒度は `1min`、`5min`、`hour` です。<br><br>* 1 日 < 時間範囲 <= 3 日の場合、指定できる時間粒度は `5min`、`hour`、`day` です。<br><br>* 3 日 < 時間範囲 <= 31 日の場合、指定できる時間粒度は `hour`、`day` です。<br><br><br>このパラメータのデフォルト値は `5min` です。デフォルト値が時間範囲と一致しない場合、API リクエストは失敗します。 |`hour` |
|Project |String |いいえ |プロジェクトを表します。<br><br><br>* `Domain` を指定した場合、API は指定したすべてのドメイン名の `Metric` データを統計します。<br><br>* `Project` を指定し、`Domain` を指定しなかった場合、API は指定したプロジェクトの `Metric` データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63623#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95) を参照してください。<br><br>* `Project` も `Domain` も指定しなかった場合、API はすべてのドメイン名の `Metric` データを統計します。 |`my_project` |
|Domain |String |いいえ |1 つ以上のドメイン名を表し、ユーザーからのリクエストをフィルタリングするために使用されます。API は、指定した各ドメイン名の `Metric` データを統計します。最大 50 個のドメイン名を指定できます。複数のドメイン名はコンマ（,）で区切ります。`Domain` を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br>`Project` を指定した場合、指定したドメイン名はその `Project` に属している必要があります。<br><br>说明<br><br>IAMユーザーがこの API を呼び出すときは、次の点に注意してください。<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp) を呼び出して、アクセス権のあるドメイン名を取得できます。<br><br>* このパラメータを指定しない場合、IAMユーザーがアクセス権を持つすべてのドメイン名を表します。 |`www.example.com,www.test.com,img.example.com` |


<span id="プロジェクトデータの統計方法"></span>
### プロジェクトデータの統計方法

プロジェクトのメトリックデータを統計する場合、CDN はプロジェクト内のドメイン名のデータを統計します。


* 統計期間中にドメイン名がプロジェクトから転出された場合、プロジェクトのメトリックデータには、転出後のドメイン名のデータは含まれません。

* 統計期間中にドメイン名がプロジェクトに転入された場合、プロジェクトのメトリックデータには、転入後のドメイン名のデータが含まれます。


**例**

次のシナリオを検討してください。


* 指定した統計期間は、ある日の 8:00～10:00 です。

* ドメイン名 X は 9:00 に別のプロジェクトからプロジェクト A に移行されました。ドメイン名 Y は常にプロジェクト A にあります。


このシナリオでは、プロジェクト A のメトリックデータを統計する場合、メトリックデータには次のものが含まれます。


* 9:00～10:00 のドメイン名 X のメトリックデータ。

* 8:00～10:00 のドメイン名 Y のメトリックデータ。


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|MetricDataList |Object[] |この API が返す結果データを表します。 | |
|Metric |String |リクエストパラメータ `Metric` で指定されたメトリックを表します。 |`traffic` |
|Values |Object[] |`Interval` に基づいて統計された `Metric` データオブジェクトのセットを表します。 | |
|TimeStamp |Long |`Value` に対応する時間間隔の開始時刻を表します。形式は Unix タイムスタンプで、精度は秒です。[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp) を参照してください。 |`1710273600` |
|Value |Double |`Metric` の内訳データを表します。 |`4568` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeOriginData&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "day",
    "Metric": "out_traffic",
    "Project": "my_project"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404230658256DB1CC6291C10133A8C6",
        "Action": "DescribeOriginData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "Metric": "out_traffic",
                "Values": [
                    {
                        "TimeStamp": 1710201600,
                        "Value": 3889061
                    },
                    {
                        "TimeStamp": 1710288000,
                        "Value": 3968016
                    },
                    {
                        "TimeStamp": 1710374400,
                        "Value": 3202556
                    },
                    {
                        "TimeStamp": 1710460800,
                        "Value": 3347793
                    },
                    {
                        "TimeStamp": 1710547200,
                        "Value": 1572368
                    },
                    {
                        "TimeStamp": 1710633600,
                        "Value": 1771534
                    },
                    {
                        "TimeStamp": 1710720000,
                        "Value": 2932340
                    },
                    {
                        "TimeStamp": 1710806400,
                        "Value": 4164708
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
