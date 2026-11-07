---
title: "FullPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/FullPublish_jp"
---

関数に対してフルリリースを行います。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。また、各関数につき1秒あたり最大1リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=FullPublish&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `FullPublish` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp) を呼び出して、関数IDを取得できます。 |`3gyz993****` |
|Description |String |いいえ |今回の公開の説明情報を入力します。 |`test publish` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|TicketId |Long |公開記録のID。 |`146023529142213****` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=FullPublish&Version=2021-03-01
{
    "FunctionId": "3246574",
    "Description": "test publish"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "FullPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "146023529142213****"
    }
}
```


&nbsp;
