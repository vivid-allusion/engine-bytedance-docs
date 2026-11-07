---
title: "DescribeCdnRegionAndIsp"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp"
---

BytePlus IP アドレスデータベースがカバーする中国の省レベルの行政区画、世界の国と地域、および中国本土のネットワーク事業者の名前とコードを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1 秒あたり最大 20 件の API リクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeCdnRegionAndIspです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Area |String |いいえ |クエリの範囲を示します。このパラメータには次の値があります。<br><br><br>* `China`：中国の省レベルの行政区画と中国本土のネットワーク事業者のコードと名前を示します。<br><br>* `Global`：世界の国と地域、および中国本土のネットワーク事業者のコードと名前を示します。<br><br><br>このパラメータのデフォルト値は `China` です。 |`Global` |
|Lang |String |いいえ |クエリ結果が表示される言語を示します。このパラメータには次の値があります。<br><br><br>* `zh`：簡体字中国語を示します。<br><br>* `en`：英語を示します。<br><br><br>このパラメータのデフォルト値は `en` です。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Isps |Object[] |中国本土のネットワーク事業者を示します。 | |
|Code |String |ネットワーク事業者のコードを示します。 |`UNICOM` |
|Name |String |ネットワーク事業者の名前を示します。 |`中国联通` |
|Regions |Object[] |エリアのリストを示します。<br><br><br>* `Area` が `Global` の場合、このパラメータは世界の国と地域のリストを示します。<br><br>* `Area` が `China` の場合、このパラメータは中国の各省レベルの行政区画のリストを示します。 | |
|Code |String |国、地域、または中国の省レベルの行政区画のコードを示します。 |`BJ` |
|Name |String |国、地域、または中国の省レベルの行政区画の名前を示します。 |`北京` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnRegionAndIsp&Version=2021-03-01
{
    "Area": "Global"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423061106DA1BD20A355B07CBEC2D",
        "Action": "DescribeCdnRegionAndIsp",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Isps": [
            {
                "Code": "CT",
                "Name": "China Telecom"
            },
            {
                "Code": "CM",
                "Name": "China Mobile"
            },
            {
                "Code": "CU",
                "Name": "China Unicom"
            },
            {
                "Code": "GWBN",
                "Name": "Great Wall Broadband"
            },
            ...
        ],
        "Regions": [
            {
                "Code": "CHE",
                "Name": "Switzerland"
            },
            {
                "Code": "AZE",
                "Name": "Azerbaijan"
            },
            {
                "Code": "PNG",
                "Name": "Papua New Guinea"
            },
            {
                "Code": "PSE",
                "Name": "Palestine"
            },
            {
                "Code": "FSM",
                "Name": "Micronesia"
            },
            ...
        ]
    }
}
```


&nbsp;
