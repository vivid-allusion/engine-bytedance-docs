---
title: "GetSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetSourceCode_jp"
---

関数の最新バージョンのコードを取得します。このAPIはデフォルトのコードファイルのコードを返します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetSourceCode&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `GetSourceCode` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|SourceCode |String |コードコンテンツ。Base64エンコード形式。 |`"LyoqCiAqIEFkZCB0a******uIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="` |
|WasmSourceCode |String |.wasmファイルのコンテンツ。Base64エンコード形式。OPAタイプの関数のみこのパラメータを返します。 |`"AGFzbQEAAAABBwFgAn9/AX8DAgEABAUBcAEBAQUDAQAQBhkDfwFBgIDAAAt/AEGAgMAAC38AQYCAwAALBysEBm1lbW9yeQIAA2FkZAAACl9fZGF0YV9lbmQDAQtfX2hlYXBfYmFzZQMCCgkBBwAgASAAagsALwRuYW1lAAw*****3JlZmVyZW5jZS10eXBlcysIc2lnbi1leHQ="` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetSourceCode&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072138180102251100110****",
        "Action": "GetSourceCode",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "SourceCode": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAogKi8KYXN5bmMgZnVuY3Rpb24gaGFuZGxlUmVxdWVzdChyZXF1ZXN0KSB7CiAgcmV0dXJuIG5ldyBSZXNwb25zZSgnSGVsbG8gV29ybGQhJywgeyBzdGF0dXM6IDIwMCB9KTsKfQ=="
    }
}
```


&nbsp;
