---
title: "CreateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateKeyValue_jp"
---

名前空間にキーバリューペアを追加します。

<span id="使用制限"></span>
## 使用制限


* スロットリング制限: 1秒あたり最大20リクエストまで送信可能です。

* キーバリューペアの追加が成功した後、Keyは変更できません。

* 同じ名前空間内のKeyは重複できません。Keyは大文字小文字を区別しません。つまり`Key`と`KEY`は同じと見なされます。


<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`CreateKeyValue`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |


<span id="要求本文のパラメータ"></span>
### 要求本文のパラメータ


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Namespace |String |はい |名前空間の名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`test-kv1` |
|NamespaceId |String |はい |名前空間のID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |はい |キー。入力要件は以下の通りです:<br><br><br>* 英字、数字、ハイフン（\-）、アンダースコア（_）のみを含めることができます。<br><br>* 512バイトを超えないこと。 |`testkey` |
|Value |String |はい |値。入力要件は以下の通りです:<br><br><br>* Base64エンコード形式でのみ入力できます。<br><br>* 128KBを超えないこと。 |`dGVzdHZhbHVlMTIz` |
|TTL |Long |いいえ |キーバリューペアの有効期間を設定します。単位: 秒。キーバリューペアが期限切れになると、エッジ関数はKeyのValueを読み取れなくなります。<br><br><br>* このパラメータを指定しない、または値が0の場合は期限切れになりません。<br><br>* 有効期間は60秒以上である必要があります。 |`0` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST   https://cdn.byteplusapi.com?Action=CreateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdHZhbHVlMTIz",
    "TTL": 0
}
```
