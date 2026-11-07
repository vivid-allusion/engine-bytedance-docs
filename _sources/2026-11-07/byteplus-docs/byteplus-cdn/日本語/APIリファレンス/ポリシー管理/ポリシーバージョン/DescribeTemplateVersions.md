---
title: "DescribeTemplateVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateVersions_jp"
---

指定されたポリシーの系譜をたどり、作成履歴を取得します。現在、この API は最大 10 件のレコードを表示します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeTemplateVersionsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |系譜をたどるポリシーのIDを示します。 |`tpl-s5o2jz6` |
|PageSize |Long |いいえ |この API は取得したレコードをページ分割します。このパラメータは、各ページに含まれるレコード数を示します。このパラメータの値の範囲は 1～50 で、デフォルト値は `10` です。 |`10` |
|PageNum |Long |いいえ |どのページのレコードを表示するかを示します。このパラメータの値は `1` のみ可能で、デフォルト値も `1` です。 |`1` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Total |Long |この API が取得したレコードの総数を示します。 |`3` |
|Versions |Object[] |指定されたポリシーの作成履歴を示し、最大 10 件のレコードを含みます。リスト内のレコードは `OperateTime` でソートされ、最初のレコードが最新の操作に対応します。 | |
|Action |String |`ReferredId` が示すポリシーについて、このパラメータはそのポリシーに対する操作を示し、次の値を取ります：<br><br><br>* `create`：作成を示します。<br><br>* `duplicate`：複製を示します。 |`create` |
|OperateTime |Long |`Action` が発生した時刻を Unix タイムスタンプ形式（秒単位）で示します。 |`1757489199` |
|ReferredId |String |記録されたポリシーのソースを示します。<br><br><br>* `Action` が `duplicate` の場合、このパラメータは記録されたポリシーがどのポリシーから複製されたかを示します。<br><br>* `Action` が `create` の場合、このパラメータは記録されたポリシーの ID を示し、その意味は記録されたポリシーがゼロから作成されたということです。 |`tpl-sekkg4o` |
|Status |String |記録されたポリシーの状態を示します。このパラメータは次の値を取ります：<br><br><br>* `locked`：公開済みを示します。<br><br>* `editing`：下書きを示します。<br><br>* `deleted`：削除済みを示します。 |`locked` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

リクエスト例ではポリシー tpl\-s57n9yr の履歴を遡及しています。このポリシーの作成履歴は以下の通りです：


1. ゼロからポリシー tpl\-s5o2jz6 を作成し、公開しました。

2. tpl\-s5o2jz6 をコピーしてポリシー tpl\-sekkg4o を作成し、tpl\-sekkg4o を公開しました。

3. tpl\-sekkg4o をコピーしてポリシー tpl\-s57n9yr を作成しました。


```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s57n9yr"
}
```


<span id="レスポンス例"></span>
### レスポンス例

レスポンス例では tpl\-s57n9yr の作成履歴を表示されています。

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910081614E4D94A367CDBAF00B94E",
        "Action": "DescribeTemplateVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "Action": "duplicate",
                "OperateTime": 1757489199,
                "ReferredId": "tpl-sekkg4o",
                "Status": "locked"
            },
            {
                "Action": "duplicate",
                "OperateTime": 1757488579,
                "ReferredId": "tpl-s5o2jz6",
                "Status": "locked"
            },
            {
                "Action": "create",
                "OperateTime": 1747795522,
                "ReferredId": "tpl-s5o2jz6",
                "Status": "locked"
            }
        ]
    }
}
```


&nbsp;
