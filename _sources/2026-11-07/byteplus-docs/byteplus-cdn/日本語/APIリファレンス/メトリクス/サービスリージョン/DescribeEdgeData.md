---
title: "DescribeEdgeData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeData_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNが受信したユーザーからのリクエストに基づき、このAPIは、あるメトリックについて、各時点におけるメトリックの内訳データを統計します。

このAPIを呼び出すには、メトリック、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件（課金リージョンを含む）を指定して、ユーザーからのリクエストをフィルタリングすることもできます。さらに、このAPIは課金リージョンをフィルタリング条件として指定することをサポートしています。最大で過去92日間のデータを照会できます。

データの安定性：ネットワークの変動の影響により、エッジノードで統計されたメトリックデータが変化する可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。したがって、このAPIが返すメトリックデータは、請求書に表示される使用量ではなく、参考用です。実際の使用量は請求書を基準にしてください。

データの適時性：メトリックデータには5分程度の遅延が生じる可能性があります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計のAPIを初めて使用する場合は、まず以下のドキュメントを読むことを強くお勧めします。これは、このAPIドキュメントを理解するのに役立ちます。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp">指標の定義と計算方法</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeEdgeData&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeEdgeDataです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Metric |String |はい |メトリックを表します。このパラメータには次の値があります。<br><br><br>* `in_traffic`：ユーザーがCDNに転送したデータ量（単位：バイト）。<br><br>* `in_bandwidth`：ユーザーがCDNに転送したデータ量に基づいて計算された帯域幅（単位：bps）。<br><br>* `out_traffic`：CDNがユーザーに転送したデータ量（単位：バイト）。<br><br>* `out_bandwidth`：CDNがユーザーに転送したデータ量に基づいて計算された帯域幅（単位：bps）。<br><br>* `requests`：CDNが受信したすべてのユーザーからのリクエストの数。<br><br>* `dynamic_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>   * リクエストメソッドがGETでもHEADでもない。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `static_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>   * リクエストメソッドがGETまたはHEADである。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `qps`：CDNが受信したユーザーからのリクエストのQPS。<br><br>* `traffic_hitrate`：トラフィックヒット率を数値で表示します。たとえば、`0.9999`は99.99%を表します。<br><br>* `response_time`：CDNがユーザーからのリクエストに応答するのにかかった平均時間（単位：ミリ秒）。<br><br>* `avg_speed`：CDNがユーザーからのリクエストに応答するときの平均データ転送速度（単位：Bps）。このメトリックのデータは、応答ステータスコードが2xxのユーザーからのリクエストについて統計されます。<br><br>* `status_all`：CDNのユーザーからのリクエストへの応答において、このパラメータは次のカテゴリのステータスコードの数を表します。<br><br>   * すべてのステータスコードの数。<br><br>   * 2xxステータスコードの数。<br><br>   * 3xxステータスコードの数。<br><br>   * 4xxステータスコードの数。<br><br>   * 5xxステータスコードの数。<br><br>   * 各ステータスコードの数。<br><br>* `status_2xx`：2xxステータスコードの数と、このカテゴリの各ステータスコードの数を表します。<br><br>* `status_3xx`：3xxステータスコードの数と、このカテゴリの各ステータスコードの数を表します。<br><br>* `status_4xx`：4xxステータスコードの数と、このカテゴリの各ステータスコードの数を表します。<br><br>* `status_5xx`：5xxステータスコードの数と、このカテゴリの各ステータスコードの数を表します。<br><br><br>各メトリックの詳細と統計方法については、[指標の定義と計算方法](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp)を参照してください。 |`traffic` |
|StartTime |Long |はい |統計期間の開始時刻を表します。形式はUnixタイムスタンプで、精度は秒です。`StartTime`は`EndTime`より前または同じでなければなりません。また、`StartTime`と`EndTime`が表す統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻を表します。形式はUnixタイムスタンプで、精度は秒です。 |`1710836303` |
|Interval |String |いいえ |時間粒度を表します。このAPIは、`Interval`に基づいて`StartTime`と`EndTime`が表す統計期間を一連の時間間隔に分割し、各時間間隔の`Metric`データを統計します。<br><br>`Interval`パラメータが統計期間を分割する方法については、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメータには次の値があります。<br><br><br>* `1min`：時間粒度が1分であることを示します。<br><br>* `5min`：時間粒度が5分であることを示します。<br><br>* `hour`：時間粒度が1時間であることを示します。<br><br>* `day`：時間粒度が1日であることを示します。<br><br><br>指定できる時間粒度は、`StartTime`と`EndTime`が表す時間範囲の影響を受けます。<br><br><br>* 時間範囲が1日以下の場合、指定できる時間粒度には`1min`、`5min`、`hour`があります。<br><br>* 1日 < 時間範囲 <= 3日の場合、指定できる時間粒度には`5min`、`hour`、`day`があります。<br><br>* 3日 < 時間範囲 <= 31日の場合、指定できる時間粒度には`hour`、`day`があります。<br><br><br>このパラメータのデフォルト値は`5min`です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 |`hour` |
|Project |String |いいえ |プロジェクトを表します。<br><br><br>* `Domain`を指定した場合、このAPIは指定したすべてのドメインの`Metric`データを統計します。<br><br>* `Project`を指定し、`Domain`を指定しなかった場合、このAPIは指定したプロジェクトの`Metric`データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63629#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95)を参照してください。<br><br>* `Project`も`Domain`も指定しなかった場合、このAPIはすべてのドメインの`Metric`データを統計します。 |`my_project` |
|Domain |String |いいえ |1つ以上のドメイン名を表し、ユーザーからのリクエストのフィルタリングに使用されます。このAPIは、指定した各ドメインの`Metric`データを統計します。最大50個のドメインを指定できます。複数のドメイン名はカンマ（,）で区切ります。`Domain`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br>`Project`を指定した場合、指定したドメイン名はその`Project`に属している必要があります。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出すときは、次の点に注意してください。<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)を呼び出して、アクセス権のあるドメインを取得できます。<br><br>* このパラメータを指定しない場合、そのIAMユーザーがアクセス権を持つすべてのドメイン名を意味します。 |`www.example.com,www.test.com,img.example.com` |
|BillingRegion |String |いいえ |1つ以上の課金リージョンを表し、ユーザーからのリクエストのフィルタリングに使用されます。このAPIは、これらの課金リージョンからのユーザーからのリクエストの`Metric`データを統計します。複数の課金リージョンはカンマ（,）で区切ります。このパラメータには次の値があります。<br><br><br>* `CHN`：中国本土を表します。<br><br>* `EU`：ヨーロッパを表します。<br><br>* `NA`：北米を表します。<br><br>* `SA`：南米を表します。<br><br>* `MEA`：中東およびアフリカを表します。<br><br>* `AP1`：アジア太平洋リージョン1を表します。<br><br>* `AP2`：アジア太平洋リージョン2を表します。<br><br>* `AP3`：アジア太平洋リージョン3を表します。<br><br><br>`BillingRegion`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。 |`CHN,EU` |


