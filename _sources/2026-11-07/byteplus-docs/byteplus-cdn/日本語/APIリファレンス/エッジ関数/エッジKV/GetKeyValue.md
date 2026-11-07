---
title: "GetKeyValue"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetKeyValue_jp"
---

キーバリューペアの値と有効期限を確認します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須かどうか |説明 |
|---|---|---|---|
|Action |String |はい |APIの名前。現在のAPIの名前は `GetKeyValue` です。 |
|Version |String |はい |APIのバージョン。現在のAPIのバージョンは `2021-03-01` です。 |
|Namespace |String |はい |ストレージスペースの名前。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |
|NamespaceId |String |はい |ストレージスペースのID。[ListKvNamespace](https://docs.byteplus.com/en/docs/byteplus-cdn/ListKvNamespace-jp)を呼び出して取得できます。 |
|Key |String |はい |値または有効期限を照会したいキー。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例値 |
|---|---|---|---|
|DDL |Long |キーバリューペアの有効期限。キーバリューペアが期限切れになると、関数はKeyのValueにアクセスできなくなります。<br><br><br>* 秒単位のUnixタイムスタンプ形式で表示されます。<br><br>* 0：期限切れなし。 |`0` |
|Key |String |照会したキー。 |`testkey` |
|Value |String |照会したキーの値。値はBase64エンコード形式です。 |`dGVzdHZhbHVlMTIz` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET   https://cdn.byteplusapi.com?Action=GetKeyValue&Version=2021-03-01&Namespace=test-kv1&NamespaceId=46d79a9944ae2fd81f2643e2fe5ef42d****&Key=testkey
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetKeyValue",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DDL": 0,
        "Key": "testkey",
        "Value": "dGVzdHZhbHVlMTIz"
    }
}
```


&nbsp;
