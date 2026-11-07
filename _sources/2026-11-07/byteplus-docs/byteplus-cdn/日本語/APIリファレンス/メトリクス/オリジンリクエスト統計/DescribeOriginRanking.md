---
title: "DescribeOriginRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginRanking_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNがオリジンサーバーに送信するリクエスト（オリジンリクエスト）に基づき、このAPIはドメインごとに一連のメトリックデータを集計し、これらの集計データを大きいものから順に並べ替えます。

このAPIを呼び出すには、メトリック、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件を指定してオリジンリクエストをフィルタリングすることもできます。最大で過去92日間のデータを照会できます。

データの安定性：ネットワークの変動の影響により、エッジノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。

データの適時性：メトリックデータには約5分の遅延が生じる可能性があります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計APIを初めて使用する場合は、まず以下のドキュメントを読むことをお勧めします。これにより、このAPIドキュメントの理解が深まります。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp">指標の定義と計算方法</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeOriginRanking&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeOriginRankingです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Item |String |はい |`Metric`データを集計するためのグループ化条件を表します。現在、このパラメータの値は`domain`のみ可能で、`Domain`ごとに`Metric`データを集計することを意味します。 |`domain` |
|Metric |String |はい |<ins>メトリックを表します</ins>。このパラメータには次の値があります：<br><br><br>* `in_traffic`：オリジンサーバーがCDNに転送するデータ量（バイト単位）。<br><br>* `in_bandwidth`：オリジンサーバーがCDNに転送するデータ量に基づいて計算された帯域幅のピーク値（bps単位）。<br><br>* `out_traffic`：CDNがオリジンサーバーに転送するデータ量（バイト単位）。<br><br>* `out_bandwidth`：CDNがオリジンサーバーに転送するデータ量に基づいて計算された帯域幅のピーク値（bps単位）。<br><br>* `requests`：オリジンリクエストの数。<br><br><br>各メトリックの詳細と統計方法については、[指標の定義と計算方法](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp)を参照してください。 |`traffic` |
|StartTime |Long |はい |統計期間の開始時刻をUnixタイムスタンプ形式（秒単位）で表します。`StartTime`は`EndTime`以前である必要があります。また、`StartTime`と`EndTime`で表される統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻をUnixタイムスタンプ形式（秒単位）で表します。 |`1710836303` |
|Interval |String |いいえ |時間粒度を表します。このAPIは`Interval`に基づいて`StartTime`と`EndTime`で表される統計期間を一連の時間間隔に分割し、各時間間隔の`Metric`データを統計します。<br><br>`Interval`パラメータが統計期間をどのように分割するために使用されるかについては、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメータには次の値があります：<br><br><br>* `1min`：時間粒度が1分であることを示します。<br><br>* `5min`：時間粒度が5分であることを示します。<br><br><br>指定できる時間粒度は、`StartTime`と`EndTime`で表される時間範囲の影響を受けます。<br><br><br>* 時間範囲<= 1日の場合、指定できる時間粒度は`1min`、`5min`です。<br><br>* 1日<時間範囲<= 31日の場合、指定できる時間粒度は`5min`のみです。<br><br><br>このパラメータのデフォルト値は`5min`です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 |`5min` |
|Project |String |いいえ |プロジェクトを表します。`Project`を指定しない場合は、すべてのプロジェクトを意味します。<br><br>`Project`と`Domain`について：<br><br><br>* `Project`を指定し、`Domain`を指定しない場合、CDNは`Item`ごとに指定されたプロジェクトの`Metric`データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63632#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95)を参照してください。<br><br>* その他の場合、CDNは`Item`ごとに指定されたドメインの`Metric`データを統計します。 |`my_project` |
|Domain |String |いいえ |1つまたは複数のドメイン名を表し、オリジンリクエストのフィルタリングに使用されます。最大50個のドメイン名を指定できます。複数のドメイン名はコンマ（,）で区切ります。`Domain`を指定しない場合は、すべてのドメイン名を意味します。`Domain`パラメータの追加説明については、`Project`パラメータを参照してください。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出す場合、次の点に注意してください：<br><br><br>* IAMユーザーは、アクセス権のあるドメインのみを指定できます。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)を呼び出して、アクセス権のあるドメインを取得できます。<br><br>* このパラメータを指定しない場合、そのIAMユーザーがアクセス権を持つすべてのドメインを意味します。 |`www.example.com,www.test.com,img.example.com` |


<span id="プロジェクトデータの統計方法"></span>
### プロジェクトデータの統計方法

プロジェクトのメトリックデータを統計する場合、CDNはプロジェクト内のドメインのデータを統計します。


* 統計期間中にドメインがプロジェクトから転出された場合、そのプロジェクトのメトリックデータには転出後のドメインのデータは含まれません。

* 統計期間中にドメインがプロジェクトに転入された場合、そのプロジェクトのメトリックデータには転入後のドメインのデータが含まれます。


**例**

次のシナリオを考えます：


* 指定した統計期間は、ある日の8:00\-10:00です。

* ドメインXは9:00に別のプロジェクトからプロジェクトAに移動しました。ドメインYはずっとプロジェクトAにあります。


このシナリオで、プロジェクトAのメトリックデータを統計する場合、メトリックデータは以下をカバーします：


* ドメインXの9:00から10:00までのメトリックデータ。

* ドメインYの8:00から10:00までのメトリックデータ。


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Item |String |リクエストパラメータ`Item`で指定されたグループ化条件を表します。 |`domain` |
|TopDataDetails |Object[] |このAPIが返す結果データを表します。 | |
|Metric |String |リクエストパラメータ`Metric`で指定されたメトリックを表します。 | |
|ValueDetails |Object[] |`Item`で集計された`Metric`データの詳細を含むデータオブジェクトのセットを表します。これらのデータオブジェクトは`Value`の大きいものから順に並べ替えられます。 | |
|ItemKey |String |`Domain`リスト内のドメイン名を表します。 |`www.example.com` |
|Ratio |Double |この`ItemKey`の`Value`が、すべての`ItemKey`の`Value`の合計に占める割合を表します。<br><br>`Metric`が`bandwidth`の場合、このパラメータは無効であり、その値は常に`0`であることに注意してください。 |`0.867` |
|Timestamp |Long |この`ItemKey`の`Value`が、すべての`ItemKey`の`Value`の合計に占める割合を表します。<br><br>`Metric`が`bandwidth`の場合、このパラメータは無効であり、その値は常に`0`であることに注意してください。 |`1710419700` |
|Value |Double |この`ItemKey`の集計`Metric`データを表します。 |`457` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeOriginRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "out_traffic",
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
        "RequestId": "2024031923314574F098A8E1F336074314",
        "Action": "DescribeOriginRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "TopDataDetails": [
            {
                "Metric": "out_traffic",
                "ValueDetails": [
                    {
                        "ItemKey": "www.example.com",
                        "Ratio": 0.9614,
                        "Timestamp": 0,
                        "Value": 3003726848
                    },
                    {
                        "ItemKey": "img.example.com",
                        "Ratio": 0.0223,
                        "Timestamp": 0,
                        "Value": 69603224
                    },
                    {
                        "ItemKey": "www.test.com",
                        "Ratio": 0.0073,
                        "Timestamp": 0,
                        "Value": 22942093
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
