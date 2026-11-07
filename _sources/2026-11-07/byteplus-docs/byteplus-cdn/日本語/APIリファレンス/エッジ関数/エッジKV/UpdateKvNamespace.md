---
title: "UpdateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateKvNamespace_jp"
---

名前空間の説明を変更します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限: 1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`UpdateKvNamespace`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |


<span id="要求本文のパラメータ"></span>
### 要求本文のパラメータ


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Namespace |String |はい |名前空間の名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`test-kv1` |
|NamespaceId |String |はい |名前空間のID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |いいえ |名前空間の新しい説明情報、長さは80文字を超えてはいけません。このパラメータを指定しない場合、元の説明が保持されます。 |`test` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST   https://cdn.byteplusapi.com?Action=UpdateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Description": "test"
}
```