<span id="プロジェクトデータの統計方法"></span>
### プロジェクトデータの統計方法

プロジェクトのメトリックデータを統計する場合、CDNはプロジェクト内のドメインのデータを統計します。


* 統計期間内にドメインがプロジェクトから転出された場合、そのプロジェクトのメトリックデータには、転出後のそのドメインのデータは含まれません。

* 統計期間内にドメインがプロジェクトに転入された場合、そのプロジェクトのメトリックデータには、転入後のそのドメインのデータが含まれます。


**例**

次のシナリオを考えます。


* 指定した統計期間は、ある日の8:00～10:00です。

* ドメインXは9:00に別のプロジェクトからプロジェクトAに移動しました。ドメインYはずっとプロジェクトAにあります。


このシナリオでは、プロジェクトAのメトリックデータを統計する場合、メトリックデータには以下が含まれます。


* ドメインXの9:00から10:00までのメトリックデータ。

* ドメインYの8:00から10:00までのメトリックデータ。


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|MetricDataList |Object[] |このAPIが返す結果データを表します。 | |
|Metric |String |リクエストパラメータ`Metric`で指定されたメトリックを表します。 |`traffic` |
|Values |Object[] |`Interval`に基づいて統計された`Metric`データオブジェクトのセットを表します。 | |
|TimeStamp |Long |`Value`に対応する時間間隔の開始時刻を表します。形式はUnixタイムスタンプで、精度は秒です。[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。 |`1710273600` |
|Value |Double |`Metric`の内訳データを表します。 |`4567` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeData&Version=2021-03-01
```


&nbsp;
