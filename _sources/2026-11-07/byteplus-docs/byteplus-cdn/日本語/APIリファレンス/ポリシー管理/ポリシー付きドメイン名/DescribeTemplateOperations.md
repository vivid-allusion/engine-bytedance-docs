---
title: "DescribeTemplateOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateOperations_jp"
---

指定されたポリシーの操作履歴を取得します。操作履歴には最大10件のレコードが含まれます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeTemplateOperationsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |照会するポリシーIDを示します。 |`tpl-s5wzdn0` |
|PageSize |Long |いいえ |このAPIは取得したレコードをページ分割します。このパラメータは、各ページに含まれるレコード数を示します。パラメータの範囲は1～50で、デフォルト値は`10`です。 |`10` |
|PageNum |Long |いいえ |どのページのレコードを表示するかを示します。このパラメータの値は`1`のみ可能で、デフォルト値も`1`です。 |`１` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Operations |Object[] |指定されたポリシーの操作履歴を示し、最大10件のレコードが含まれます。リスト内のレコードは`OperateTime`でソートされ、最初のレコードが最新の操作に対応します。 | |
|Action |String |記録された操作を示します。このパラメータには次の値があります：<br><br><br>* `bind`：ドメイン名の関連付けを示します。<br><br>* `create`：ポリシーの作成を示します。<br><br>* `release`：ポリシーのリリースを示します。 |`bind` |
|DomainsAfter |Object[] |`Action`が`bind`の場合、このパラメータは関連付けられたドメイン名情報を示します。`Action`が`bind`でない場合、このパラメータの値は`null`です。 | |
|Domain |String |関連付けられたドメイン名を示します。 |`www.example.com` |
|DomainsBefore |Object[] |`Action`が`bind`の場合、このパラメータは関連付け前にポリシーが関連付けられていたドメイン名情報を示します。<br><br>以下のいずれかの場合、このパラメータの値は`null`です：<br><br><br>* `Action`が`bind`でない。<br><br>* 記録された操作が最初のドメイン名関連付けです。 | |
|Domain |String |関連付け操作前にポリシーが関連付けられていたドメイン名を示します。 |`abc.example.com` |
|OperateTime |Long |記録された操作時間を示し、形式はUnixタイムスタンプで、秒単位です。 |`1755314680` |
|Total |Long |操作履歴のレコード数を示します。 |`3` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateOperations&Version=2021-03-01
{
    "TemplateId": "tpl-s5wzdn0"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910090657D2AD1B292BAAA8BF5384",
        "Action": "DescribeTemplateOperations",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Operations": [
            {
                "Action": "release",
                "DomainsAfter": [
                    {
                        "Domain": "www.example.com"
                    }
                ],
                "DomainsBefore": [
                    {
                        "Domain": "abc.example.com"
                    }
                ],
                "OperateTime": 1755323476
            },
            {
                "Action": "bind",
                "DomainsAfter": [
                    {
                        "Domain": "abc.example.com"
                    }
                ],
                "DomainsBefore": null,
                "OperateTime": 1755314680
            },
            {
                "Action": "release",
                "DomainsAfter": null,
                "DomainsBefore": null,
                "OperateTime": 1755312538
            },
            {
                "Action": "create",
                "DomainsAfter": null,
                "DomainsBefore": null,
                "OperateTime": 1755309241
            }
        ],
        "Total": 4
    }
}
```


&nbsp;
