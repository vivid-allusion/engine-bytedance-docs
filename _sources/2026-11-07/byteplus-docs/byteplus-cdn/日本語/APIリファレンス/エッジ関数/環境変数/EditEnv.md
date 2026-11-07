---
title: "EditEnv"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/EditEnv_jp"
---

関数の環境変数を更新します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">環境変数の追加、削除、変更操作は、関数が再度リリースされた後に有効になります。</div>


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=EditEnv&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `EditEnv` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |`23455331245` |
|Envs |Object[] |はい |環境変数。 |`[{"Key": "abc","Value": "123"}]` |
|Key |String |はい |環境変数のキー。 |`a` |
|Value |String |はい |環境変数の値。 |`a` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=EditEnv&Version=2021-03-01
{
    "FunctionId": "23455331245",
    "Envs": [
        {
            "Key": "abc",
            "Value": "123"
        }
    ]
}
```


&nbsp;
