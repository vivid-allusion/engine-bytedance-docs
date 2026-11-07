---
title: "UpdateFunction"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateFunction_jp"
---

関数の名前または説明を更新します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエストの説明"></span>
## リクエストの説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateFunction&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API 名称。現在のAPIの名前は `UpdateFunction` です。 |
|Version |String |はい |API バージョン。現在のAPIのバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-jp)を呼び出して関数IDを取得できます。 |`3gyz993****` |
|Name |String |はい |新しい関数名。名前は以下の要件を満たす必要があります：<br><br><br>* 英字、数字、ハイフン（\-）のみを含むことができます。<br><br>* 長さは128文字以内でなければなりません。 |`test-Function2` |
|Remark |String |いいえ |関数の備考。入力要件は次のとおりです：<br><br><br>* 任意の文字を使用できます。<br><br>* 長さは80文字を超えてはいけません。<br><br>* このフィールドを使用しない場合は、変更されません。このフィールドの値が入力されていない場合、説明は空に変更されます。 |`This is a test Function` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com/?Action=UpdateFunction&Version=2021-03-01
{
  "FunctionId": "bc36dc7c58e942f0b9f125d186df54d9",
  "Name": "test-doc",
  "Remark": ""
}
```
