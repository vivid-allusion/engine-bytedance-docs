---
title: "DescribeTemplates"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp"
---

フィルタ条件に一致するポリシーリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeTemplatesです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Filters |Object[] |いいえ |ポリシーリストを取得するためのフィルタ条件のセットを表します。フィルタ条件を指定しない場合、このAPIはアカウント配下のすべてのポリシーを返します。<br><br>複数のフィルタ条件間はAND関係となり、すべてのフィルタ条件を満たすポリシーのみがAPIのレスポンスに含まれます。<br><br>APIレスポンスで実際に返されるポリシーは、`PageNum`と`PageSize`の影響を受けます。 | |
|Fuzzy |Boolean |いいえ |マッチング方式を表します。このパラメータは以下の値を取ります：<br><br><br>* `true`：あいまいマッチングを表します。ポリシーマッチング時に、`Name`の対応する値が`Value`配列内の任意の値を含む場合、そのポリシーはフィルタ条件に一致すると見なされます。<br><br>* `false`：完全一致を表します。`Name`の対応する値が`Value`配列内の値と完全に一致する場合、そのポリシーはフィルタ条件に一致すると見なされます。<br><br><br>また、指定可能な`Fuzzy`の値は`Name`の値によって影響を受けます。`Name`の説明を参照してください。<br><br>このパラメータのデフォルト値は`false`です。<br><br>マッチングプロセスは大文字小文字を区することに注意してください。 | |
|Name |String |いいえ |フィルタタイプを表します。このパラメータは以下の値を取ります：<br><br><br>* `Title`：ポリシー名によるフィルタリングを表します。<br><br>* `Id`：IDによるポリシーのフィルタリングを表します。このパラメータ値では、`Fuzzy`の値は`false`のみ可能です。<br><br>* `Domain`：ドメイン名により、そのドメインにバインドされたポリシーをフィルタリングします。<br><br>* `Type`：タイプによるポリシーのフィルタリングを表します。このパラメータ値では、`Fuzzy`の値は`false`のみ可能です。<br><br>* `Status`：ステータスによるポリシーのフィルタリングを表します。このパラメータ値では、`Fuzzy`の値は`false`のみ可能です。<br><br><br>複数のフィルタ条件を同時に指定できますが、異なるフィルタ条件内の`Name`は同じにできません。 | |
|Value |String[] |いいえ |`Name`に対応する値を表し、配列です。<br><br><br>* `Name`が`Title`、`Id`、または`Domain`の場合、`Value`配列内の各値の長さは100文字以内である必要があります。<br><br>* `Name`が`Type`の場合、`Value`配列には以下の1つまたは複数の値を含めることができます：<br><br>   * `cipher`：暗号化ポリシーを表します。<br><br>   * `service`：配信ポリシーを表します。<br><br>   * `rule`：ルールエンジンポリシーを表します。<br><br>* `Name`が`Status`の場合、`Value`配列には以下の1つまたは複数の値を含めることができます：<br><br>   * `locked`：ステータスが「公開済み」を表します。<br><br>   * `editing`：ステータスが「下書き」を表します。<br><br><br>说明<br><br><br>* `Fuzzy`が`false`の場合、配列内に複数の値を指定できます。<br><br>* `Fuzzy`が`true`の場合、配列内に1つの値のみ指定できます。 | |
|PageNum |Long |いいえ |APIが返すポリシーリストに対して、このパラメータはページ番号を表します。このAPIは、指定されたページ番号のページに存在するポリシーを実際に返します。<br><br>このAPIが返すポリシーは`PageSize`によってページ分割されます。APIが返すポリシー数が100で、`PageSize`を`10`に指定した場合、返されるポリシーは10ページに分散されます。`PageNum`を`2`に指定した場合、2ページ目のポリシーを取得することを意味します。<br><br>指定したページにポリシーが存在しない場合、レスポンスの`Templates`パラメータの値は`null`となります。<br><br>`PageNum`のデフォルト値は`1`です。 |`1` |
|PageSize |Long |いいえ |各ページに含まれるポリシー数を表します。<br><br>このパラメータの値の範囲は1\-200で、デフォルト値は`10`です。 |`10` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Templates |Object[] |このAPIが返すポリシーリストを表します。<br><br>リスト内のポリシーは、リクエストパラメータ`PageNum`が示すページに存在するポリシーであり、必ずしもフィルタ条件に一致するすべてのポリシーではありません。 | |
|BoundDomains |Object[] |`TemplateId`で指定されたポリシーにバインドされているドメイン名リストを表します。<br><br>ポリシーがドメインにバインドされていない場合、このパラメータの値は`null`です。 | |
|BoundTime |Long |ポリシーが`Domain`で指定されたドメインにバインドされた時刻を表し、Unixタイムスタンプ形式です。 | |
|Domain |String |ポリシーにバインドされているドメイン名を表します。 | |
|CreateTime |Long |ポリシーの作成時刻を表し、Unixタイムスタンプ形式です。 | |
|Message |String |ポリシーの説明を表します。 | |
|Status |String |ポリシーのステータスを表します。このパラメータは以下の値を取ります：<br><br><br>* `locked`：ステータスが「公開済み」を表します。<br><br>* `editing`：ステータスが「下書き」を表します。 | |
|TemplateId |String |APIが返すポリシーリスト内のポリシーIDを表します。 | |
|Title |String |ポリシーの名前を表します。 | |
|Type |String |ポリシーのタイプを表します。このパラメータは以下の値を取ります：<br><br><br>* `cipher`：暗号化ポリシーを表します。<br><br>* `service`：配信ポリシーを表します。<br><br>* `rule`：ルールエンジンポリシーを表します。 | |
|UpdateTime |Long |ポリシーの最終更新時刻を表し、Unixタイムスタンプ形式です。<br><br>ポリシーが作成後更新されていない場合、このパラメータの値は`CreateTime`の値と同じです。 | |
|Exception |Boolean |ポリシーが特殊設定を含むかどうかを表します。特殊設定とは、ユーザーではなくBytePlusエンジニアが操作する設定を指します。このパラメータは以下の値を取ります：<br><br><br>* `true`：特殊設定を含むことを表します。<br><br>* `false`：特殊設定を含まないことを表します。 | |
|Project |String |ポリシーが所属するプロジェクトを表します。 | |
|ProdVersion |String |ポリシー配下で公開済み、つまりステータスが`running`のバージョンを表します。ステータスが`running`のバージョンが存在しない場合、このパラメータの値は空（""）です。 | |
|TotalCount |Long |フィルタ条件に一致するポリシー数を表します。このパラメータの値は`PageSize`と`PageNum`の影響を受けません。 |`2` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeTemplates&Version=2021-03-01
{
    "Filters": [
        {
            "Name": "Title",
            "Fuzzy": false,
            "Value": [
                "NetTVWeb001",
                "NetTV003"
            ]
        },
        {
            "Name": "Id",
            "Fuzzy": false,
            "Value": [
                "tpl-sZRpwq",
                "tpl-sWm5EW"
            ]
        },
        {
            "Name": "Domain",
            "Fuzzy": true,
            "Value": [
                "example.com"
            ]
        },
        {
            "Name": "Type",
            "Fuzzy": false,
            "Value": [
                "cipher",
                "service"
            ]
        },
        {
            "Name": "Status",
            "Fuzzy": false,
            "Value": [
                "locked",
                "editing"
            ]
        }
    ]
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403030536061418EF0E947E85EC76B6",
        "Action": "DescribeTemplates",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Templates": [
            {
                "BoundDomains": [
                    {
                        "BoundTime": 1709174039,
                        "Domain": "www.example.com"
                    }
                ],
                "CreateTime": 1709173909,
                "Exception": false,
                "Message": "",
                "Project": "default",
                "Status": "locked",
                "TemplateId": "tpl-sZRpwq",
                "Title": "NetTVWeb001",
                "Type": "service",
                "UpdateTime": 1709174039,
                "ProdVersion": "P-250411.32717"
            },
            {
                "BoundDomains": null,
                "CreateTime": 1709018409,
                "Exception": false,
                "Message": "Rewrite",
                "Project": "default",
                "Status": "editing",
                "TemplateId": "tpl-sWm5EW",
                "Title": "NetTV003",
                "Type": "service",
                "UpdateTime": 1709018409,
                "ProdVersion": ""
            }
        ],
        "TotalCount": 2
    }
}
```


&nbsp;
