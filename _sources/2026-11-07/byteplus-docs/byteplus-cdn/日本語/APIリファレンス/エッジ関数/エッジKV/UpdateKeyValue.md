---
title: "UpdateKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateKeyValue_jp"
---

キーバリューペアの値と有効期間を変更します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限: 1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`UpdateKeyValue`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |


<span id="要求本文のパラメータ"></span>
### 要求本文のパラメータ


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Namespace |String |はい |名前空間の名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`test-kv1` |
|NamespaceId |String |はい |名前空間のID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Key |String |はい |値または保存時間を変更したいキー。API [ListKvKey](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvKey-jp)を呼び出して取得できます。 |`testkey` |
|Value |String |はい |新しい値を入力します。このパラメータを指定しない場合、元の値が保持されます。入力要件は次のとおりです：<br><br><br>* Base64エンコード形式のみ入力できます。<br><br>* 128KBを超えてはいけません。 |`dGVzdDEyMw==` |
|TTL |Long |はい |新しい有効期間を秒単位で入力します。キーバリューペアが期限切れになると、アクセスできなくなります。このパラメータを指定しない場合、元の値が保持されます。<br><br><br>* 0: 期限切れなし。<br><br>* 有効期間は60秒未満にすることはできません。 |`0` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateKeyValue&Version=2021-03-01
{
    "Namespace": "test-kv1",
    "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
    "Key": "testkey",
    "Value": "dGVzdDEyMw==",
    "TTL": 0
}
```


&nbsp;
