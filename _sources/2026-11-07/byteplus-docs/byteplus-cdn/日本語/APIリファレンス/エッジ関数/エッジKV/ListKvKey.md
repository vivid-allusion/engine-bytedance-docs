---
title: "ListKvKey"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvKey_jp"
---

名前空間内のキーバリューペアリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限: 1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`ListKvKey`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |
|Namespace |String |はい |名前空間の名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |
|NamespaceId |String |はい |名前空間のID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |
|Page |Integer |いいえ |ページ番号。 |
|Limit |Integer |いいえ |1ページあたりのレコード数。デフォルトは50件です。<br><br>最大50件まで。 |
|OrderBy |Integer |いいえ |このパラメータは、クエリするキーバリューペアの順序を指定し、以下の値を受け付けます：<br><br><br>* 1: キーバリューペアを降順で並べ替えます。<br><br>* 2（デフォルト）: キーバリューペアを昇順で並べ替えます。 |
|OrderType |String |いいえ |使用可能なソートタイプ：<br><br><br>* create_time（デフォルト）: 作成時間に基づいてキーバリューペアをソートします。<br><br>* update_time: 最終更新時間に基づいてキーバリューペアをソートします。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|NamespaceKeys |Object |名前空間内のキーバリューペアの詳細。 | |
|Namespace |String |キーバリューペアが属する名前空間の名前。 |`test-kv1` |
|NamespaceId |String |キーバリューペアが属する名前空間のID。 |`14776510402228****` |
|Key |String |キー。 |`testkey` |
|KeyStatus |Integer |キーバリューペアのステータス。<br><br><br>* 100: 期限切れ<br><br>* 200: 正常 |`200` |
|DDL |Long |キーバリューペアの有効期限。キーバリューペアが期限切れになると、KeyのValueにアクセスできなくなります。<br><br><br>* UNIXタイムスタンプ形式で表示されます。<br><br>* 0: 永久ストレージ。 |`0` |
|CreateTime |Long |キーバリューペアの作成時間。UNIXタイムスタンプ形式で表示されます。 |`1662005890` |
|UpdateTime |Long |キーバリューペアの更新時間。UNIXタイムスタンプ形式で表示されます。 |`1664337001` |
|TotalCount |Long |名前空間内のキーバリューペアの総数。 |`2` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListKvKey&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Page=1&Limit=10&OrderBy=2&OrderType=create_time
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "20230810210051741B321D8****",
        "Action": "ListKvKey",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "NamespaceKeys": [
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "testkey",
                "KeyStatus": 200, 
                "DDL": 0,
                "CreateTime": 1678085786,
                "UpdateTime": 1678085786
            },
            {
                "Namespace": "test-kv1",
                "NamespaceId": "14776510402****",
                "Key": "key",
                "KeyStatus": 100,
                "DDL": 1678259532,
                "CreateTime": 1678092385,
                "UpdateTime": 1682327035
            },
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
