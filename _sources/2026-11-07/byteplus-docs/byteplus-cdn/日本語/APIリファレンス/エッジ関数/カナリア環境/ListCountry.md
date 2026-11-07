---
title: "ListCountry"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCountry_jp"
---

国リストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListCountry&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |APIの名前。現在のAPIの名前は `ListCountry` です。 |
|Version |String |はい |APIのバージョン。現在のAPIのバージョンは `2021-03-01` です。 |
|Continents |String |いいえ |大陸を指定します。複数の大陸を指定する場合はカンマで区切ります。 |
|Page |Integer |いいえ |国リストのページ番号。<br><br>&nbsp;<br><br>PageパラメータとLimitパラメータの両方を指定しない場合、全データが返されます。Limitのみを指定し、Pageを指定しない場合、第1ページのデータが返されます。Pageのみを指定し、Limitを指定しない場合、全データが返されます。PageとLimitの両方を指定した場合、条件に合致するデータが返されます。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。現在、1ページあたり最大50レコードを取得できます。<br><br>&nbsp;<br><br>PageパラメータとLimitパラメータの両方を指定しない場合、全データが返されます。Limitのみを指定し、Pageを指定しない場合、第1ページのデータが返されます。Pageのみを指定し、Limitを指定しない場合、全データが返されます。PageとLimitの両方を指定した場合、条件に合致するデータが返されます。 |
|OrderBy |Integer |いいえ |国のソート方法。<br><br><br>* 1：降順でデータを並べ替えます。<br><br>* 2（デフォルト）：昇順でデータを並べ替えます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|Countries |Object[] |国リスト。 | |
|Country |String |国または地域。 |`United States` |
|Continent |String |国または地域が属する大陸。 |`North America` |
|TotalCount |Long |検索条件に一致する国または地域の総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListCountry&Version=2021-03-01&Continents=Asia,Europe
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListCountry",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Countries": [
            {
                "Continent": "Asia",
                "Country": "Vietnam"
            },
            {
                "Continent": "Europe",
                "Country": "France"
            },
            {
                "Continent": "Asia",
                "Country": "Singapore"
            },
            {
                "Continent": "Asia",
                "Country": "Japan"
            },
            {
                "Continent": "Europe",
                "Country": "Germany"
            },
            {
                "Continent": "North America",
                "Country": "United States"
            },
            {
                "Continent": "Asia",
                "Country": "Thailand"
            },
            {
                "Continent": "Europe",
                "Country": "Russia"
            },
            {
                "Continent": "Asia",
                "Country": "Indonesia"
            },
            {
                "Continent": "Asia",
                "Country": "Malaysia"
            },
            {
                "Continent": "Asia",
                "Country": "South Korea"
            },
            {
                "Continent": "South America",
                "Country": "Brazil"
            },
            {
                "Continent": "Asia",
                "Country": "Philippines"
            },
            {
                "Continent": "Asia",
                "Country": "Turkey"
            },
            {
                "Continent": "Asia",
                "Country": "Saudi Arabia"
            }
        ],
        "TotalCount": 15
    }
}
```


&nbsp;
