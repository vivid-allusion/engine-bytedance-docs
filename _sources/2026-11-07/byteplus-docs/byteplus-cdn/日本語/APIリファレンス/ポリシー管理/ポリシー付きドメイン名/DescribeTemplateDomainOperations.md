---
title: "DescribeTemplateDomainOperations"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateDomainOperations_jp"
---

指定されたドメイン名の操作履歴を取得します。操作履歴には最大10件のレコードが含まれます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeTemplateDomainOperationsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |はい |照会するドメイン名を示します。 |`www.example.com` |
|PageSize |Long |いいえ |このAPIは取得したレコードをページ分割します。このパラメータは、各ページに含まれるレコード数を示します。パラメータの範囲は1～50で、デフォルト値は`10`です。 |`10` |
|PageNum |Long |いいえ |どのページのレコードを表示するかを示します。このパラメータの値は`1`のみ可能で、デフォルト値も`1`です。 |`1` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Operations |Object[] |指定されたドメイン名の操作履歴を示し、最大10件のレコードが含まれます。リスト内のレコードは`OperateTime`でソートされ、最初のレコードが最新の操作に対応します。 | |
|Action |String |記録された操作を示します。このパラメータには次の値があります：<br><br><br>* `create`：ドメイン名の作成を示します。<br><br>* `update`：設定の更新を示します。 |`create` |
|ConfigAfter |String |更新後のドメイン名設定を示し、以下の情報を含みます：<br><br><br>* 関連付けられた配信ポリシーID。<br><br>* 関連付けられた暗号化ポリシーID。<br><br>* 関連付けられたルールエンジンポリシーID。<br><br>* HTTPS暗号化サービスが有効になっているかどうか。<br><br>* 関連付けられた証明書ID。<br><br>* サービス地域。<br><br>* WAFが有効になっているかどうか。<br><br><br>このパラメータは、シリアル化されたドメイン名設定情報を含むJSON文字列です。 | |
|ConfigBefore |String |`Action`が`update`の場合、このパラメータは更新前のドメイン名設定を示します。`Action`が`create`の場合、このパラメータの値は`null`です。 | |
|OperateTime |Long |記録された操作時間を示し、形式はUnixタイムスタンプで、秒単位です。 |`1755314680` |
|Total |Long |操作履歴のレコード数を示します。 | |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateDomainOperations&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910092134B929D683A64BF500C428",
        "Action": "DescribeTemplateDomainOperations",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Operations": [
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747921048
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747921044
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747900254
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747900155
            },
            {
                "Action": "update",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"tpl-c18yw0o\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "OperateTime": 1747899947
            },
            {
                "Action": "create",
                "ConfigAfter": "{\"ServiceTemplateId\":\"tpl-s5o2jz6\",\"CipherTemplateId\":\"\",\"RuleTemplateIds\":[],\"HTTPSSwitch\":\"off\",\"CertId\":\"\",\"ServiceRegion\":\"outside_chinese_mainland\",\"WAFStatus\":\"off\"}",
                "ConfigBefore": "",
                "OperateTime": 1747795591
            }
        ],
        "Total": 6
    }
}
```


&nbsp;
