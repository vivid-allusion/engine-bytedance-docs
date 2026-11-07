---
title: "DeleteFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteFunction_jp"
---

指定された関数を削除します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエストの説明"></span>
## リクエストの説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=DeleteFunction&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPIの名前は `DeleteFunction` です。 |
|Version |String |はい |APIバージョン。現在のAPIのバージョンは `2021-03-01` です。 |


<span id="ボディパラメータ"></span>
### ボディパラメータ


|パラメータ |タイプ |必須 |説明 |サンプル値 |
|---|---|---|---|---|
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-jp)を呼び出して関数IDを取得できます。 |`3gyz993****` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
GET  https://cdn.byteplusapi.com?Action=DeleteFunction&Version=2021-03-01
{
  "FunctionId": "3gyz993****"
}
```
