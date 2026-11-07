---
title: "DeleteTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteTemplate_jp"
---

ポリシーまたはポリシーの特定のバージョンを削除します。

 **ポリシーの削除**

ポリシーが削除されると、そのポリシーのすべてのバージョンが削除されます。

ポリシーを削除するには、そのポリシーがいかなるドメイン名にもバインドされていない必要があります。[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)を呼び出すことで、ポリシーがドメイン名にバインドされているかどうかを確認できます。そのポリシーの`BoundDomains`が`null`の場合のみ、そのポリシーを削除できます。

ポリシーが1つ以上のドメイン名にバインドされている場合は、これらのドメイン名から解約する必要があります。解約方法については、[UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateTemplateDomain_jp)の関連説明を参照してください。

 **ポリシーバージョンの削除**

公開されていないポリシーバージョンのみを削除できます。つまり、`Status`が`draft`または`stop`のバージョンのみを削除できます。ポリシー配下のすべてのバージョンと各バージョンの状態を取得するには、[DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp)を参照してください。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDeleteTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |削除するポリシーのIDを指定します。<br><br>削除したいポリシーのIDは、[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)を呼び出すことで取得できます。 |`tpl-s2N4rW` |
|TemplateVersion |String |いいえ |削除するバージョンを指定します。このバージョンのステータスは`running`であってはなりません。<br><br>ポリシー配下のすべてのバージョンと各バージョンのステータスは、[DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp)を呼び出すことで取得できます。 |`P-250414.89520` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-sqdYQ2",
    "TemplateVersion": "P-250414.89520"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "DeleteTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
