---
title: "DescribeDistrictSummary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictSummary_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNが受信したユーザーからのリクエストに基づき、このAPIは1つのメトリックの集計データを統計します。

このAPIを呼び出すには、メトリック、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件を指定してユーザーからのリクエストをフィルタリングすることもできます。最大で過去92日間のデータをクエリできます。

データの安定性：ネットワークの変動により、エッジノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。したがって、このAPIが返すメトリックデータは請求書に表示される使用量ではなく、参照用です。実際の使用量については、請求書を参照してください。

データの適時性：メトリックデータには約5分間の遅延が生じる可能性があります。

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

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeDistrictSummary&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeDistrictSummaryです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Metric |String |はい |メトリックを示します。このパラメータには次の値があります：<br><br><br>* `in_traffic`：ユーザーがCDNに送信したデータ量（バイト単位）。<br><br>* `in_bandwidth`：ユーザーがCDNに送信したデータ量に基づいて計算された帯域幅のピーク値（bps単位）。<br><br>* `out_traffic`：CDNがユーザーに送信したデータ量（バイト単位）。<br><br>* `out_bandwidth`：CDNがユーザーに送信したデータ量に基づいて計算された帯域幅のピーク値（bps単位）。<br><br>* `requests`：CDNが受信したユーザーからのリクエストの数。<br><br>* `dynamic_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>   * リクエストメソッドがGETでもHEADでもない。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `static_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>   * リクエストメソッドがGETまたはHEADである。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `qps`：CDNが受信したユーザーからのリクエストのQPSのピーク値。<br><br>* `response_time`：CDNがユーザーからのリクエストに応答するのにかかった平均時間（ミリ秒単位）。<br><br>* `avg_speed`：CDNがユーザーからのリクエストに応答するときの平均データ転送速度（Bps単位）。このメトリックのデータは、応答ステータスコードが2xxのユーザーからのリクエストについて統計されます。<br><br>* `status_all`：CDNのユーザーからのリクエストへの応答において、このパラメータは次のカテゴリのステータスコードの数を示します：<br><br>   * すべてのステータスコードの数。<br><br>   * 2xxステータスコードの数。<br><br>   * 3xxステータスコードの数。<br><br>   * 4xxステータスコードの数。<br><br>   * 5xxステータスコードの数。<br><br>   * 各ステータスコードの数。<br><br>* `status_2xx`：2xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_3xx`：3xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_4xx`：4xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br>* `status_5xx`：5xxステータスコードの数と、このカテゴリの各ステータスコードの数。<br><br><br>各メトリックの詳細と統計方法については、[指標の定義と計算方法](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp)を参照してください。<br><br>说明<br><br>`Metric`を`response_time`または`avg_speed`に指定する場合は、必ず`Protocol`を指定してください。`Protocol`パラメータの説明を参照してください。 |`traffic` |
|StartTime |Long |はい |統計期間の開始時刻をUnixタイムスタンプ（秒単位）で示します。`StartTime`は`EndTime`以前である必要があります。また、`StartTime`と`EndTime`で示される統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻をUnixタイムスタンプ（秒単位）で示します。 |`1710836303` |
|Interval |String |いいえ |時間粒度を示します。このAPIは、`Interval`に基づいて`StartTime`と`EndTime`で示される統計期間を一連の時間間隔に分割し、各時間間隔の`Metric`データを統計します。<br><br>`Interval`パラメータが統計期間をどのように分割するために使用されるかについては、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメータには次の値があります：<br><br><br>* `1min`：時間粒度が1分であることを示します。<br><br>* `5min`：時間粒度が5分であることを示します。<br><br><br>指定できる時間粒度は、`StartTime`と`EndTime`で示される時間範囲の影響を受けます。<br><br><br>* 時間範囲が1日以下の場合、指定できる時間粒度は`1min`、`5min`です。<br><br>* 時間範囲が1日を超え31日以下の場合、指定できる時間粒度は`5min`のみです。<br><br><br>このパラメータのデフォルト値は`5min`です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 |`5min` |
|Project |String |いいえ |プロジェクトを示します。<br><br><br>* `Domain`を指定した場合、このAPIは指定したすべてのドメイン名の`Metric`データを統計します。<br><br>* `Project`を指定し、`Domain`を指定しない場合、このAPIは指定したプロジェクトの`Metric`データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63625#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95)を参照してください。<br><br>* `Project`も`Domain`も指定しない場合、このAPIはすべてのドメイン名の`Metric`データを統計します。 |`my_project` |
|Domain |String |いいえ |ユーザーからのリクエストをフィルタリングするための1つ以上のドメイン名を示します。このAPIは、指定した各ドメイン名の`Metric`データを統計します。最大50個のドメイン名を指定できます。複数のドメイン名はコンマ（,）で区切ります。`Domain`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br>`Project`を指定した場合、指定したドメイン名はその`Project`に属している必要があります。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出す場合、次の点に注意してください：<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)を呼び出して、アクセス権のあるドメイン名を取得できます。<br><br>* このパラメータを指定しない場合、そのIAMユーザーがアクセス権を持つすべてのドメイン名が対象となります。 |`www.example.com,www.test.com,img.example.com` |
|Location |String |いいえ |ユーザーからのリクエストをフィルタリングするための国および地域のコードを示します。1つ以上のコードを指定でき、CDNはこれらの国および地域からのユーザーからのリクエストの`Metric`データを統計します。複数の国および地域コードはコンマ（,）で区切ります。最大30の国と地域を指定できます。<br><br><br>* `Location`を指定した場合、`Province`を指定することはできません。逆も同様です。<br><br>* `Location`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br><br>[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出して、コードと国および地域の対応表を取得できます。 |`CHN,AZE` |
|Province |String |いいえ |ユーザーからのリクエストをフィルタリングするための中国の省レベルの行政区のコードを示します。1つ以上のコードを指定でき、CDNはこれらの省レベルの行政区からのユーザーからのリクエストの`Metric`データを統計します。複数のコードはコンマ（,）で区切ります。最大10個のコードを指定できます。<br><br>`Province`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br>[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出して、コードと中国の省レベルの行政区の対応表を取得できます。 |`AH,BJ,CQ,FJ` |
|Isp |String |いいえ |リクエストで使用される中国のネットワーク事業者のコードを示し、ユーザーからのリクエストをフィルタリングするために使用されます。たとえば、`CT`は中国電信を示します。1つ以上のコードを指定でき、CDNはこれらのネットワーク事業者を使用するユーザーからのリクエストの`Metric`データを統計します。複数のコードはコンマ（,）で区切ります。最大5つのコードを指定できます。<br><br><br>* `Location`が`CHN`であるか、`Province`を指定した場合にのみ、`Isp`を指定できます。<br><br>* `Isp`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br><br>[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出して、コードとネットワーク事業者の対応表を取得できます。 |`CT,CM,CU,GWBN` |
|Protocol |String |いいえ |リクエストで使用されるアプリケーション層プロトコルを示し、ユーザーからのリクエストをフィルタリングするために使用されます。このパラメータの有効な値は次のとおりです：<br><br><br>* `http`：HTTPプロトコルを示します。<br><br>* `https`：HTTPSプロトコルを示します。<br><br>* `quic`：QUICプロトコルを示します。<br><br>* `websocket`：WebSocketプロトコルを示します。<br><br>* `non-websocket`：HTTPプロトコル、HTTPSプロトコル、およびQUICプロトコルを示します。<br><br><br>`Protocol`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br>说明<br><br>`Metric`が`response_time`または`avg_speed`の場合、WebSocketプロトコルを除外するために`Protocol`を指定してください。WebSocketリクエストでは、これらの2つのメトリックのデータが不正確であるためです。 |`https` |
|IpVersion |String |いいえ |リクエストで使用されるネットワーク層プロトコルを示し、ユーザーからのリクエストをフィルタリングするために使用されます。このパラメータの有効な値は次のとおりです：<br><br><br>* `IPv4`：IPv4プロトコルを示します。<br><br>* `IPv6`：IPv6プロトコルを示します。<br><br><br>`IpVersion`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。 |`IPv4` |


<span id="プロジェクトデータの統計方法"></span>
### プロジェクトデータの統計方法

プロジェクトのメトリックデータを統計する場合、CDNはプロジェクト内のドメイン名のデータを統計します。


* 統計期間中にドメイン名がプロジェクトから転出された場合、プロジェクトのメトリックデータには転出後のドメイン名のデータは含まれません。

* 統計期間中にドメイン名がプロジェクトに転入された場合、プロジェクトのメトリックデータには転入後のドメイン名のデータが含まれます。


**例**

次のシナリオを考えます：


* 指定した統計期間は、ある日の8:00\-10:00です。

* ドメイン名Xは9:00に別のプロジェクトからプロジェクトAに移動しました。ドメイン名YはずっとプロジェクトAにあります。


このシナリオで、プロジェクトAのメトリックデータを統計する場合、メトリックデータには以下が含まれます：


* ドメイン名Xの9:00から10:00までのメトリックデータ。

* ドメイン名Yの8:00から10:00までのメトリックデータ。


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|MetricDataList |Object[] |このAPIが返す結果データを示します。 | |
|Metric |String |リクエストパラメータ`Metric`で指定されたメトリックを示します。 |`traffic` |
|Value |Double |集計後の`Metric`データを示します。このデータは`TimeZone`に対して統計されます。 |`3475788` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDistrictSummary&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "IpVersion": "IPv4",
    "Isp": "CT,CM,CU,GWBN",
    "Metric": "out_traffic",
    "Project": "my_project",
    "Protocol": "https",
    "Province": "AH,BJ,CQ,FJ"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024042306510037EB957CFE0697E4F78B",
        "Action": "DescribeDistrictSummary",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "Metric": "out_traffic",
                "Value": 191723046.9
            }
        ]
    }
}
```


&nbsp;
