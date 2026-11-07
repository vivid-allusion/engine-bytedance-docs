---
title: "ListKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace_jp"
---

エッジKV名前空間のリストを取得します。

<span id="使用制限"></span>
## 使用制限


* スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

* 1回のリクエストで最大1000個の名前空間を返します。


<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `ListKvNamespace` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例値 |
|---|---|---|---|---|
|PageNumber |Integer |いいえ |ページ番号。デフォルトは1です。 |`1` |
|PageSize |Integer |いいえ |1ページあたりのレコード数。デフォルトは10で、最大1000です。 |`10` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |
|---|---|---|
|Total |Integer |レコードの総数。 |
|PageNumber |Integer |現在のページ番号。 |
|PageSize |Integer |1ページあたりのレコード数。 |
|Namespaces |Object[] |名前空間のリスト。 |


<span id="namespaces"></span>
### Namespaces


|パラメータ |タイプ |説明 |
|---|---|---|
|Id |String |名前空間のID。 |
|Name |String |名前空間の名前。 |
|Description |String |名前空間の説明。 |
|CreateTime |Long |作成時刻。Unixタイムスタンプ形式。 |
|UpdateTime |Long |更新時刻。Unixタイムスタンプ形式。 |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
GET   https://cdn.byteplusapi.com?Action=ListKvNamespace&Version=2021-03-01
{
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024060411542001001002321000C1****",
        "Action": "ListKvNamespace",
        "Version": "2021-03-01",
        "Service": "cdn",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 2,
        "PageNumber": 1,
        "PageSize": 10,
        "Namespaces": [
            {
                "Id": "46d79a9944ae2fd81f2643e2fe5ef42d****",
                "Name": "test-kv1",
                "Description": "namespace 01",
                "CreateTime": 1717484060,
                "UpdateTime": 1717484060
            },
            {
                "Id": "56d79a9944ae2fd81f2643e2fe5ef42d****",
                "Name": "test-kv2",
                "Description": "namespace 02",
                "CreateTime": 1717484060,
                "UpdateTime": 1717484060
            }
        ]
    }
}
```


&nbsp;
