---
title: "LockTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/LockTemplate_jp"
---

ポリシーを公開します。これは、ステータスが`draft`のバージョンを公開することを意味します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このAPIはもうメンテナンスされていません。<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/ReleaseTemplate_jp">ReleaseTemplate</a>の使用をお勧めします。</div>


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=LockTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はLockTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |公開する必要があるポリシーのIDを表します。<br><br>[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)を使用して、公開したいポリシーのIDを取得できます。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=LockTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-s2N4rW"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "LockTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
