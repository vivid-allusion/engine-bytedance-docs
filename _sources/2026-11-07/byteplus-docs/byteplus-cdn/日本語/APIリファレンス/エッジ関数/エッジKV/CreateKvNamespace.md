---
title: "CreateKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateKvNamespace_jp"
---

名前空間を作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限: 1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`CreateKvNamespace`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |


<span id="要求本文のパラメータ"></span>
### 要求本文のパラメータ


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Namespace |String |はい |名前空間に識別可能な名前を設定します。入力要件は以下の通りです:<br><br><br>* 長さは2から64文字の間であること。<br><br>* 英字、数字、ハイフン(\-)、アンダースコア(_)のみを含めることができる。<br><br>* 大文字小文字を区別しないため、「Namespace」と「NAMESPACE」は同じと見なされます。また、エッジ関数は大文字小文字を変換しません。 |`test-kv1` |
|Description |String |いいえ |名前空間の説明を設定します。長さは80文字を超えないこと。 |`test` |
|ProjectName |String |いいえ |名前空間が属するプロジェクト名。デフォルトは`default`です。 |`default` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST   https://cdn.byteplusapi.com?Action=CreateKvNamespace&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "Description": "test",
    "ProjectName": "default"
}
```
