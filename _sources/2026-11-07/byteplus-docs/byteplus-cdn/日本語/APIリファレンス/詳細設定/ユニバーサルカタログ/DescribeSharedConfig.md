---
title: "DescribeSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_jp"
---

ユニバーサルカタログの設定を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeSharedConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConfigName |String |いいえ |ユニバーサルカタログの名前を表します。 |`my_whitelist` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|AllowIpAccessRule |Object |IPアローリストの設定を表し、`ConfigType` は `allow_ip_access_rule` に対応します。 | |
|Rules |String[] |このIPアローリストのエントリを表します。 |`["10.10.10.10","192.168.1.1"]` |
|AllowRefererAccessRule |Object |Refererアローリストの設定を表し、`ConfigType` は `allow_referer_access_rule` に対応します。 | |
|AllowEmpty |Boolean |Refererヘッダーが空（""）またはRefererヘッダーを含まないリクエストを許可しないかどうかを表します。このパラメータには、次の値があります：<br><br><br>* `true`：許可しないことを表します。リクエストのRefererヘッダーが空（""）であるか、Refererヘッダーが含まれていない場合、CDNはリクエストを拒否します。<br><br>* `false`：許可することを表します。 |`true` |
|CommonType |Object |このRefererアローリストのコンテンツを表します。 | |
|IgnoreCase |Boolean |`Rules` のエントリで大文字と小文字を区別するかどうかを表します。このパラメータには、次の値があります：<br><br><br>* `true`：大文字と小文字を区別しないことを表します。<br><br>* `false`：大文字と小文字を区別することを表します。 |`true` |
|Rules |String[] |このRefererアローリストのエントリを表します。 |`["1.1.1.1","*.ww.com","aaa.ww.com"]` |
|ConfigName |String |このユニバーサルカタログの名前を表します。 |`my_whitelist` |
|ConfigType |String |このユニバーサルカタログのタイプを表します。このパラメータには、次の値があります：<br><br><br>* `deny_ip_access_rule`：IPブロックリストを表します。<br><br>* `allow_ip_access_rule`：IPアローリストを表します。<br><br>* `deny_referer_access_rule`：Refererブロックリストを表します。<br><br>* `allow_referer_access_rule`：Refererアローリストを表します。<br><br>* `common_match_list`：汎用リストを表します。<br><br>* `4xx_error_page`：カスタムエラーページを表します。 |`allow_ip_access_rule` |
|DenyIpAccessRule |Object |IPブロックリストの設定を表し、`ConfigType` は `deny_ip_access_rule` に対応します。 | |
|Rules |String[] |このIPブロックリストのエントリを表します。 |`["10.10.10.10","192.168.1.1"]` |
|DenyRefererAccessRule |Object |Refererブロックリストの設定を表し、`ConfigType` は `deny_referer_access_rule` に対応します。 | |
|AllowEmpty |Boolean |Refererヘッダーが空（""）またはRefererヘッダーを含まないリクエストを許可するかどうかを表します。このパラメータには、次の値があります：<br><br><br>* `true`：許可することを表します。<br><br>* `false`：許可しないことを表します。リクエストのRefererヘッダーが空（""）であるか、Refererヘッダーが含まれていない場合、CDNはリクエストを拒否します。 |`true` |
|CommonType |Object |このRefererブロックリストのコンテンツを表します。 | |
|IgnoreCase |Boolean |このパラメータの説明は、Refererアローリストの `IgnoreCase` の説明と同じです。 |`true` |
|Rules |String[] |このRefererブロックリストのエントリを表します。 |`["1.1.1.1","*.ww.com","aaa.ww.com"]` |
|Project |String |このユニバーサルカタログが属するプロジェクト名を表します。 |`default` |
|CommonMatchList |Object |共通リストの設定を表し、`ConfigType` は `common_match_list` に対応します。 | |
|CommonType |Object |この共通リストのコンテンツを表します。 | |
|IgnoreCase |Boolean |このパラメータの説明は、Refererアローリストの `IgnoreCase` の説明と同じです。 |`true` |
|Rules |String[] |この共通リストのエントリを表します。 |`["abc","param"]` |
|ErrorPageRule |Object |カスタムエラーページの設定を表します。 | |
|RuleContent |String |このカスタムエラーページのHTMLコードを表します。 |`<html><head><title>Test</title></head><body><h1>Header</h1>Hello World</body></html>` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209082302440129758BDA68D5D9AF",
        "Action": "DescribeSharedConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AllowRefererAccessRule": {
            "AllowEmpty": false,
            "CommonType": {
                "IgnoreCase": true,
                "Rules": [
                    "xxx.xx.xxx.xxx",
                    "www.example.com",
                    "abc.example.com"
                ]
            }
        },
        "CommonMatchList": null,
        "ConfigName": "My_List",
        "ConfigType": "allow_referer_access_rule",
        "Project": "default"
    }
}
```


&nbsp;
