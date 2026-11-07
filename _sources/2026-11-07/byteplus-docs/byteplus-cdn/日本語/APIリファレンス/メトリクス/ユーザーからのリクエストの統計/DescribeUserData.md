---
title: "DescribeUserData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeUserData_jp"
---

<span id="apiの説明"></span>
## APIの説明

CDNが受信したユーザーからのリクエストに基づき、このAPIは各時点におけるユニークなクライアントIPアドレスの数を統計します。

このAPIを呼び出すには、ドメイン名、統計期間、および時間粒度を指定する必要があります。また、複数のフィルタリング条件を指定してユーザーからのリクエストをフィルタリングすることもできます。最大で過去92日間のデータをクエリできます。

データの安定性：ネットワークの変動により、エッジノードで統計されたメトリックデータが変更される可能性があります。ほとんどの場合、メトリックデータは12時間以内に徐々に安定します。

データの適時性：ユニークビジター数は、1時間粒度で統計されたメトリックデータに基づいています。そのため、データ統計には約2時間の遅延が生じる可能性があります。たとえば、09:00から10:00までの時間帯のユニークビジター数については、11:00頃に正確な結果を取得できます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">データ統計APIを初めて使用する場合は、まず以下のドキュメントを読むことをお勧めします。これにより、このAPIドキュメントの理解が深まります。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp">統計期間の説明</a></div>



<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeUserDataです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|StartTime |Long |はい |統計期間の開始時刻をUnixタイムスタンプ（秒単位）で示します。`StartTime`は`EndTime`以前である必要があります。また、`StartTime`と`EndTime`で示される統計期間は31日を超えることはできません。 | |
|EndTime |Long |はい |統計期間の終了時刻をUnixタイムスタンプ（秒単位）で示します。 | |
|Interval |String |はい |時間粒度を示します。このAPIは、`Interval`に基づいて`StartTime`と`EndTime`で示される統計期間を一連の時間間隔に分割し、各時間間隔のユニークなクライアントIPアドレスの数を統計します。<br><br>`Interval`パラメータが統計期間をどのように分割するために使用されるかについては、[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。<br><br>このパラメータには次の値があります：<br><br><br>* `hour`：時間粒度が1時間であることを示します。<br><br>* `day`：時間粒度が1日であることを示します。 | |
|Domain |String |はい |ユーザーからのリクエストをフィルタリングするためのドメイン名を示します。<br><br>说明<br><br>IAMユーザーがこのAPIを呼び出す場合、次の点に注意してください：<br><br><br>* IAMユーザーが指定できるドメイン名は、そのIAMユーザーがアクセス権を持つドメイン名です。IAMユーザーは[DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomains_jp)を呼び出して、アクセス権のあるドメイン名を取得できます。 | |
|IpVersion |String |いいえ |ユーザーからのリクエストをフィルタリングするために使用されるネットワーク層プロトコルを示します。このパラメータの有効な値は次のとおりです：<br><br><br>* `IPv4`：IPv4プロトコルを示します。<br><br>* `IPv6`：IPv6プロトコルを示します。<br><br><br>`IpVersion`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。 | |
|Location |String |いいえ |ユーザーからのリクエストをフィルタリングするための国または地域のコードを示します。CDNは、これらの国および地域からのユーザーからのリクエストのクライアントIPアドレスの数を統計します。<br><br><br>* `Location`を指定した場合、`Province`を指定することはできません。逆も同様です。<br><br>* `Location`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br><br>[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出して、コードと国および地域の対応表を取得できます。 | |
|Province |String |いいえ |ユーザーからのリクエストをフィルタリングするための中国の省レベルの行政区のコードを示します。CDNは、これらの省レベルの行政区からのユーザーからのリクエストのクライアントIPアドレスの数を統計します。<br><br>`Province`を指定しない場合、このパラメータを使用してリクエストをフィルタリングしないことを示します。<br><br>[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出して、コードと中国の省レベルの行政区の対応表を取得できます。 | |
|TimeZone |String |いいえ |タイムゾーンパラメータを指定します。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|MetricDataList |Object[] |各時点におけるユニークなクライアントIPアドレスの数を含むデータオブジェクトのセットを示します。 | |
|TimeStamp |Long |時点をUnixタイムスタンプ（秒単位）で示します。[統計期間の説明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_jp)を参照してください。 | |
|Value |Double |この`TimeStamp`時点におけるユニークなクライアントIPアドレスの数を示します。このデータのタイムゾーンはUTC+08:00です。 | |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021-03-01
{
    "Domain": "www.example.com",
    "StartTime": 1710950400,
    "EndTime": 1710998170,
    "Interval": "hour",
    "IpVersion": "IPv4",
    "Province": "AH"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403220141458C564C77FA147001D2E1",
        "Action": "DescribeUserData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "TimeStamp": 1710950400,
                "Value": 421
            },
            {
                "TimeStamp": 1710954000,
                "Value": 428
            },
            {
                "TimeStamp": 1710957600,
                "Value": 439
            },
            {
                "TimeStamp": 1710961200,
                "Value": 436
            },
            {
                "TimeStamp": 1710964800,
                "Value": 435
            },
            {
                "TimeStamp": 1710968400,
                "Value": 446
            },
            {
                "TimeStamp": 1710972000,
                "Value": 433
            },
            {
                "TimeStamp": 1710975600,
                "Value": 430
            },
            {
                "TimeStamp": 1710979200,
                "Value": 428
            },
            {
                "TimeStamp": 1710982800,
                "Value": 412
            },
            {
                "TimeStamp": 1710986400,
                "Value": 423
            },
            {
                "TimeStamp": 1710990000,
                "Value": 417
            },
            {
                "TimeStamp": 1710993600,
                "Value": 394
            },
            {
                "TimeStamp": 1710997200,
                "Value": 407
            }
        ]
    }
}
```


&nbsp;
