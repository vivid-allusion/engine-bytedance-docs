---
title: "GetCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/GetCronJob_jp"
---

Cronトリガーの詳細情報を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：GET

* Request URL： https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `GetCronJob` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |
|JobName |String |はい |トリガー名。 |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |タイプ |説明 |例値 |
|---|---|---|---|
|Job |Object[] |Cronトリガーリスト。 |`Task details` |
|JobName |String |トリガー名。 |`cron2` |
|CronExpression |String |Cron式。 |`*/1 * * **` |
|Parameter |String |カスタムパラメータ。 |`cron` |
|Description |String |Cronトリガーの説明。 |`test` |
|JobState |Long |Cronトリガーの状態。<br><br><br>* 1：実行待ち<br><br>* 3：無効<br><br>* 4：キャンセル |`1` |
|CronType |Integer |Cronトリガーの範囲。<br><br><br>* 1：グローバル。<br><br>* 2：単一ノード。 |`1` |
|CreateTime |Long |作成時間。 |`1638326159` |
|UpdateTime |Long |更新時間。 |`1638326159` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```HTTP
GET https://cdn.byteplusapi.com?Action=GetCronJob&Version=2021-03-01&FunctionId=3gyz993****&JobName=cron2
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
  "ResponseMetadata": {
    "RequestId": "20211207213413010225146063****",
    "Action": "GetCronJob",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "Job": {
      "JobName": "cron2",
      "CronExpression": "*/59 * * * *",
      "Parameter": "cron_all",
      "Description": "",
      "JobState": 1,
      "CronType": 2,
      "Operator": "****",
      "CreateTime": 1638871686,
      "UpdateTime": 1638871686
    }
  }
}
```


&nbsp;
