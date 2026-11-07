---
title: "ListContinentCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListContinentCluster_jp"
---

カナリア環境またはフルリリース環境のエッジノードリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |APIの名前。現在のAPIの名前は `ListContinentCluster` です。 |
|Version |String |はい |APIのバージョン。現在のAPIのバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数のID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|Continents |String |いいえ |大陸を指定します。複数の大陸を指定する場合はカンマで区切ります。 |
|Countries |String |いいえ |国を指定します。複数の国を指定する場合はカンマで区切ります。 |
|ClusterType |Integer |いいえ |リリース環境のタイプ。<br><br><br>* 100：カナリア環境。<br><br>* 200：フルリリース環境。 |
|Page |Integer |いいえ |エッジノードリストのページ番号。<br><br>&nbsp;<br><br>PageパラメータとLimitパラメータの両方を指定しない場合、全データが返されます。Limitのみを指定し、Pageを指定しない場合、第1ページのデータが返されます。Pageのみを指定し、Limitを指定しない場合、全データが返されます。PageとLimitの両方を指定した場合、条件に合致するデータが返されます。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。現在、1ページあたり最大50レコードを取得できます。<br><br>&nbsp;<br><br>PageパラメータとLimitパラメータの両方を指定しない場合、全データが返されます。Limitのみを指定し、Pageを指定しない場合、第1ページのデータが返されます。Pageのみを指定し、Limitを指定しない場合、全データが返されます。PageとLimitの両方を指定した場合、条件に合致するデータが返されます。 |
|OrderBy |Integer |いいえ |エッジノードのソート方法。<br><br><br>* 1：降順でデータを並べ替えます。<br><br>* 2（デフォルト）：昇順でデータを並べ替えます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|ContinentCluster |Object[] |エッジノードリスト。 | |
|Country |String |エッジノードが存在する国または地域。 |`Singapore` |
|Continent |String |エッジノードが存在する大陸。 |`Asia` |
|ClusterType |Integer |エッジノードのタイプ。<br><br><br>* 100：カナリアリリースエッジノード<br><br>* 200：フルリリースエッジノード |`100` |
|Traffic |String |このエッジノードにデプロイされた関数のバージョン番号。 |`[{"version_tag":"1.0.1"}]` |
|TotalCount |Long |検索条件に一致するエッジノードの総数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListContinentCluster&Version=2021-03-01&FunctionId=b21f19d28c7f4fbbb8b8bc799f28****
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListContinentCluster",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ContinentCluster": [
            {
                "Continent": "Europe",
                "Country": "France",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Turkey",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Philippines",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Japan",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Malaysia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Saudi Arabia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "South America",
                "Country": "Brazil",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "South Korea",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Europe",
                "Country": "Russia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Thailand",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Indonesia",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "North America",
                "Country": "United States",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Singapore",
                "ClusterType": 200,
                "Traffics": ""
            },
            {
                "Continent": "Asia",
                "Country": "Vietnam",
                "ClusterType": 100,
                "Traffics": "[{\"version_tag\":\"1.0.1\"}]"
            },
            {
                "Continent": "Europe",
                "Country": "Germany",
                "ClusterType": 100,
                "Traffics": ""
            }
        ],
        "TotalCount": 15
    }
}
```


&nbsp;
