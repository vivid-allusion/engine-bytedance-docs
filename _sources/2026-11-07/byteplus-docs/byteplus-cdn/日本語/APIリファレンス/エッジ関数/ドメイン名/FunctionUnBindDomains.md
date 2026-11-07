---
title: "FunctionUnBindDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/FunctionUnBindDomains_jp"
---

ドメイン名と関数の関連付けを解除します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=FunctionUnBindDomains&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `FunctionUnBindDomains` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domains |String[] |はい |関連付けを解除するドメイン名を入力します。[ListFunctionDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunctionDomains_jp) を呼び出して、利用可能なCDNドメイン名リストを取得できます。 |`["test1.example.com","test2.example.com"]` |
|FunctionId |String |はい |関連付けを解除する関数IDを入力します。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp) を呼び出して、FunctionIdを取得できます。 |`3gyz993****` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=FunctionUnBindDomains&Version=2021-03-01
{
  "FunctionId": "b21f19d28c7f4fbbb8b8bc799f28****",
  "Domains":[
    "a.example.com",
    "b.example.com"
    ]
}
```
