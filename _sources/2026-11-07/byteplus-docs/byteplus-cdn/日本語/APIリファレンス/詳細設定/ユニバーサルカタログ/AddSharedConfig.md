---
title: "AddSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/AddSharedConfig_jp"
---

ユニバーサルカタログを作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はAddSharedConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConfigName |String |はい |ユニバーサルカタログの名前を表します。名前には次の要件があります：<br><br><br>* 名には漢字、文字、数字、アンダースコア（_）を含めることができ、長さは3〜45文字です。漢字1文字は3文字としてカウントされます。<br><br>* プライマリーアカウントに既存のユニバーサルカタログの名前と同じにすることはできません。 |`my_list` |
|ConfigType |String |はい |このユニバーサルカタログのタイプを表します。このパラメータには次の値があります：<br><br><br>* `deny_ip_access_rule`：IPブロックリストを表します。<br><br>* `allow_ip_access_rule`：IPアローリストを表します。<br><br>* `deny_referer_access_rule`：Refererブロックリストを表します。<br><br>* `allow_referer_access_rule`：Refererアローリストを表します。<br><br>* `common_match_list`：汎用リストを表します。 |`allow_ip_access_rule` |
|AllowIpAccessRule |Object |いいえ |IPアローリストの設定を表し、`ConfigType`は`allow_ip_access_rule`に対応します。 | |
|Rules |String[] |いいえ |エントリのリストを表し、リスト内の各エントリはIPアドレスまたはCIDRブロックです。IPアドレスとCIDRブロックは、IPv4およびIPv6形式にすることができます。<br><br>リストのクォータは次のとおりです：<br><br><br>* リストには最大30,000エントリを含めることができます。<br><br><br>CDNがこのユニバーサルカタログを作成すると、リスト内の重複するエントリは削除されます。重複するエントリはクォータを消費しません。 |`["x.x.x.x","xx.xx.xx.xx/24"]` |
|AllowRefererAccessRule |Object |いいえ |Refererアローリストの設定を表し、`ConfigType`は`allow_referer_access_rule`に対応します。 | |
|AllowEmpty |Boolean |いいえ |Refererヘッダーが空（""）またはRefererヘッダーを含まないリクエストを許可しないかどうかを表します。このパラメータには次の値があります：<br><br><br>* `true`：許可しないことを表します。リクエストのRefererヘッダーが空（""）であるか、Refererヘッダーが含まれていない場合、CDNはリクエストを拒否します。<br><br>* `false`：許可することを表します。<br><br><br>このパラメータのデフォルト値は`false`です。 |`false` |
|CommonType |Object |いいえ |このRefererアローリストの内容を表します。 | |
|IgnoreCase |Boolean |いいえ |`Rules`のエントリで大文字と小文字を区別するかどうかを表します。このパラメータには次の値があります：<br><br><br>* `true`：大文字と小文字を区別しないことを表します。<br><br>* `false`：大文字と小文字を区別することを表します。<br><br><br>このパラメータのデフォルト値は`true`です。 |`true` |
|Rules |String[] |いいえ |エントリのリストを表し、リスト内の各エントリはドメイン名またはIPアドレスです。ドメイン名はワイルドカードドメインにすることができ、IPアドレスはIPv4およびIPv6形式にすることができます。<br><br>リストのクォータは次のとおりです：<br><br><br>* リストには最大4,000エントリを含めることができます。<br><br><br>CDNがこのユニバーサルカタログを作成すると、リスト内の重複するエントリは削除されます。重複するエントリはクォータを消費しません。 |`["xx.xx.xx.xx","*.example.com"]` |
|DenyIpAccessRule |Object |いいえ |IPブロックリストの設定を表し、`ConfigType`は`deny_ip_access_rule`に対応します。 | |
|Rules |String[] |いいえ |このパラメータの説明は、IPアローリストの`Rules`の説明と同じです。 |`["x.x.x.x","xx.xx.xxx.xx"]` |
|DenyRefererAccessRule |Object |いいえ |Refererブロックリストの設定を表し、`ConfigType`は`deny_referer_access_rule`に対応します。 | |
|AllowEmpty |Boolean |いいえ |Refererヘッダーが空（""）またはRefererヘッダーを含まないリクエストを許可するかどうかを表します。このパラメータには次の値があります：<br><br><br>* `true`：許可することを表します。<br><br>* `false`：許可しないことを表します。リクエストのRefererヘッダーが空（""）であるか、Refererヘッダーが含まれていない場合、CDNはリクエストを拒否します。<br><br><br>このパラメータのデフォルト値は`true`です。 |`true` |
|CommonType |Object |いいえ |このRefererブロックリストの内容を表します。 | |
|IgnoreCase |Boolean |いいえ |このパラメータの説明は、Refererアローリストの`IgnoreCase`の説明と同じです。 |`true` |
|Rules |String[] |いいえ |このパラメータの説明は、Refererアローリストの`Rules`の説明と同じです。 |`["x.x.x.xxx","*.example.com"]` |
|Project |String |いいえ |このユニバーサルカタログが属するプロジェクトの名前を表します。デフォルト値は`default`です。<br><br>[プロジェクト管理](https://console.byteplus.com/iam/resourcemanage/project)にアクセスして、作成済みのプロジェクトと各プロジェクトに含まれるリソースを表示できます。 |`default` |
|CommonMatchList |Object |いいえ |共通リストの設定を表し、`ConfigType`は`common_match_list`に対応します。 | |
|CommonType |Object |いいえ |この共通リストの内容を表します。 | |
|IgnoreCase |Boolean |いいえ |`Rules`のエントリで大文字と小文字を区別するかどうかを表します。このパラメータには次の値があります：<br><br><br>* `true`：大文字と小文字を区別しないことを表します。<br><br>* `false`：大文字と小文字を区別することを表します。<br><br><br>このパラメータのデフォルト値は`true`です。 |`true` |
|Rules |String[] |いいえ |エントリのリストを表し、リスト内の各エントリは文字列です。<br><br>リストのクォータは次のとおりです：<br><br><br>* リストには最大4,000エントリを含めることができます。<br><br>* すべてのエントリの合計長は200,000文字を超えることはできません。<br><br><br>CDNがこのユニバーサルカタログを作成すると、リスト内の重複するエントリは削除されます。重複するエントリはクォータを消費しません。 |`["param1","param2"]` |
|ExpireMinutes |Long |いいえ |有効期限が切れるまでの時間（分）。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=AddSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List",
    "ConfigType": "allow_referer_access_rule",
    "AllowRefererAccessRule": {
        "CommonType": {
            "Rules": [
                "xxx.xx.xxx.xxx",
                "www.example.com",
                "abc.example.com"
            ]
        }
    }
}
```


&nbsp;
