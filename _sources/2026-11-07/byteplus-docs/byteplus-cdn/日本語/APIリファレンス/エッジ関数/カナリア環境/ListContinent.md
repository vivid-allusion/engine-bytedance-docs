---
title: "ListContinent"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListContinent_jp"
---

指定された関数に対して、利用可能なエッジノードが存在する大陸のリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListContinent&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |APIの名前。現在のAPIの名前は `ListContinent` です。 |
|Version |String |はい |APIのバージョン。現在のAPIのバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数のID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |サンプル値 |
|---|---|---|---|
|Continents |String[] |大陸のリスト。 |`["Asia"]` |


<span id="サンプル"></span>
## サンプル

<span id="リクエストサンプル"></span>
### リクエストサンプル

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListContinent&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="レスポンスサンプル"></span>
### レスポンスサンプル

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListContinent",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Continents": [
            "Asia"
        ]
    }
}
```


&nbsp;
