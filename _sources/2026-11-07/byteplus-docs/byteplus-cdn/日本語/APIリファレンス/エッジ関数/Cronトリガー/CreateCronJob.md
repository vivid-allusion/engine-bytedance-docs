---
title: "CreateCronJob"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateCronJob_jp"
---

Cronトリガーを作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20リクエストまで送信可能です。

<span id="リクエスト説明"></span>
## リクエスト説明


* Request Method：POST

* Request URL： https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |タイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名は `CreateCronJob` です。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは `2021-03-01` です。 |


<span id="要求本文のパラメータ"></span>
### 要求本文のパラメータ


|パラメータ |タイプ |必須 |説明 |例値 |
|---|---|---|---|---|
|FunctionId |String |はい |関数ID。[ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/ListFunction-jp)を呼び出して関数IDを取得できます。 |`3gyz993****` |
|JobName |String |はい |Cronトリガー名。名前は以下の要件を満たす必要があります：<br><br><br>* 各関数内のCronトリガー名は一意である必要があります。<br><br>* 名前の長さは128文字を超えることはできません。 |`cron1` |
|CronExpression |String |はい |Cron式。[サポートされるCron式](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers-jp#%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%82%8Bcron%E5%BC%8F)を参照してください。 |`*/1 * * **` |
|Parameter |String |いいえ |カスタムパラメータ。関数実行時に、エッジ関数はこのパラメータを関数コード内のCronEventオブジェクトに渡します。 |`cron` |
|Description |String |いいえ |Cronトリガーの説明。 |`test` |
|CronType |Integer |はい |Cronトリガーの範囲：<br><br>1：グローバル：すべてのエッジノードで実行。<br><br>2：単一ポイント：ランダムに任意のエッジノードで実行。 |`1` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

なし

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST  https://cdn.byteplusapi.com?Action=CreateCronJob&Version=2021-03-01
{
    "FunctionId":"3gyz993****",
    "JobName":"test1111",
    "CronExpression":"5 4 * * *",
    "Parameter":"fetch_1",
    "Description":"",
    "CronType":2
}
```


&nbsp;
