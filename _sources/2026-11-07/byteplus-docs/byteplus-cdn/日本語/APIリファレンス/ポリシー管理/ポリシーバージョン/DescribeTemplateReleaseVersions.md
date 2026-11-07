---
title: "DescribeTemplateReleaseVersions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp"
---

指定されたポリシーのバージョンリストを取得します。追加のパラメータを指定して、バージョンリストをフィルタリングおよびソートできます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">各ポリシーは最大50個の公開済みバージョンを記録できます。</div>


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeTemplateReleaseVersionsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |バージョンリストを取得するポリシーのIDを示します。 |`tpl-s18ynd9`<br><br> |
|Filters |Object[] |いいえ |フィルタ条件のリストを示し、最大10個の条件を含めることができます。 | |
|Name |String |いいえ |フィルタ対象を示します。このパラメータには以下の値があります：<br><br><br>* `Status`：ポリシーのステータスを指定してバージョンリストをフィルタリングすることを示します。<br><br>* `Version`：バージョン番号を指定してバージョンリストをフィルタリングすることを示します。 |`Status` |
|Value |String[] |いいえ |フィルタ値のリストを示します。<br><br><br>* `Name`が`Status`の場合、以下のフィルタ値の1つまたは複数を指定できます：<br><br>* `stop`：ステータスが「停止」であることを示します。<br><br>* `running`：ステータスが「実行中」であることを示します。<br><br>* `draft`：ステータスが「ドラフト」であることを示します。<br><br>* `Name`が`Version`の場合、1つまたは複数のバージョン番号を指定でき、最大10個までです。 |`["stop","running"]`<br><br> |
|Fuzzy |Boolean |いいえ |マッチング方式を示します。このパラメータの値は`false`のみであり、完全一致を示します。<br><br>このパラメータのデフォルト値は`false`です。 |`false` |
|SortRule |Object |いいえ |ソート規則を示します。 | |
|OrderBy |String |いいえ |ソート対象を示します。このパラメータには以下の値があります：<br><br><br>* `CreateTime`：バージョンの作成時刻を示します。<br><br>* `ReleaseTime`：バージョンの最新公開時刻を示します。<br><br>* `Version`：バージョン番号を示します。 |`CreateTime`<br><br> |
|Asc |Boolean |いいえ |ソート順序を示します。このパラメータには以下の値があります：<br><br><br>* `false`：降順でソートすることを示します。<br><br>* `true`：昇順でソートすることを示します。<br><br><br>このパラメータのデフォルト値は`false`です。 |`false` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Total |Long |フィルタ条件に一致するバージョンの数を示します。 |`10` |
|Versions |Object[] |条件に一致するバージョンのリストを示します。 | |
|CreateTime |Long |このバージョンの作成時刻を示し、Unixタイムスタンプ形式です。 |`1744610623` |
|Env |String |このバージョンの公開環境を示します。<br><br><br>* `Status`が`draft`ではない場合、このパラメータの値は常に`prod`であり、本番環境を示します。<br><br>* `Status`が`draft`の場合、このパラメータの値は空（""）です。 |`prod` |
|Message |String |このバージョンの説明を示します。 |`my desc` |
|ReleaseTime |Long |このバージョンの最新公開時刻を示し、Unixタイムスタンプ形式です。 |`1744610623` |
|Status |String |このバージョンのステータスを示します。<br><br><br>* `stop`：ステータスが「停止」であることを示します。<br><br>* `running`：ステータスが「実行中」であることを示します。<br><br>* `draft`：ステータスが「ドラフト」であることを示します。 |`stop` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplateReleaseVersions&Version=2021-03-01
{
    "TemplateId": "tpl-s18ynd9",
    "Filters": [
        {
            "Name": "Status",
            "Value": [
                "stop",
                "running",
                "draft"
            ]
        }
    ],
    "SortRule": {
        "OrderBy": "CreateTime",
        "Asc": true
    }
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202504140728216B5EA730EF294C000118",
        "Action": "DescribeTemplateReleaseVersions",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Total": 3,
        "Versions": [
            {
                "CreateTime": 1744361302,
                "Env": "prod",
                "Message": "aaa",
                "ReleaseTime": 1744613891,
                "Status": "running",
                "Version": "P-250411.16282"
            },
            {
                "CreateTime": 1744364788,
                "Env": "prod",
                "Message": "sdfgh",
                "ReleaseTime": 1744599039,
                "Status": "stop",
                "Version": "P-250414.89520"
            },
            {
                "CreateTime": 1744610623,
                "Env": "",
                "Message": "",
                "ReleaseTime": 1744610623,
                "Status": "draft",
                "Version": "draft"
            }
        ]
    }
}
```


&nbsp;
