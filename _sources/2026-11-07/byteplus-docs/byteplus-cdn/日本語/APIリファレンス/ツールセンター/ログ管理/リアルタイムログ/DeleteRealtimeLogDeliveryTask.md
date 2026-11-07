---
title: "DeleteRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteRealtimeLogDeliveryTask_ja"
---

無効化されたリアルタイムログ配信タスクを削除します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DeleteRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDeleteRealtimeLogDeliveryTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TaskID |String |はい |削除するタスクのIDを示します。タスクの `Status` は `disable` である必要があります。<br><br>注意<br><br>配信先がTLSの場合、タスクを削除すると、対応するログトピックも削除されます。 |`b23298e8-c262-4cb6-8138-2c311230b972` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteRealtimeLogDeliveryTask&Version=2021-03-01
{
    "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
}
```


&nbsp;
