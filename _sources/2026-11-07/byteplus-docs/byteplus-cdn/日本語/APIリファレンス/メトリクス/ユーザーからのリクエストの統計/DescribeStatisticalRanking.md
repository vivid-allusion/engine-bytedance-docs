---
title: "DescribeStatisticalRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeStatisticalRanking_jp"
---

<span id="api-説明"></span>
## API 説明

この API は、CDN が受信したユーザーからのリクエストに基づいて、一連のメトリックデータを人気オブジェクトタイプ別に集計し、これらの集計データを大きいものから順に並べ替え、最後にこれらの人気オブジェクトを返します。人気オブジェクトタイプには、リクエストクライアントの国と地域、リクエスト URL、Referer ドメイン、UA 文字列内のオブジェクト、独立したクライアント IP アドレスの数が含まれます。

この API を呼び出す際には、メトリック、人気オブジェクトタイプ、統計期間、および時間粒度を 1 つ指定する必要があります。また、複数のフィルタリング条件を指定してユーザーからのリクエストをフィルタリングすることもできます。最大で過去 92 日間のデータを照会できます。

データの安定性：ネットワークの変動の影響により、エッジノードで統計されたメトリックデータが変化する可能性があります。ほとんどの場合、メトリックデータは 12 時間以内に徐々に安定します。

