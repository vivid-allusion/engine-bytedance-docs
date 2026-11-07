---
title: "DescribeEdgeSummary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeSummary_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNが受信したユーザーからのリクエストに基づき、このAPIは1つのメトリックの集計データを統計します。

このAPIを呼び出すには、メトリック、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件（課金リージョンを含む）を指定してユーザーからのリクエストをフィルタリングすることもできます。最大で過去92日間のデータを照会できます。

データの安定性：ネットワークの変動の影響により、エッジノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。したがって、このAPIが返すメトリックデータは請求書に記載されている使用量ではなく、参照用です。実際の使用量については、請求書を参照してください。

データの適時性：メトリックデータには約5分の遅延が生じる可能性があります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計APIを初めて使用する場合は、まず以下のドキュメントを読むことをお勧めします。これにより、このAPIドキュメントの理解が深まります。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp">指標の定義と計算方法</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeEdgeSummary&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeEdgeSummaryです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Metric |String |はい |メトリックを表します。このパラメーターには次の値があります。<br><br><br>* `in_traffic`：ユーザーからCDNに転送されたデータ量（単位：バイト）。<br><br>* `in_bandwidth`：ユーザーからCDNに転送されたデータ量に基づいて計算された帯域幅のピーク値（単位：bps）。<br><br>* `out_traffic`：CDNからユーザーに転送されたデータ量（単位：バイト）。<br><br>* `out_bandwidth`：CDNからユーザーに転送されたデータ量に基づいて計算された帯域幅のピーク値（単位：bps）。<br><br>* `requests`：CDNが受信したユーザーからのリクエストの数。<br><br>* `dynamic_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすリクエストの数。<br><br>   * リクエストメソッドがGETでもHEADでもない。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `static_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすリクエストの数。<br><br>   * リクエストメソッドがGETまたはHEADである。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `qps`：CDNが受信したユーザーからのリクエストのQPSピーク値。<br><br>* `traffic_hitrate`：CDNのトラフィックヒット率を数値で示します。たとえば、`0.9999`は99.99%を表します。<br><br>* `response_time`：CDNがユーザーからのリクエストに応答するまでにかかった平均時間（単位：ミリ秒）。<br><br>* `avg_speed`：CDNがユーザーからのリクエストに応答するときの平均データ転送速度（単位：Bps）。このメトリックのデータは、応答ステータスコードが2xxのユーザーからのリクエストについて統計されます。<br><br>* `status_all`：CDNのユーザーからのリクエストへの応答において、このパラメーターは次のカテゴリのステータスコードの数を示します。<br><br>   * すべてのステータスコードの数。<br><br>   * 2xxステータスコードの数。<br><br>   * 3xxステータスコードの数。<br><br>   * 4xxステータスコードの数。<br><br>   * 5xxステータスコードの数。<br><br>   * 各ステータスコードの数。<br><br>* `status_2xx`：2xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_3xx`：3xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_4xx`：4xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_5xx`：5xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br><br>各メトリックの詳細と統計方法については、[指標の定義と計算方法](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp)を参照してください。 |`traffic` |
|StartTime |Long |はい |統計期間の開始時刻を表します。形式はUnixタイムスタンプで、精度は秒です。`StartTime`は`EndTime`以前である必要があります。また、`StartTime`と`EndTime`で表される統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻を表します。形式はUnixタイムスタンプで、精度は秒です。 |`1710836303` |
|Interval |String |いいえ |時間粒度を表します。このAPIは`Interval`に基づいて`StartTime`と`EndTime`で表される統計期間を一連の時間間隔に分割し、各時間間隔の`Metric`データを統計します。<br><br>`Interval`パラメーターを使用して統計期間を分割する方法については、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメーターには次の値があります。<br><br><br>* `1min`：時間粒度が1分であることを示します。<br><br>* `5min`：時間粒度が5分であることを示します。<br><br><br>指定できる時間粒度は、`StartTime`と`EndTime`で表される時間範囲の影響を受けます。<br><br><br>* 時間範囲が1日以内の場合、指定できる時間粒度は`1min`、`5min`です。<br><br>* 時間範囲が1日を超え31日以内の場合、指定できる時間粒度は`5min`のみです。<br><br><br>このパラメーターのデフォルト値は`5min`です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 |`5min` |
|Project |String |いいえ |プロジェクトを表します。<br><br><br>* `Domain`を指定した場合、APIは指定したすべてのドメイン名の`Metric`データを統計します。<br><br>* `Project`を指定し、`Domain`を指定しなかった場合、APIは指定したプロジェクトの`Metric`データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63630#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95)を参照してください。<br><br>* `Project`も`Domain`も指定しなかった場合、APIはすべてのドメイン名の`Metric`データを統計します。 |`my_project` |
|Domain |String |いいえ |1つまたは複数のドメイン名を表し、ユーザーからのリクエストをフィルタリングするために使用されます。このAPIは、指定した各ドメイン名の`Metric`データを統計します。最大50個のドメイン名を指定できます。複数のドメイン名はコンマ（,）で区切ります。`Domain`を指定しない場合、このパラメーターを使用してリクエストをフィルタリングしないことを示します。<br><br>`Project`を指定した場合、指定したドメイン名はその`Project`に属している必要があります。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出すときは、次の点に注意してください。<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)を呼び出して、アクセス権のあるドメイン名を取得できます。<br><br>* このパラメーターを指定しない場合、IAMユーザーがアクセス権を持つすべてのドメイン名を表します。 |`www.example.com,www.test.com,img.example.com` |
|BillingRegion |String |いいえ |1つまたは複数の課金リージョンを表し、ユーザーからのリクエストをフィルタリングするために使用されます。このAPIは、これらの課金リージョンからのユーザーからのリクエストの`Metric`データを統計します。複数の課金リージョンはコンマ（,）で区切ります。このパラメーターには次の値があります。<br><br><br>* `CHN`：中国本土を表します。<br><br>* `EU`：ヨーロッパを表します。<br><br>* `NA`：北米を表します。<br><br>* `SA`：南米を表します。<br><br>* `MEA`：中東およびアフリカを表します。<br><br>* `AP1`：アジア太平洋リージョン1を表します。<br><br>* `AP2`：アジア太平洋リージョン2を表します。<br><br>* `AP3`：アジア太平洋リージョン3を表します。<br><br><br>`BillingRegion`を指定しない場合、このパラメーターを使用してリクエストをフィルタリングしないことを示します。 |`CHN,EU` |


