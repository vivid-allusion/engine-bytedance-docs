---
title: "CreateTemplateVersion"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_jp"
---

ポリシーの下書きバージョンを作成します。


* デフォルトでは、このAPIは現在公開されているバージョンに基づいて下書きバージョンを作成し、コンソールの「バージョン作成」操作に対応します。作成された下書きバージョンは、現在公開されているバージョンと同じ設定を持ちます。

* 既存のバージョンを指定して下書きバージョンを作成することもでき、コンソールの「バージョンコピー」操作に対応します。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">下書きバージョンを既に含むポリシーに対してこのAPIを呼び出すことはできません。</div>


<div data-tips="true" data-tips-type="tip">指定されたポリシーに下書きバージョンが含まれているかどうかを判断するには、指定されたポリシーに対して<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp">DescribeTemplateReleaseVersions</a>を呼び出すことができます。APIが返すバージョンリストで、<code>Status</code>が<code>draft</code>のバージョンが存在するかを確認してください。</div>


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はCreateTemplateVersionです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |下書きバージョンを作成する必要があるポリシーのIDを示します。 |`tpl-s18ynd9` |
|Message |String |いいえ |この下書きバージョンの説明を示します。 |`my desc`<br><br> |
|ReferredVersion |String |いいえ |既存のバージョンのIDを示します。このAPIはこのバージョンに基づいて下書きバージョンを作成します。<br><br>このパラメータの値は`draft`にすることはできず、デフォルト値は現在公開されているバージョンのIDです。<br><br>[DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp)を呼び出して、このポリシー配下のすべてのバージョンを取得できます。 |`P-250414.89520`<br><br> |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=CreateTemplateVersion&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Message": "Hello World",
    "ReferredVersion": "P-250414.89520"
}
```


&nbsp;
