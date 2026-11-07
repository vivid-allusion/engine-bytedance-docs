---
title: "SnapshotPublish"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/SnapshotPublish_jp"
---

関数コードを指定したバージョンにロールバックします。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。また、各関数につき1秒あたり最大1リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=SnapshotPublish&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `SnapshotPublish` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp) を呼び出して、関数IDを取得できます。 |`3gyz993****` |
|VersionTag |String |はい |バージョン番号。[ListVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/ListVersions-jp) を呼び出して、バージョン番号を取得できます。 |`1.0.1` |
|PublishType |Integer |はい |公開タイプ：<br><br><br>* 200：全量公開<br><br>* 100：灰度公開 |`200` |
|Description |String |いいえ |今回の公開の説明情報を入力します。 |`test publish` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例 |
|---|---|---|---|
|TicketId |String |公開記録のID。 |`278335600748419****` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=SnapshotPublish&Version=2021-03-01
{
    "FunctionId": "3gyz993****",
    "PublishType": 200,
    "VersionTag": "1.0.1"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json

{
    "ResponseMetadata": {
        "RequestId": "202112072116030102251331430*****",
        "Action": "SnapshotPublish",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TicketId": "278335600748419****"
    }
}
```


&nbsp;
