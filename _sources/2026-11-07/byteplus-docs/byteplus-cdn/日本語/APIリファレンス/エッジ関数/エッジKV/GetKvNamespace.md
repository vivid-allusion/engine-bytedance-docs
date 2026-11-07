---
title: "GetKvNamespace"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetKvNamespace_jp"
---

名前空間の詳細情報を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限: 1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`GetKvNamespace`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |
|Namespace |String |はい |名前空間の名前。API[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |
|NamespaceId |String |はい |名前空間のID。API[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|Namespace |Object |名前空間の詳細。 | |
|Namespace |String |名前空間の名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`test-kv1` |
|NamespaceId |String |名前空間のID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |`46d79a9944ae2fd81f2643e2fe5ef42d****` |
|Description |String |名前空間の説明。 |`test` |
|Creator |String |名前空間の作成者。 |`testuser` |
|CreateTime |Long |作成時間。Unixタイムスタンプ（秒）形式。 |`1661864175` |
|UpdateTime |Long |更新時間。Unixタイムスタンプ（秒）形式。 |`1678288603` |
|ProjectName |String |名前空間が属するプロジェクトの名前。 |`default` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetKvNamespace&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "202308080952004CD21902****",
        "Action": "GetKvNamespace",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Namespace": {
            "Namespace": "test-kv1",
            "NamespaceId": "46d79a9944ae2fd81f2643e2fe5ef42d****",
            "Description": "test",
            "Creator": "testuser",
            "ProjectName": "default",
            "CreateTime": 1661864175,
            "UpdateTime": 1678288603
        }
    }
}
```
