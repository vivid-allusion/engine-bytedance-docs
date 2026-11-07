---
title: "ListCacheSharedDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCacheSharedDomains_jp"
---

作成済みの共有キャッシュ設定を取得します。フィルタリング条件を指定して、APIが返す設定をフィルタリングできます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListCacheSharedDomainsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|PrimaryDomain |String |いいえ |ドメイン名を示し、そのドメイン名をターゲットドメインとして使用する共有キャッシュ設定を取得します。<br><br>このパラメータを指定しない場合、このフィルタリング条件は指定されません。<br><br>`PrimaryDomain`と`SecondaryDomain`はどちらか一方しか指定できません。 |`example.com` |
|SecondaryDomain |String |いいえ |ドメイン名を示し、共有キャッシュドメイン名リストにそのドメイン名が含まれる共有キャッシュ設定を取得します。<br><br>このパラメータを指定しない場合、このフィルタリング条件は指定されません。 |`example.net` |
|ExactMatch |Boolean |いいえ |`PrimaryDomain`または`SecondaryDomain`を設定内のドメイン名と照合する際に、CDNが完全一致を使用するかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`：完全一致を使用することを示します。<br><br>* `false`：あいまい一致を使用することを示します。<br><br><br>このパラメータのデフォルト値は`false`です。 |`true` |
|PageSize |Long |いいえ |このAPIは取得した設定をページ分割します。このパラメータは、各ページに含まれる設定の数を示します。パラメータの範囲は1～100で、デフォルト値は`10`です。 |`10` |
|PageNum |Long |いいえ |どのページの設定を表示するかを示します。このパラメータのデフォルト値は`1`です。 |`1` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Data |Object[] |このAPIが返す共有キャッシュ設定のリストを示します。 | |
|CacheSharedOn |String |設定ドメイン名リストを示します。複数のドメイン名はカンマ（,）で区切られます。 |`www.example.com,abc.example.com` |
|TargetHost |String |ターゲットドメイン名を示します。 |`www.example.com` |
|UpdateTime |Long |この設定の最終更新時間を示し、形式はUnixタイムスタンプで、単位は秒です。 |`1755831922` |
|PageNumber |Long |指定した`PageNumber`を示します。 |`1` |
|PageSize |Long |指定した`PageSize`を示します。 |`10` |
|Total |Long |フィルタリング条件に一致する設定の数を示します。 |`3` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021-03-01
{
    "ExactMatch": false,
    "PrimaryDomain": "example"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910102143FC1FDB61C3CFED0130C4",
        "Action": "ListCacheSharedDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CacheSharedOn": "www.example.com,abc.example.com",
                "TargetHost": "www.example.net",
                "UpdateTime": 1755831922
            },
            {
                "CacheSharedOn": "docs.example.com",
                "TargetHost": "docs.example.net",
                "UpdateTime": 1749631703
            }
        ],
        "PageNumber": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
