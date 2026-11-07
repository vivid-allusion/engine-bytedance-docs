---
title: "DescribeEdgeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeRanking_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNが受信したユーザーからのリクエストに基づき、このAPIは一連のメトリックデータをグループ別に集計し、これらの集計データを降順にソートします。グループ化条件には、ドメイン名と課金リージョンが含まれます。

このAPIを呼び出すには、メトリック、グループ化条件、統計期間、および時間粒度を指定する必要があります。また、ユーザーからのリクエストをフィルタリングするために、複数のフィルタリング条件（課金リージョンを含む）を指定することもできます。最大で過去92日間のデータを照会できます。

データの安定性：ネットワークの変動により、エッジノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。

データの適時性：メトリックデータには約5分の遅延が生じる場合があります。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計APIを初めて使用する場合は、まず以下のドキュメントを読むことを強くお勧めします。これにより、このAPIドキュメントの理解が深まります。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp">指標の定義と計算方法</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeEdgeRanking&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeEdgeRankingです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Item |String |はい |`Metric`データを集計するためのグループ化条件を表します。このパラメータには次の値があります：<br><br><br>* `domain`：`Domain`で指定されたドメイン名を表します。<br><br>* `billingRegion`：`BillingRegion`で指定された課金リージョンを表します。 |`domain` |
|Metric |String |はい |メトリックを表します。このパラメータには次の値があります：<br><br><br>* `in_traffic`：ユーザーがCDNに転送したデータ量（単位：バイト）。<br><br>* `in_bandwidth`：ユーザーがCDNに転送したデータ量に基づいて計算されたピーク帯域幅（単位：bps）。<br><br>* `out_traffic`：CDNがユーザーに転送したデータ量（単位：バイト）。<br><br>* `out_bandwidth`：CDNがユーザーに転送したデータ量に基づいて計算されたピーク帯域幅（単位：bps）。<br><br>* `requests`：CDNが受信したすべてのユーザーからのリクエストの数。<br><br>* `dynamic_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>   * リクエストメソッドがGETでもHEADでもない。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br>* `static_requests`：CDNが受信したユーザーからのリクエストのうち、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>   * リクエストメソッドがGETまたはHEADである。<br><br>   * CDNの応答ステータスコードが405ではない。<br><br><br>各メトリックの詳細と統計方法については、[指標の定義と計算方法](https://docs.byteplus.com/en/docs/byteplus-cdn/metrics-definition-jp)を参照してください。 |`traffic` |
|BillingRegion |String |いいえ |ユーザーからのリクエストをフィルタリングするための1つ以上の課金リージョンを表します。このAPIは、これらの課金リージョンからのユーザーからのリクエストの`Metric`データを統計します。複数の課金リージョンはカンマ（,）で区切ります。このパラメータには次の値があります：<br><br><br>* `CHN`：中国本土を表します。<br><br>* `EU`：ヨーロッパを表します。<br><br>* `NA`：北米を表します。<br><br>* `SA`：南米を表します。<br><br>* `MEA`：中東およびアフリカを表します。<br><br>* `AP1`：アジア太平洋リージョン1を表します。<br><br>* `AP2`：アジア太平洋リージョン2を表します。<br><br>* `AP3`：アジア太平洋リージョン3を表します。<br><br><br>`BillingRegion`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしません。 |`CHN,EU` |
|StartTime |Long |はい |統計期間の開始時刻をUnixタイムスタンプ（秒精度）で表します。`StartTime`は`EndTime`以前である必要があります。また、`StartTime`と`EndTime`で表される統計期間は31日を超えることはできません。 |`1710259200` |
|EndTime |Long |はい |統計期間の終了時刻をUnixタイムスタンプ（秒精度）で表します。 |`1710836303` |
|Interval |String |いいえ |時間粒度を表します。このAPIは、`Interval`に基づいて`StartTime`と`EndTime`で表される統計期間を一連の時間間隔に分割し、各時間間隔の`Metric`データを統計します。<br><br>`Interval`パラメータが統計期間をどのように分割するために使用されるかについては、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメータには次の値があります：<br><br><br>* `1min`：時間粒度が1分であることを表します。<br><br>* `5min`：時間粒度が5分であることを表します。<br><br><br>指定できる時間粒度は、`StartTime`と`EndTime`で表される時間範囲の影響を受けます。<br><br><br>* 時間範囲が1日以内の場合、指定できる時間粒度は`1min`、`5min`です。<br><br>* 時間範囲が1日を超え31日以内の場合、指定できる時間粒度は`5min`です。<br><br><br>このパラメータのデフォルト値は`5min`です。デフォルト値が時間範囲と一致しない場合、APIリクエストは失敗します。 |`5min` |
|Project |String |いいえ |プロジェクトを表します。`Project`を指定しない場合、すべてのプロジェクトを表します。<br><br>`Project`と`Domain`について：<br><br><br>* `Project`を指定し、`Domain`を指定しない場合、CDNは`Item`に従って指定されたプロジェクトの`Metric`データを統計します。[プロジェクトデータの統計方法](https://docs.byteplus.com/en/docs/18/63624#%E3%83%97%E3%83%AD%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AE%E7%B5%B1%E8%A8%88%E6%96%B9%E6%B3%95)を参照してください。<br><br>* その他の場合、CDNは`Item`に従って指定されたドメイン名の`Metric`データを統計します。<br><br><br>[Item、Project、Domainの設定の組み合わせ](https://docs.byteplus.com/en/docs/18/63624#item%E3%80%81project%E3%80%81domain%E3%81%AE%E8%A8%AD%E5%AE%9A%E3%81%AE%E7%B5%84%E3%81%BF%E5%90%88%E3%82%8F%E3%81%9B)を参照してください。 |`my_project` |
|Domain |String |いいえ |ユーザーからのリクエストをフィルタリングするための1つ以上のドメイン名を表します。最大50個のドメイン名を指定できます。複数のドメイン名はカンマ（,）で区切ります。`Domain`を指定しない場合、すべてのドメイン名を表します。`Domain`パラメータの追加の説明については、`Project`パラメータを参照してください。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出す場合、次の点に注意してください：<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名のみを指定できます。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains-jp)を呼び出して、アクセス権のあるドメイン名を取得できます。<br><br>* このパラメータを指定しない場合、IAMユーザーがアクセス権を持つすべてのドメイン名を表します。 |`www.example.com,www.test.com,img.example.com` |


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


<span id="item、project、domainの設定の組み合わせ"></span>
### Item、Project、Domainの設定の組み合わせ


| **グループ化条件** | **フィルタリング条件** ||**説明** |
|---|---|---|---|
|**Item** |**Project** |**Domain** ||
|domain |指定 |指定 |指定されたドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |
||指定 |指定しない |指定されたプロジェクトのすべてのドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |
||指定しない |指定 |指定されたドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |
||指定しない |指定しない |すべてのドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |
|project |指定 |指定 |*不正* |
||指定 |指定しない |指定されたプロジェクトについて、各 **プロジェクト** のメトリックデータを統計します。 |
||指定しない |指定 |*不正* |
||指定しない |指定しない |すべてのプロジェクトについて、各 **プロジェクト** のメトリックデータを統計します。 |
|billingRegion |指定 |指定 |指定されたドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |
||指定 |指定しない |指定されたプロジェクトについて、各 **プロジェクト** のメトリックデータを統計します。 |
||指定しない |指定 |指定されたドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |
||指定しない |指定しない |すべてのドメイン名について、各 **ドメイン名**のメトリックデータを統計します。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Item |String |リクエストパラメータ`Item`で指定されたグループ化条件を表します。 |`domain` |
|TopDataDetails |Object[] |このAPIが返す結果データを表します。 | |
|Metric |String |リクエストパラメータ`Metric`で指定されたメトリックを表します。 |`requests` |
|ValueDetails |Object[] |`Item`によって集計された`Metric`データの詳細を含むデータオブジェクトのセットを表します。これらのデータオブジェクトは`Value`の降順にソートされます。 | |
|ItemKey |String |`Item`に属する値を表します。<br><br><br>* `Item`が`domain`の場合、`ItemKey`はリクエストパラメータ`Domain`で指定されたリスト内のドメイン名です。<br><br>* `Item`が`BillingRegion`の場合、`ItemKey`はリクエストパラメータ`BillingRegion`で指定されたリスト内の課金リージョンです。 |`www.example.com` |
|Ratio |Double |この`ItemKey`の`Value`が、すべての`ItemKey`の`Value`の合計に占める割合を表します。<br><br>`Metric`が`bandwidth`の場合、このパラメータは無効であり、その値は常に`0`であることに注意してください。 |`0.978` |
|Timestamp |Long |`Value`の時点をUnixタイムスタンプ（秒精度）で表します。このパラメータは`Metric`が`bandwidth`の場合にのみ有効であり、ピーク帯域幅の時刻を表します。`Metric`が`bandwidth`でない場合、このパラメータは無効であり、その値は常に`0`です。 |`1710419700` |
|Value |Double |この`ItemKey`の集計`Metric`データを表します。 |`456` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "out_traffic",
    "Item": "domain",
    "BillingRegion": "CHN,EU",
    "Project": "my_project",
    "Domain": "www.example.com,www.test.com,img.example.com"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404230653511721F4B223CB40DB0A16",
        "Action": "DescribeEdgeRanking",
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
                        "Ratio": 0.8358,
                        "Timestamp": 0,
                        "Value": 63217888212.6
                    },
                    {
                        "ItemKey": "www.test.com",
                        "Ratio": 0.1642,
                        "Timestamp": 0,
                        "Value": 12417784242.6
                    },
                    {
                        "ItemKey": "img.example.com",
                        "Ratio": 0,
                        "Timestamp": 0,
                        "Value": 1584509.3
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
