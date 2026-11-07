---
title: "DeleteSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteSharedConfig_jp"
---

既存のユニバーサルカタログを削除します。

<span id="前提条件"></span>
## 前提条件

ユニバーサルカタログを削除する前に、それがどのドメインにも関連付けられていないことを確認してください。ユニバーサルカタログを削除するには、以下の手順に従います：


1. [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_jp) を呼び出して、ユニバーサルカタログに関連付けられているドメインを取得します。

2. ユニバーサルカタログに関連付けられている**各**ドメインについて、以下の手順を実行します：

   1. [DuplicateTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/DuplicateTemplate_jp) を呼び出して、ドメインにバインドされている配信ポリシーをコピーします。

   2. 新しく作成されたポリシーについては、[UpdateServiceTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateServiceTemplate_jp) を呼び出してポリシーを変更し、関連する CDN 機能設定でユニバーサルカタログが参照されていないことを確認します。[ユニバーサルカタログ](https://docs.byteplus.com/en/docs/byteplus-cdn/universal-catalogue-jp) を参照して、ユニバーサルカタログを参照できる CDN 機能を確認できます。

   3. [UpdateTemplateDomain](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateTemplateDomain_jp) を呼び出して、新しく作成された配信ポリシーをドメインにバインドします。

3. DeleteSharedConfig を呼び出して、ユニバーサルカタログを削除します。


IAMユーザーがこの API を呼び出したときに「`The configuration is associated with domain names and cannot be deleted`」というエラーが表示され、IAMユーザーが [DescribeDomainShared](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_jp) を呼び出しても関連付けられたドメインが見つからない場合は、IAMユーザーにユニバーサルカタログが関連付けられているドメインへのアクセス権がない可能性があります。この場合、プライマリーアカウントがユニバーサルカタログとドメインの関連付けを解除する必要があり、その後、IAMユーザーはユニバーサルカタログを削除できます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDeleteSharedConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConfigName |String |はい |ユニバーサルカタログの名前を示します。[前提条件](https://docs.byteplus.com/en/docs/18/63582#%E5%89%8D%E6%8F%90%E6%9D%A1%E4%BB%B6) をご参照ください。 |`my_whitelist` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DeleteSharedConfig&Version=2021-03-01
```


&nbsp;
