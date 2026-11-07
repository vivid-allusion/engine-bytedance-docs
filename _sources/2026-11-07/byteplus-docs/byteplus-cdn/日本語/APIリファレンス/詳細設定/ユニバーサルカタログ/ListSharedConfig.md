---
title: "ListSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_jp"
---

指定されたクエリ条件に基づいて、条件を満たすユニバーサルカタログのリストを取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListSharedConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConfigName |String |いいえ |ユニバーサルカタログの名前を表し、この名前に完全に一致するユニバーサルカタログを取得するために使用されます。 |`my_whitelist` |
|ConfigType |String |いいえ |ユニバーサルカタログのタイプを表し、このタイプのユニバーサルカタログのリストを取得するために使用されます。このパラメータには次の値があります：<br><br><br>* `deny_ip_access_rule`：IPブロックリストを表します。<br><br>* `allow_ip_access_rule`：IPアローリストを表します。<br><br>* `4xx_error_page`: カスタムエラーページを表します。<br><br>* `deny_referer_access_rule`：Refererブロックリストを表します。<br><br>* `allow_referer_access_rule`：Refererアローリストを表します。<br><br>* `common_match_list`：汎用リストを表します。 |`allow_ip_access_rule` |
|PageNum |Long |いいえ |ページ番号を表します。CDNは`PageSize`に基づいて、クエリ条件を満たすユニバーサルカタログのリストをページ分割します。このAPIが返すユニバーサルカタログの数が100で、`PageSize`が`10`であると仮定すると、これらのユニバーサルカタログは10ページに分散されます。CDNはデフォルトで1ページ目のユニバーサルカタログを表示します。<br><br>このパラメータのデフォルト値は`1`です。 |`1` |
|PageSize |Long |いいえ |各ページに含まれるユニバーサルカタログの数を表します。<br><br>このパラメータの値の範囲は1～1,000で、デフォルト値は`10`です。 |`10` |
|Project |String |いいえ |プロジェクト名を表し、このプロジェクトに属するユニバーサルカタログのリストを取得するために使用されます。 |`default` |
|ConfigTypeList |String[] |いいえ |1つ以上のユニバーサルカタログのタイプを表し、これらのタイプのユニバーサルカタログのリストを取得するために使用されます。このパラメータ値は、`ConfigType`の使用可能な値の組み合わせにすることができます。`ConfigType`と`ConfigTypeList`を同時に指定することはできません。 |`["allow_ip_access_rule","deny_ip_access_rule"]` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|ConfigData |Object[] |クエリ条件を満たすユニバーサルカタログのリストを表します。 | |
|ConfigName |String |リスト内のグローバル設定の名前を表します。 |`my_whitelist` |
|ConfigType |String |このグローバル設定のタイプを表します。このパラメータには次の値があります：<br><br><br>* `deny_ip_access_rule`：IPブロックリストを表します。<br><br>* `allow_ip_access_rule`：IPアローリストを表します。<br><br>* `4xx_error_page`: カスタムエラーページを表します。<br><br>* `deny_referer_access_rule`：Refererブロックリストを表します。<br><br>* `allow_referer_access_rule`：Refererアローリストを表します。<br><br>* `common_match_list`：共通リストを表します。 |`deny_ip_access_rule` |
|DomainCount |Long |このグローバル設定に関連付けられているドメイン名の数を表します。 |`2` |
|Project |String |このグローバル設定が属するプロジェクトを表します。 |`default` |
|UpdateTime |Long |このグローバル設定の最終更新時刻をUnixタイムスタンプで表します。 |`1655856000` |
|PageNum |Long |リクエストパラメータで指定した`PageNum`を表します。 |`1` |
|PageSize |Long |リクエストパラメータで指定した`PageSize`を表します。 |`10` |
|Total |Long |クエリ条件を満たすユニバーサルカタログの総数を表します。 |`20` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListSharedConfig&Version=2021-03-01
{
    "ConfigType": "allow_ip_access_rule"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240117195639014D4059167D42B2C640",
        "Action": "ListSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigData": [
            {
                "ConfigName": "deny_ip",
                "ConfigType": "deny_ip_access_rule",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705492181
            },
            {
                "ConfigName": "error_page",
                "ConfigType": "4xx_error_page",
                "DomainCount": 1,
                "Project": "default",
                "UpdateTime": 1705334019
            },
            {
                "ConfigName": "common_list",
                "ConfigType": "common_match_list",
                "DomainCount": 0,
                "Project": "default",
                "UpdateTime": 1705332721
            },
            {
                "ConfigName": "deny_referer",
                "ConfigType": "deny_referer_access_rule",
                "DomainCount": 3,
                "Project": "default",
                "UpdateTime": 1702484378
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 34
    }
}
```


&nbsp;
