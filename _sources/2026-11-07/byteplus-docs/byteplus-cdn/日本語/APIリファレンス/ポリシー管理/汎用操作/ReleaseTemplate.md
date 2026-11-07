---
title: "ReleaseTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ReleaseTemplate_jp"
---

ポリシーの指定バージョンを公開します。


* 公開するバージョンのステータスが`draft`の場合、このAPI操作はコンソールでの"公開"操作に対応します。

* 公開するバージョンのステータスが`stop`の場合、このAPI操作はコンソールでの"ロールバック"操作に対応します。


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はReleaseTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |公開するバージョンが存在するポリシーIDを表します。 |`tpl-s18ynd9` |
|Env |String |いいえ |公開環境を表します。現在、このパラメータ値は`prod`のみで、本番環境を表します。このパラメータのデフォルト値も`prod`です。 |`prod` |
|Message |String |いいえ |公開操作の説明を表します。 |`My Desc` |
|TemplateVersion |String |いいえ |公開するバージョン番号を表します。このパラメータのデフォルト値は`draft`です。 |`P-250411.16282` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ReleaseTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "TemplateVersion": "P-250411.16282"
}
```


&nbsp;
