---
title: "DeleteMultiKeys"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteMultiKeys_jp"
---

キーバリューペアを一括削除します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限: 1分あたり最大6リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com?Action=DeleteMultiKeys&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`DeleteMultiKeys`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |


<span id="要求本文のパラメータ"></span>
### 要求本文のパラメータ


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Namespace |String |はい |名前空間の名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`test-kv1` |
|NamespaceId |String |はい |名前空間のID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|KeyList |Array of strings |はい |削除するキーバリューペアのキー。 |`["key1","key2"]` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|DeleteResult |Object |削除結果。 | |
|FailedKeys |Array of strings |削除に失敗したキー。 |`["key1","key2"]` |
|SuccessfulCount |String |正常に削除されたキーの数。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=DeleteMultiKeys&Version=2021-03-01
{
  "Namespace": "test-kv1",
  "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
  "KeyList": [
    "key1",
    "key2"
  ]
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230808095102CFDFA3280****",
        "Action": "DeleteMultiKeys",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
        "Result": {
            "DeleteResult": {
                "FailedKeys": [
                    "key2"
                ],
                "SuccessfulCount": 1
            }
        }
}        
```
