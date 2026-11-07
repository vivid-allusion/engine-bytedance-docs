---
title: "GetScriptSourceCode"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetScriptSourceCode_jp"
---

関数の最新バージョンのコードを取得します。このAPIはすべてのコードファイルのコードを返します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetScriptSourceCode&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は`GetScriptSourceCode`です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは`2021-03-01`です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|ScriptSourceCode |JSONMap |関数コード。 | |
|_key |String |コードファイルの名前。 |`test` |
|_value |String |コードファイルのコンテンツ。コードはBase64エンコード形式に変換されます。 |`LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetScriptSourceCode&Version=2021-03-01&FunctionId=3gyz993****
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "2022021014244901022524313903*****",
        "Action": "GetScriptSourceCode",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ScriptSourceCode": {
            "test": "LyoqCiAqIEFkZCB0aGUgbmVjZXNzYXJ5IGV2ZW50IGxpc3RlbmVyCiAqIEBwYXJhbSB7RXZlbnR9IGZldGNoIGV2ZW50LCB7RnVuY3Rpb259IGFzeW5jIGZ1bmN0aW9uCiAqLwphZGRFdmVudExpc3RlbmVyKCdmZXRjaCcsIGV2ZW50ID0+IHsKICBldmVudC5yZXNwb25kV2l0aChoYW5kbGVSZXF1ZXN0KGV2ZW50LnJlcXVlc3QpKTsKfSkKCi8qKgogKiBNYWtlIGEgcmVzcG9uc2UgdG8gY2xpZW50CiAqIEBwYXJhbSB7UmVxdWVzdH0gcmVxdWVzdAoKQHJldHVybiAqLwphc3luYyBmdW5jdGlvbiBoYW5kbGVSZXF1ZXN0KHJlcXVlc3QpIHsKICByZXR1cm4gbmV3IFJlc3BvbnNlKCdIZWxsbyBXb3JsZCEnLCB7IHN0YXR1czogMjAwIH0pOwp9Cg=="
        }
    }
}
```


&nbsp;
