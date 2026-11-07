---
title: "CreateFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-CreateFunction-jp"
---

関数を作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエスト。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド：POST

* リクエストURL：https://cdn.byteplusapi.com?Action=CreateFunction&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPIの名前は `CreateFunction` です。 |
|Version |String |はい |APIバージョン。現在のAPIのバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Name |String |はい |関数名。命名規則は以下の通りです：<br><br><br>* 大文字、小文字、数字、ハイフン（\-）が使用可能。<br><br>* 名前は128文字を超えてはいけません。 |`test-Function` |
|ProjectName |String |いいえ |関数が属するプロジェクトの名前。デフォルト値は `default` です。 |`default` |
|Remark |String |いいえ |この関数の備考。入力要件は以下の通りです：<br><br><br>* 任意の文字が許可されます。<br><br>* 長さは128文字を超えてはいけません。 |`This is a test Function` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|FunctionId |String |関数のID。 |`3gyz993****` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
POST  https://cdn.byteplusapi.com?Action=CreateFunction&Version=2021-03-01
{
  "Name": "test-Function"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202404220916070BE49FB085D18E85BA26",
    "Action": "CreateFunction",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "FunctionId": "bc36dc7c58e942f0b9f125d186df****"
  }
}
```
