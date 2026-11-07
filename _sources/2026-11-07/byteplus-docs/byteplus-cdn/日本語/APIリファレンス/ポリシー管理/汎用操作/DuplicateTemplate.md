---
title: "DuplicateTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DuplicateTemplate_jp"
---

既存のポリシーをコピーして、設定が同一でタイプも同一のポリシーを作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDuplicateTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ReferredTemplateId |String |はい |コピー対象のポリシーのIDを表します。<br><br>[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)を使用して、コピーしたいポリシーのIDを取得できます。 |`tpl-sZRpwq` |
|Message |String |いいえ |作成するポリシーの説明を表し、文字数は120文字以内にする必要があります。 |`This is a dup policy.`<br><br> |
|Title |String |いいえ |作成するポリシーの名前を表し、文字数は100文字以内にする必要があります。<br><br>このパラメータが指定されていない場合、CDNはランダムな名前を生成します。 |`Dup_Policy` |
|Project |String |いいえ |作成するポリシーが所属するプロジェクトを表します。<br><br>このパラメータのデフォルト値は`default`で、Defaultプロジェクトを示します。 |`default` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TemplateId |String |作成するポリシーのIDを表します。 |`tpl-s2N4rW`<br><br> |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DuplicateTemplate&Version=2021-03-01
{
    "ReferredTemplateId": "tpl-sZRpwq",
    "Title": "Dup_Policy",
    "Message": "This is a dup policy."
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024030403552737EB957CFE0697DBB981",
        "Action": "DuplicateTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-s2N4rW"
    }
}
```


&nbsp;
