---
title: "UpdateCountryCluster"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCountryCluster_jp"
---

カナリア環境またはフルリリース環境のエッジノードを更新します。

<span id="使用制限"></span>
## 使用制限

リクエスト制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |APIの名前。現在のAPIの名前は `UpdateCountryCluster` です。 |
|Version |String |はい |APIのバージョン。現在のAPIのバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|FunctionId |String |はい |関数のID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|ClusterType |Integer |はい |リリース環境のタイプ。<br><br><br>* 100：カナリア環境。<br><br>* 200：フルリリース環境。 |
|Countries |String[] |はい |更新する国または地域のリスト。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```JSON
POST  https://cdn.byteplusapi.com?Action=UpdateCountryCluster&Version=2021-03-01
{
    "ClusterType": 200,
    "Countries": [
        "Singapore"
    ],
    "FunctionId": "3gyz993****",
}
```


&nbsp;
