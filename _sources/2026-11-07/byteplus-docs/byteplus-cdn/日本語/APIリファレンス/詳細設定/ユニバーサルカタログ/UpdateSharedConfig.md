---
title: "UpdateSharedConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateSharedConfig_jp"
---

ユニバーサルカタログを変更します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUpdateSharedConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConfigName |String |はい |ユニバーサルカタログの名前を表します。<br><br>既存のユニバーサルカタログ名は [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_jp) を呼び出すことで取得できます。 | |
|AllowIpAccessRule |Object |いいえ |IPアローリストの設定を表し、`ConfigType` は `allow_ip_access_rule` に対応します。 | |
|Option |String |いいえ |変更操作の種類を表します。このパラメータには、次の値を指定できます。<br><br><br>1. `overlap`：既存のエントリを完全に上書きすることを示します。<br><br>2. `add`：エントリを追加することを示します。<br><br>3. `delete`：指定したエントリを削除することを示します。<br><br><br>このパラメータのデフォルト値は `overlap` です。 | |
|Rules |String[] |いいえ |エントリのリストを表します。各エントリは、IPアドレスまたはCIDRブロックです。IPアドレスとCIDRブロックは、IPv4とIPv6の両方の形式をサポートします。<br><br>リストの制限は次のとおりです。<br><br><br>* `Option` が `overlap` の場合、リスト内のエントリ数は30,000を超えることはできません。<br><br>* `Option` が `add` の場合、リスト内のエントリと `ConfigName` 内の既存のエントリの合計が30,000を超えることはできません。詳細設定に既存のエントリ数を確認するには、[DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_jp) を呼び出します。<br><br><br>CDNが `ConfigName` を更新する際、リスト内の重複したエントリは削除されます。重複したエントリは制限にカウントされません。 | |
|AllowRefererAccessRule |Object |いいえ |Refererアローリストの設定を表し、`ConfigType` は `allow_referer_access_rule` に対応します。 | |
|AllowEmpty |Boolean |いいえ |Refererヘッダーが空（""）またはRefererヘッダーを含まないリクエストを許可するかどうかを示します。このパラメータには、次の値を指定できます。<br><br><br>* `true`：許可しないことを示します。リクエストのRefererヘッダーが空（""）であるか、またはRefererヘッダーが含まれていない場合、CDNはリクエストを拒否します。<br><br>* `false`：許可することを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|CommonType |Object |いいえ |このRefererアローリストのコンテンツを表します。 | |
|IgnoreCase |Boolean |いいえ |`Rules` のエントリで大文字と小文字を区別するかどうかを示します。このパラメータには、次の値を指定できます。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメータのデフォルト値は `true` です。 |`true` |
|Option |String |いいえ |このパラメータの説明は、IPアローリスト設定の `Option` の説明と同じです。 |`overlap` |
|Rules |String[] |いいえ |エントリのリストを表します。各エントリは、IPアドレスまたはドメイン名です。IPアドレスはIPv4とIPv6の両方の形式をサポートし、ドメイン名はワイルドカードドメイン名をサポートします。<br><br>リストの制限は次のとおりです。<br><br><br>* `Option` が `overlap` の場合、リスト内のエントリ数は4,000を超えることはできません。<br><br>* `Option` が `add` の場合、リスト内のエントリと `ConfigName` 内の既存のエントリの合計が4,000を超えることはできません。詳細設定に既存のエントリ数を確認するには、[DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_jp) を呼び出します。<br><br><br>CDNが `ConfigName` を更新する際、リスト内の重複したエントリは削除されます。重複したエントリは制限にカウントされません。 |`["1.1.1.22","*.example.com"]` |
|DenyIpAccessRule |Object |いいえ |IPブロックリストの設定を表し、`ConfigType` は `deny_ip_access_rule` に対応します。 | |
|Option |String |いいえ |このパラメータの説明は、IPアローリスト設定の `Option` の説明と同じです。 |`overlap` |
|Rules |String[] |いいえ |このパラメータの説明は、IPアローリストの `Rules` の説明と同じです。 |`["1.1.1.22","11.11.11.11","12.12.12.0/24"]` |
|DenyRefererAccessRule |Object |いいえ |Refererブロックリストの設定を表し、`ConfigType` は `deny_referer_access_rule` に対応します。 | |
|AllowEmpty |Boolean |いいえ |Refererヘッダーが空（""）またはRefererヘッダーを含まないリクエストを許可するかどうかを示します。このパラメータには、次の値を指定できます。<br><br><br>* `true`：許可することを示します。<br><br>* `false`：許可しないことを示します。リクエストのRefererヘッダーが空（""）であるか、またはRefererヘッダーが含まれていない場合、CDNはリクエストを拒否します。<br><br><br>このパラメータのデフォルト値は `true` です。 |`true` |
|CommonType |Object |いいえ |このRefererブロックリストのコンテンツを表します。 | |
|IgnoreCase |Boolean |いいえ |このパラメータの説明は、Refererアローリストの `IgnoreCase` の説明と同じです。 |`true` |
|Option |String |いいえ |このパラメータの説明は、IPアローリスト設定の `Option` の説明と同じです。 |`overlap` |
|Rules |String[] |いいえ |このパラメータの説明は、Refererアローリストの `Rules` の説明と同じです。 |`["1.1.1.22","*.example.com"]` |
|CommonMatchList |Object |いいえ |汎用リストの設定を表し、`ConfigType` は `common_match_list` に対応します。 | |
|CommonType |Object |いいえ |この汎用リストのコンテンツを表します。 | |
|IgnoreCase |Boolean |いいえ |`Rules` のエントリで大文字と小文字を区別するかどうかを示します。このパラメータには、次の値を指定できます。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメータのデフォルト値は `true` です。 |`false` |
|Option |String |いいえ |このパラメータの説明は、IPアローリスト設定の `Option` の説明と同じです。 |`overlap` |
|Rules |String[] |いいえ |エントリのリストを表します。各エントリは文字列です。<br><br>リストの制限は次のとおりです。<br><br><br>* `Option` が `overlap` の場合、リスト内のエントリ数は4,000を超えることはできず、すべてのエントリの合計長は200,000文字を超えることはできません。<br><br>* `Option` が `add` の場合、リスト内のエントリと `ConfigName` 内の既存のエントリの合計が4,000を超えることはできません。詳細設定に既存のエントリ数を確認するには、[DescribeSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeSharedConfig_jp) を呼び出します。<br><br><br>CDNが `ConfigName` を更新する際、リスト内の重複したエントリは削除されます。重複したエントリは制限にカウントされません。 |`["param1","param2"]` |
|ExpireMinutes |Long |いいえ |期限切れまでの時間（分）。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateSharedConfig&Version=2021-03-01
{
    "ConfigName": "My_List",
    "DenyRefererAccessRule": {
        "CommonType": {
            "Option": "add",
            "Rule": [
                "xx.xxx.xxx.xx",
                "xxx.xxx.xxx.xx"
            ]
        }
    }
}
```


&nbsp;
