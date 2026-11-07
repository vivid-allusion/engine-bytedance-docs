---
title: "DescribeEdgeStatusCodeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeStatusCodeRanking_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNが受信したユーザーからのリクエストに基づき、このAPIはドメイン名ごとに一連のメトリックデータを集計し、これらの集計データを大きいものから小さいものへと並べ替えます。

このAPIを呼び出すには、ステータスコードメトリック、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件を指定してユーザーからのリクエストをフィルタリングすることもできます。最大で過去92日間のデータを照会できます。

データの安定性：ネットワークの変動の影響により、エッジノードで統計されたメトリックデータが変化することがあります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。

データの適時性：メトリックデータには約5分の遅延が生じることがあります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計APIを初めて使用する場合は、まず以下のドキュメントを読むことを強くお勧めします。これにより、このAPIドキュメントの理解が深まります。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeEdgeStatusCodeRanking&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeEdgeStatusCodeRankingです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Item |String |はい |グループ化条件を示します。現在、このパラメーターの値は `domain` のみで、`Domain` に基づいて `Metric` データを集計することを示します。 |`domain` |
|Metric |String |はい |CDNがユーザーからのリクエストに応答する際、このパラメーターは次のいずれかのカテゴリのステータスコードの数を示します：<br><br><br>* `status_2xx`：2xxステータスコードの数を示します。<br><br>* `status_3xx`：3xxステータスコードの数を示します。<br><br>* `status_4xx`：4xxステータスコードの数を示します。<br><br>* `status_5xx`：5xxステータスコードの数を示します。 |`status_4xx` |
|StartTime |Long |はい |統計期間の開始時刻をUnixタイムスタンプ（秒単位）で示します。`StartTime` は `EndTime` 以前でなければなりません。また、`StartTime` と `EndTime` で示される統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻をUnixタイムスタンプ（秒単位）で示します。 |`1710836303` |
|Interval |String |いいえ |時間粒度を示します。このAPIは `Interval` に基づいて `StartTime` と `EndTime` で示される統計期間を一連の時間間隔に分割し、各時間間隔の `Metric` データを統計します。<br><br>`Interval` パラメーターが統計期間をどのように分割するために使用されるかについては、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp) を参照してください。<br><br>このパラメーターには次の値があります：<br><br><br>* `1min`：時間粒度が1分であることを示します。<br><br>* `5min`：時間粒度が5分であることを示します。<br><br><br>指定できる時間粒度は、`StartTime` と `EndTime` で示される時間範囲の影響を受けます。<br><br><br>* 時間範囲が1日以下の場合、指定できる時間粒度は `1min`、`5min` です。<br><br>* 時間範囲が1日を超え31日以下の場合、指定できる時間粒度は `5min` です。<br><br><br>このパラメーターのデフォルト値は `5min` です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 |`1min` |
|Project |String |いいえ |プロジェクトを示します。<br><br><br>* `Domain` を指定した場合、APIは指定されたすべてのドメイン名の `Metric` データを統計します。<br><br>* `Project` を指定し、`Domain` を指定しなかった場合、APIは指定されたプロジェクトの `Metric` データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63622#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95) を参照してください。<br><br>* `Project` も `Domain` も指定しなかった場合、APIはすべてのドメイン名の `Metric` データを統計します。 |`my_project` |
|Domain |String |いいえ |ユーザーからのリクエストをフィルタリングするために使用される1つまたは複数のドメイン名を示します。このAPIは、指定された各ドメイン名の `Metric` データを統計します。最大50個のドメイン名を指定できます。複数のドメイン名はコンマ（,）で区切ります。`Domain` を指定しない場合、このパラメーターを使用してリクエストをフィルタリングしないことを示します。<br><br>`Project` を指定した場合、指定するドメイン名はその `Project` に属している必要があります。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出す場合、次の点に注意してください：<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp) を呼び出して、アクセス権のあるドメイン名を取得できます。<br><br>* このパラメーターを指定しない場合、そのIAMユーザーがアクセス権を持つすべてのドメイン名が対象となります。 |`www.example.com,www.test.com,img.example.com` |


<span id="プロジェクトデータの統計方法"></span>
### プロジェクトデータの統計方法

プロジェクトのメトリックデータを統計する場合、CDNはプロジェクト内のドメイン名のデータを統計します。


* 統計期間中にドメイン名がプロジェクトから転出された場合、そのプロジェクトのメトリックデータには転出後のドメイン名のデータは含まれません。

* 統計期間中にドメイン名がプロジェクトに転入された場合、そのプロジェクトのメトリックデータには転入後のドメイン名のデータが含まれます。


**例**

次のシナリオを考えてみましょう：


* 指定した統計期間は、ある日の8:00\-10:00です。

* ドメイン名Xは9:00に別のプロジェクトからプロジェクトAに移動しました。ドメイン名YはずっとプロジェクトAにあります。


このシナリオでプロジェクトAのメトリックデータを統計する場合、メトリックデータには次のものが含まれます：


* ドメイン名Xの9:00から10:00までのメトリックデータ。

* ドメイン名Yの8:00から10:00までのメトリックデータ。


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Item |String |リクエストパラメーター `Item` で指定されたグループ化条件を示します。 |`domain` |
|Metric |String |リクエストパラメーター `Metric` で指定されたメトリックを示します。 |`status_4xx` |
|TopDataDetails |Object[] |`Item` によって集計された `Metric` データの詳細を含むデータオブジェクトのセットを示します。各データオブジェクトには、各カテゴリのステータスコードの数と割合が含まれます。これらのデータオブジェクトは、指定された `Metric` に従って大きいものから小さいものへと並べ替えられます。 | |
|ItemKey |String |`Domain` リスト内のドメイン名を示します。 |`www.example.com` |
|Status2xx |Double |この `ItemKey` の2xxステータスコードの数を示します。 |`45678` |
|Status2xxRatio |Double |この `ItemKey` の2xxステータスコードの割合を示します。 |`0.47` |
|Status3xx |Double |この `ItemKey` の3xxステータスコードの数を示します。 |`0` |
|Status3xxRatio |Double |この `ItemKey` の3xxステータスコードの割合を示します。 |`0` |
|Status4xx |Double |この `ItemKey` の4xxステータスコードの数を示します。 |`3` |
|Status4xxRatio |Double |この `ItemKey` の4xxステータスコードの割合を示します。 |`0.0001` |
|Status5xx |Double |この `ItemKey` の5xxステータスコードの数を示します。 |`0` |
|Status5xxRatio |Double |この `ItemKey` の5xxステータスコードの割合を示します。 |`0` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeStatusCodeRanking&Version=2021-03-01
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
        "RequestId": "20240319234228A07998A9B5FFC309EB82",
        "Action": "DescribeEdgeStatusCodeRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "Metric": "status_2xx",
        "TopDataDetails": [
            {
                "ItemKey": "img.example.com.com",
                "Status2xx": 22428898,
                "Status2xxRatio": 0.61,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 333,
                "Status4xxRatio": 0.0001,
                "Status5xx": 34,
                "Status5xxRatio": 0
            },
            {
                "ItemKey": "www.test.com",
                "Status2xx": 9470608,
                "Status2xxRatio": 0.37,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 2380317,
                "Status4xxRatio": 0.6019,
                "Status5xx": 324607,
                "Status5xxRatio": 0.0109
            },
            {
                "ItemKey": "www.example.com",
                "Status2xx": 3069749,
                "Status2xxRatio": 0.02,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 7,
                "Status4xxRatio": 0,
                "Status5xx": 0,
                "Status5xxRatio": 0
            }
        ]
    }
}
```


&nbsp;