<span id="プロジェクトデータの統計方法"></span>
### プロジェクトデータの統計方法

プロジェクトのメトリックデータを統計する場合、CDNはプロジェクト内のドメイン名のデータを統計します。


* 統計期間中にドメイン名がプロジェクトから転出された場合、プロジェクトのメトリックデータには転出後のドメイン名のデータは含まれません。

* 統計期間中にドメイン名がプロジェクトに転入された場合、プロジェクトのメトリックデータには転入後のドメイン名のデータが含まれます。


**例**

次のシナリオを考えます。


* 指定した統計期間は、ある日の8:00～10:00です。

* ドメイン名Xは9:00に別のプロジェクトからプロジェクトAに移行されました。ドメイン名YはずっとプロジェクトAにあります。


このシナリオでプロジェクトAのメトリックデータを統計する場合、メトリックデータには次のものが含まれます。


* ドメイン名Xの9:00から10:00までのメトリックデータ。

* ドメイン名Yの8:00から10:00までのメトリックデータ。


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|MetricDataList |Object[] |このAPIが返す結果データを表します。 | |
|Metric |String |リクエストパラメーター`Metric`で指定されたメトリックを表します。 |`traffic` |
|Value |Double |集計後の`Metric`データを表します。 |`3475788` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeSummary&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "bandwidth",
    "Project": "my_project",
    "BillingRegion": "CHN,EU"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423065708E622246DA96029C147AF",
        "Action": "DescribeEdgeSummary",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "Metric": "out_traffic",
                "Value": 75637256964.5
            }
        ]
    }
}
```


&nbsp;
