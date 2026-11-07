---
title: "ListCdnDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCdnDomains_jp"
---

BytePlus CDN内のドメイン名リストと各ドメインの基本情報を取得します。これにはビジネスタイプ、実行ステータス、CNAMEアドレス、サービス地域などが含まれます。フィルタリング条件を指定してドメインリストをフィルタリングできます。詳細なドメイン設定を取得する場合は、[DescribeCdnConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_jp)を呼び出してください。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListCdnDomainsです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |いいえ |検索するドメイン名を表し、あいまい検索をサポートします。 |`example` |
|ServiceType |String |いいえ |ビジネスタイプを表し、ドメインをフィルタリングして該当ビジネスタイプのドメインを取得するために使用します。このパラメータには以下の値があります：<br><br><br>* `download`：ファイルダウンロードを表します。<br><br>* `web`：ウェブページを表します。<br><br>* `video`：オーディオビデオオンデマンドを表します。 |`web` |
|ResourceTags |String[] |いいえ |タグリストを表し、ドメインをフィルタリングしてリスト内の任意のタグを持つドメインを取得するために使用します。リストには最大10個のタグを含めることができ、各タグの形式は`key:value`です。このパラメータの例については右側の例を参照してください。 |`["key1:val1","key2:val2"]` |
|Status |String |いいえ |ドメインステータスを表し、ドメインをフィルタリングして該当ステータスのドメインを取得するために使用します。このパラメータには以下の値があります：<br><br><br>* `online`：ステータスが"オンライン"であることを表します。<br><br>* `configuring`：ステータスが"設定中"であることを表します。<br><br>* `offline`：ステータスが"オフライン"であることを表します。 |`offline` |
|Project |String |いいえ |プロジェクトを表し、そのプロジェクトに属するドメインを取得します。 |`default` |
|OriginProtocol |String |いいえ |プロトコルを表し、オリジンリクエストでこのプロトコルを使用するドメインを取得します。このパラメータには以下の値があります：<br><br><br>* `http`：HTTPプロトコルを表します。<br><br>* `https`：HTTPSプロトコルを表します。<br><br>* `followclient`：ユーザーリクエストで使用されるプロトコルを表します。 |`http` |
|IPv6 |Boolean |いいえ |IPv6機能が有効になっているかどうかに基づいてドメインをフィルタリングするかを表します。このパラメータには以下の値があります：<br><br><br>* `true`: IPv6が有効になっていることを表します。<br><br>* `false`: IPv6が有効になっていないことを表します。 |`true` |
|HTTPS |Boolean |いいえ |HTTPS暗号化サービスが有効になっているかどうかに基づいてドメインをフィルタリングするかを表します。このパラメータには以下の値があります：<br><br><br>* `true`: HTTPS暗号化サービスが有効になっていることを表します。<br><br>* `false`: HTTPS暗号化サービスが有効になっていないことを表します。 |`true` |
|PrimaryOrigin |String |いいえ |プライマリオリジンサーバーを表し、プライマリオリジンサーバー設定にこのサーバーが含まれているドメインを取得します。このパラメータの値はIPアドレスでもドメイン名でも構いません。 |`helloworld.example.com` |
|PageNum |Long |いいえ |ページ番号を表し、そのページ上のドメインリストを取得します。このパラメータのデフォルト値は`1`です。<br><br>CDNはフィルタリング条件に合致するドメインをページ分割します。応答パラメータ`Total`とリクエストパラメータ`PageSize`を使用して、このAPIが返すページ数を計算できます。 |`1` |
|PageSize |Long |いいえ |1ページに含まれるドメイン数を表します。このパラメータの値の範囲は1\-100で、デフォルト値は`10`です。 |`10` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|PageNum |Long |リクエストパラメータ内の`PageNum`を表します。 |`1` |
|PageSize |Long |リクエストパラメータ内の`PageSize`を表します。 |`10` |
|Total |Long |フィルタリング条件に合致するドメイン数を表します。このパラメータの値はリクエストパラメータ`PageSize`と`PageNum`の影響を受けません。 |`100` |
|Data |Object[] |フィルタリング条件に合致するドメインリストを表します。 | |
|Domain |String |リスト内の1つのドメインを表します。 |`www.example.com` |
|ServiceType |String |このドメインのビジネスタイプを表します。このパラメータには以下の値があります：<br><br><br>* `download`：ファイルダウンロードを表します。<br><br>* `web`：ウェブページを表します。<br><br>* `video`：オーディオビデオオンデマンドを表します。 |`web` |
|Status |String |このドメインのステータスを表します。このパラメータには以下の値があります：<br><br><br>* `online`：ステータスが"オンライン"であることを表します。<br><br>* `configuring`：ステータスが"設定中"であることを表します。<br><br>* `offline`：ステータスが"オフライン"であることを表します。 |`online` |
|Cname |String |CDNがこのドメインに割り当てたCNAMEを表します。 |`www.example.com.bpgslb.com` |
|ServiceRegion |String |このドメインのサービス地域を表します。このパラメータには以下の値があります：<br><br><br>* `chinese_mainland`：中国本土を表します。<br><br>* `global`：グローバルを表します。<br><br>* `outside_chinese_mainland`：中国本土を除くグローバルを表します。 |`domestic` |
|CreateTime |Long |このドメインがCDNに追加された日時を表し、Unixタイムスタンプ形式です。 |`1625587200` |
|UpdateTime |Long |このドメインの最終更新日時を表し、Unixタイムスタンプ形式です。更新操作にはドメインの有効化、無効化、ドメイン設定の変更などが含まれます。 |`1601371409` |
|Project |String |このドメインが属するプロジェクトを表します。 |`default` |
|OriginProtocol |String |オリジンリクエストで使用されるプロトコルを表します。このパラメータには以下の値があります：<br><br><br>* `http`：HTTPプロトコルを表します。<br><br>* `https`：HTTPSプロトコルを表します。<br><br>* `followclient`：ユーザーリクエストで使用されるプロトコルを表します。 |`http` |
|IPv6 |Boolean |このドメインでIPv6機能が有効になっているかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`: IPv6が有効になっていることを表します。<br><br>* `false`: IPv6が有効になっていないことを表します。 | |
|HTTPS |Boolean |このドメインでHTTPS暗号化サービスが有効になっているかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`: HTTPS暗号化サービスが有効になっていることを表します。<br><br>* `false`: HTTPS暗号化サービスが有効になっていないことを表します。 |`true` |
|PrimaryOrigin |String[] |このドメインに設定されたプライマリオリジンサーバーリストを表します。 |`1.2.3.4,2.3.4.5` |
|BackupOrigin |String[] |このドメインに設定されたバックアップオリジンサーバーリストを表します。このドメインにバックアップオリジンサーバーが設定されていない場合、このパラメータの値は`null`です。 |`1.2.3.4,2.3.4.5` |
|ResourceTags |Object[] |このドメインに付与されたタグリストを表します。このドメインにタグが付与されていない場合、このパラメータの値は`null`です。 | |
|Key |String |タグリスト内の1つのタグのkeyを表します。 |`userKey` |
|Value |String |このタグのvalueを表します。 |`userValue` |
|CacheShared |String |このドメインが共有キャッシュ設定内で果たす役割を表します。このパラメータには以下の値があります：<br><br><br>* `target_host`：共有キャッシュ設定が存在し、その設定内でこのドメインの役割がターゲットドメインであることを表します。<br><br>* `cache_shared_on`：共有キャッシュ設定が存在し、その設定内でこのドメインの役割が設定されたドメインであることを表します。<br><br>* `""`：このパラメータの値が空の場合、このドメインはどの共有キャッシュ設定にも存在しないことを表します。 |`target_host` |
|CacheSharedTargetHost |String |`CacheShared`が`cache_shared_on`の場合、このドメインとキャッシュを共有するターゲットドメインを表します。`CacheShared`が`target_host`または空の値（""）の場合、このパラメータの値は空（""）です。 |`www.example.net` |
|IsConflictDomain |Boolean |このドメイン名が競合ドメインであるかどうかを表します。デフォルトでは、各ドメイン名はコンテンツ配信ネットワーク内で一意です。既にコンテンツ配信ネットワークに存在するドメイン名を追加する必要がある場合、チケットを提出する必要があります。ドメインの追加が成功した場合、このドメインは競合ドメインとなります。<br><br>このパラメータには以下の値があります：<br><br><br>* `true`：このドメイン名が競合ドメインであることを表します。<br><br>* `false`：このドメイン名が競合ドメインではないことを表します。 |`false` |
|DomainLock |Object |このドメイン名のロックステータスを表します。 | |
|Remark |String |もし `Status` が `on` の場合、このパラメータ値はロックされた理由を記録しています。もし `Status` が `off` の場合、このパラメータ値は空（""）です。 |`域名锁定，不允许自助配置操作，域名下线` |
|Status |String |ドメインがロックされているかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `on`：このドメインがロックされていることを表します。<br><br>* `off`：このドメインがロックされていないことを表します。 |`on` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListCdnDomains&Version=2021-03-01
{
    "Domain": "example",
    "ResourceTags": [
        "key1:val1",
        "key2:val2"
    ]
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250821112545F5890E6D640605A33280",
        "Action": "ListCdnDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "BackupOrigin": [
                    "203.0.113.9",
                    "img2.example.com"
                ],
                "CacheShared": "",
                "CacheSharedTargetHost": "",
                "Cname": "www.example.com.bplslb.com",
                "CreateTime": 1755585663,
                "Domain": "www.example.com",
                "HTTPS": true,
                "IPv6": true,
                "OriginProtocol": "https",
                "PrimaryOrigin": [
                    "203.0.113.8",
                    "img.example.com",
                    "bpcntest.tos-ap-southeast-3.bytepluses.com",
                    "mybucket.oss-ap-southeast-1.aliyuncs.com",
                    "mybucket.cos.ap-singapore.myqcloud.com",
                    "my-bucket.s3.ap-southeast-1.amazonaws.com",
                    "myazstorage.blob.core.windows.net"
                ],
                "Project": "default",
                "ResourceTags": [
                    {
                        "Key": "mykey",
                        "Value": "myvalue"
                    }
                ],
                "ServiceRegion": "outside_chinese_mainland",
                "ServiceType": "web",
                "Status": "online",
                "UpdateTime": 1755585663,
                "Waf": false
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "Total": 1
    }
}
```


&nbsp;