データの適時性：人気オブジェクトは、時間単位で統計されたメトリックデータに基づいています。そのため、データ統計には約 2 時間の遅延が生じる可能性があります。たとえば、09:00 から 10:00 までの時間帯の人気オブジェクトについては、11:00 頃に正確な結果を取得できます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1 秒あたり最大 20 件の API リクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeStatisticalRankingです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Item |String |はい |グループ化および並べ替え条件として、人気オブジェクトのタイプを表します。この API は `Item` に基づいて `Metric` データを集計し、これらの集計データを並べ替えます。このパラメーターには次の値があります。<br><br><br>* `region`：リクエストクライアントの国または地域を表します。<br><br>* `url`：リクエスト URL のパスを表します。<br><br>* `referer`：リクエストの `Referer` ドメインを表します。<br><br>* `ua`：リクエストの `User-Agent` 文字列を表します。<br><br>* `clientip`：クライアントの IP アドレスを表します。<br><br><br>说明<br><br><br>* `Item` が `ua` の場合、追加のグループ化条件として `UaType` を指定する必要もあります。<br><br>* `Item` が `region` の場合、追加のグループ化条件として `Area` を指定する必要もあります。 |`region` |
|Metric |String |はい |メトリックを表します。このパラメーターの使用可能な値は `Item` の影響を受けます。<br><br><br>* `Item` が `referer`、`ua`、または `clientip` の場合、このパラメーターには次の値があります。<br><br>   * `in_traffic`：ユーザーが CDN に転送したデータ量（バイト単位）。<br><br>   * `out_traffic`：CDN がユーザーに転送したデータ量（バイト単位）。<br><br>   * `requests`：CDN が受信したユーザーからのリクエストの数。<br><br>   * `dynamic_requests`：CDN が受信した、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>      * リクエストメソッドが GET でも HEAD でもない。<br><br>      * CDN の応答ステータスコードが 405 ではない。<br><br>   * `static_requests`：CDN が受信した、次のすべての条件を満たすユーザーからのリクエストの数。<br><br>      * リクエストメソッドが GET または HEAD である。<br><br>      * CDN の応答ステータスコードが 405 ではない。<br><br>* `Item` が `url` の場合、このパラメーターには次の値があります。<br><br>   * `in_traffic`<br><br>   * `out_traffic`<br><br>   * `requests`<br><br>   * `dynamic_requests`<br><br>   * `static_requests`<br><br>   * `status_2xx`：CDN のユーザーからのリクエストへの応答で、このパラメーターは 2xx ステータスコードの数を表します。<br><br>   * `status_3xx`：3xx ステータスコードの数を表します。<br><br>   * `status_4xx`：4xx ステータスコードの数を表します。<br><br>   * `status_5xx`：5xx ステータスコードの数を表します。<br><br>* `Item` が `region` の場合、このパラメーターには次の値があります。<br><br>   * `clientip`：独立したクライアント IP アドレスの数を表します。<br><br>   `Item` が `region` の場合、このパラメーターのデフォルト値は `clientip` であり、指定しなくてもかまいません。 |`traffic` |
|StartTime |Long |はい |統計期間の開始時刻を表します。形式は Unix タイムスタンプで、精度は秒です。`StartTime` は `EndTime` 以前である必要があります。同時に、`StartTime` と `EndTime` が表す統計期間は 31 日を超えることはできません。<br><br>说明<br><br><br>* `StartTime` と `EndTime` は統計期間を指定します。ただし、実際の統計期間の開始時刻と終了時刻は両方とも時間単位です。<br><br>   例：`StarTime` が表す時刻が 15:07 で、`EndTime` が表す時刻が 15:21 の場合、実際の統計期間は [15:00,16:00）です。<br><br>   `EndTime` がちょうど正時の場合、実際の統計期間はさらに 1 時間延長されることに注意してください。`StartTime` が表す時刻が 15:07 で、`EndTime` が表す時刻が 16:00 の場合、実際の統計期間は [15:00,17:00）です。 |`1710950400` |
|EndTime |Long |はい |統計期間の終了時刻を表します。形式は Unix タイムスタンプで、精度は秒です。 |`1710998170` |
|Domain |String |はい |ユーザーからのリクエストをフィルタリングするために使用されるドメイン名を表します。<br><br>说明<br><br>IAMユーザーがこの API を呼び出す場合、次の点に注意してください。<br><br><br>* IAMユーザーは、アクセス権のあるドメイン名を 1 つだけ指定できます。IAMユーザーは [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp) を呼び出して、アクセス権のあるドメイン名を取得できます。 | |
|UaType |String |いいえ |User\-Agent 文字列内のオブジェクトタイプを表します。`Item` が `ua` の場合、このパラメーターは追加のグループ化条件として指定する必要があります。`Item` が `ua` でない場合、このパラメーターは無効です。<br><br>このパラメーターには次の値があります。<br><br><br>* `browser`：`User-Agent` 文字列内のブラウザタイプを表します。<br><br>* `system`：`User-Agent` 文字列内のオペレーティングシステムタイプを表します。<br><br>* `equipment`：`User-Agent` 文字列内のクライアントデバイスのタイプを表します。 |`system` |
|Area |String |いいえ |地域タイプを表します。このパラメーターは、`Item` が `region` の場合にのみ有効で、クライアント IP アドレス数の地域分布を取得するための追加のグループ化条件として使用されます。このパラメーターには次の値があります。<br><br><br>* `Global`：世界の国と地域を表します。<br><br>* `China`：中国の省レベルの行政区を表します。<br><br><br>说明<br><br><br>* `Metric` を指定しない場合、`Area` は指定しなくてもかまいません。<br><br>   * `Area` を指定しない場合、この API は国、地域、中国の省レベルの行政区別に分布した独立したクライアント IP アドレスの数を返します。<br><br>* `Metric` を指定した場合、`Area` を指定する必要があります。 |`global` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Item |String |リクエストパラメーター `Item` で指定された人気オブジェクトタイプを表します。 |`region` |
|Metric |String |リクエストパラメーター `Metric` で指定されたメトリックを表します。 |`traffic` |
|RankingDataList |Object[] |人気オブジェクトの詳細のリストを表します。 | |
|ItemKey |String |人気オブジェクトを表します。<br><br><br>* `Item` が `url` の場合、この人気オブジェクトはリクエスト URL のパスです。<br><br>* `Item` が `referer` の場合、この人気オブジェクトは `Referer` ドメインです。<br><br>* `Item` が `region` の場合、この人気オブジェクトは地域コードです。<br><br>* `Item` が `clientip` の場合、この人気オブジェクトは国、地域、または中国の省レベルの行政区のコードです。<br><br>* `Item` が `ua` の場合、<br><br>   * `UaType` が `equipment` の場合、この人気オブジェクトはある種のデバイスタイプです。<br><br>   * `UaType` が `system` の場合、この人気オブジェクトはある種のオペレーティングシステムです。<br><br>   * `UaType` が `browser` の場合、この人気オブジェクトはある種のブラウザです。 |`GS` |
|ItemKeyCN |String |* `Item` が `region` と `clientip` の場合、`ItemKeyCN` は `ItemKey` に対応する地域の中国語名です。<br><br>* `Item` が `url` の場合、`ItemKeyCN` は `ItemKey` に対応するパスです。<br><br>* `Item` が `ua`、`referer`、`url`、または `referer` の場合、`ItemKeyCN` は `ItemKey` と同じです。 |`甘肃` |
|Value |Double |この `ItemKey` の集計 `Metric` データを表します。`Value` のタイムゾーンは UTC+08:00 です。 |`777` |
|UaType |String |リクエストパラメーターの `UaType` で指定されたオブジェクトタイプを表します。リクエストパラメーターに `UaType` が含まれていない場合、このパラメーターは応答結果に表示されません。 |`system` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021-03-01
{
    "Area": "Global",
    "Domain": "www.example.com",
    "StartTime": 1720614677,
    "EndTime": 1721478677,
    "Item": "region",
    "Metric": "clientip"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202407221231341976A83AF08B9822FD8F",
        "Action": "DescribeStatisticalRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "region",
        "Metric": "clientip",
        "RankingDataList": [
            {
                "ItemKey": "USA",
                "ItemKeyCN": "美国",
                "Value": 2857990
            },
            {
                "ItemKey": "IND",
                "ItemKeyCN": "印度",
                "Value": 744081
            },
            {
                "ItemKey": "BRA",
                "ItemKeyCN": "巴西",
                "Value": 695588
            },
            {
                "ItemKey": "FRA",
                "ItemKeyCN": "法国",
                "Value": 454253
            },
            ...
        ]
    }
}
```


&nbsp;
