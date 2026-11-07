---
title: "UpdateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateCronJob_jp"
---

Cronトリガーを更新します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリ"></span>
### クエリ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |APIの名前。現在のAPIの名前は `UpdateCronJob` です。 |
|Version |String |はい |APIのバージョン。現在のAPIのバージョンは `2021-03-01` です。 |


<span id="ボディ"></span>
### ボディ


|パラメータ |タイプ |必須 |説明 |例 |
|---|---|---|---|---|
|FunctionId |String |はい |関数のID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |`3gyz993****` |
|JobName |String |はい |Cronトリガーの名前。 |`cron1` |
|CronExpression |String |はい |Cron式。 |`*/1 * * * *` |
|Parameter |String |いいえ |カスタムパラメータ。 |`cron` |
|Description |String |いいえ |トリガーの説明。 |`test` |
|CronType |Integer |はい |Cronトリガーの範囲。<br><br><br>* 1：グローバル。<br><br>* 2：単一ポイント。 |`1` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=UpdateCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1",
    "CronExpression":"*/1 * * * *",
    "Parameter":"cron_al",
    "Description":"",
    "CronType":1
}
```
