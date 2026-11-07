---
title: "DescribeCdnAccessLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnAccessLog_jp"
---

指定されたドメイン名のアクセスログを取得します。このAPIは、これらのアクセスログのダウンロードURLを返します。BytePLus CDNは毎時間、正確な時間で訪問ログをパッケージ化します。

データ保持期間：このAPIを呼び出す際は、指定する期間の時間幅が30日を超えないことをお勧めします。ログ数が膨大になるため、API呼び出しがタイムアウトする可能性があります。

ログ遅延：CDNはデフォルトで1時間粒度で、過去1時間に収集されたログをパッケージ化し、ログパッケージを生成します。ログパッケージは生成後約3時間でダウンロード可能になります。ネットワーク遅延などの理由により、CDNが収集したログには最大24時間の遅延が発生する可能性があります。収集された遅延ログに対して、CDNはそれを対応するログパッケージに追加します。そのため、ログパッケージは生成後24時間以内にログの追加が発生する可能性があります。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeCdnAccessLogです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |はい |ドメイン名を表します。このAPIは、そのドメイン名のアクセスログを取得します。 |`www.example.com` |
|ServiceRegion |String |いいえ |サービスリージョンを表し、アクセスログのフィルタリングに使用されます。このパラメータには以下の値があります：<br><br><br>* `chinese_mainland`：**中国本土**を表します。<br><br>* `global`： **グローバル** を表します。<br><br>* `outside_chinese_mainland`：\*\*グローバル（中国本土を除く）\*\*を表します。<br><br><br>このパラメータのデフォルト値は`global`です。 |`global` |
|StartTime |Long |はい |ログ統計期間の開始時刻を表し、時刻形式はUnixタイムスタンプです。留意すべき点は、`StartTime`はログ統計期間の実際の開始時刻ではありません。<br><br>実際の開始時刻は、`StartTime`を時間粒度で後方に切り上げた時刻です。<br><br>例：<br><br><br>* 指定した`StartTime`が示す時刻が15:07の場合、実際の開始時刻は16:00です。<br><br>* 指定した`StartTime`が示す時刻が15:00の場合、実際の開始時刻は15:00です。 |`1641844915` |
|EndTime |Long |はい |ログ統計期間の終了時刻を表し、時刻形式はUnixタイムスタンプです。留意すべき点は、`EndTime`はログ統計期間の実際の終了時刻ではありません。<br><br>実際の終了時刻は、`EndTime`を時間粒度で後方に切り上げた時刻です。 |`1641953589` |
|PageNum |Long |いいえ |ページ番号を表します。このAPIは、そのページ番号で指定されたページ上のログパッケージを返します。<br><br>このAPIが返すログパッケージは、`PageSize`に基づいてページ分割されます。このAPIが返すログパッケージ数が100で、指定した`PageSize`が`10`の場合、返されるログパッケージは10ページに分散されます。指定した`PageNum`が`2`の場合、2ページ目のログパッケージを取得することを意味します。<br><br>指定したページにログパッケージがない場合、返される結果の`DomainLogDetails`パラメータの値は`null`です。<br><br>`PageNum`のデフォルト値は`1`です。 |`1` |
|PageSize |Long |いいえ |各ページに含まれるログパッケージ数を表します。<br><br>このパラメータの値の範囲は1\-100で、デフォルト値は`10`です。 |`1` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|Domain |String |リクエストパラメータの`Domain`を表します。 |`www.a.com` |
|PageSize |Long |リクエストパラメータの`PageSize`を表します。 |`100` |
|PageNum |Long |リクエストパラメータの`PageNum`を表します。 |`1` |
|TotalCount |Long |フィルタリング条件に一致するログパッケージ数を表します。 |`100` |
|DomainLogDetails |Object[] |このAPIが返すログパッケージリストを表します。 | |
|LogName |String |リスト内の1つのログパッケージの名前を表します。名前の命名規則は<*Domain*\>_<*Start_Time*\>_<*End_Time*\>.gzです。<br><br>说明<br><br>ログパッケージ名では、`Start_Time`および`End_Time`のタイムゾーンはUTC+08:00です。 |`www.example.com_20210707100000_20210707110000.gz` |
|StartTime |Long |ログパッケージに対応するログ統計期間の実際の開始時刻を表し、形式はUnixタイムスタンプです。<br><br>`StartTime`と`EndTime`の間の時間間隔は1時間です。 |`1642392000` |
|EndTime |Long |ログパッケージに対応するログ統計期間の実際の終了時刻を表し、形式はUnixタイムスタンプです。 |`1642395600` |
|LogPath |String |ログパッケージのダウンロードURLを表します。ダウンロードURLの有効期間は24時間です。 |`https://cdnlog.bytedance.com/cdn-openapi/userlog/file-download/v1?fileName=www.example.com_20210707110000_20210707120000.gz&token=cecc2501edaecfc0141bce16f82e487c1fcb26ea3d393bd085a241be367e9875f059f695250d952e1c819b38fcdefd75` |
|LogSize |Long |ログパッケージのサイズを表し、単位は`bytes`です。<br><br>说明<br><br>ログパケットは生成後24時間以内に追加される可能性があるため、各API呼び出しで取得されるログパケットのサイズは異なる場合があります。最新のログパケットサイズをご参照ください。 |`9107` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021-03-01
{
    "PageSize": 10,
    "PageNum": 1,
    "Domain": "www.example.com",
    "StartTime": 1717236489,
    "EndTime": 1717409289,
    "ServiceRegion": "global"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202406031008365F2C63BC765D774E4A8C",
        "Action": "DescribeCdnAccessLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore"
    },
    "Result": {
        "Domain": "perfops2.byte-test.com",
        "DomainLogDetails": [
            {
                "EndTime": 1717401600,
                "LogName": "www.example.com_20240603150000_20240603160000_outsideChineseMainland.gz",
                "LogPath": "URL1",
                "LogSize": 4009503,
                "StartTime": 1717398000
            },
            {
                "EndTime": 1717398000,
                "LogName": "www.example.com_20240603140000_20240603150000.gz",
                "LogPath": "URL2",
                "LogSize": 849,
                "StartTime": 1717394400
            },
            {
                "EndTime": 1717398000,
                "LogName": "www.example.com_20240603140000_20240603150000_outsideChineseMainland.gz",
                "LogPath": "URL3",
                "LogSize": 3616460,
                "StartTime": 1717394400
            },
            {
                "EndTime": 1717394400,
                "LogName": "www.example.com_20240603130000_20240603140000.gz",
                "LogPath": "URL4",
                "LogSize": 1163,
                "StartTime": 1717390800
            },
            {
                "EndTime": 1717394400,
                "LogName": "www.example.com_20240603130000_20240603140000_outsideChineseMainland.gz",
                "LogPath": "URL5",
                "LogSize": 2958868,
                "StartTime": 1717390800
            },
            {
                "EndTime": 1717390800,
                "LogName": "www.example.com_20240603120000_20240603130000.gz",
                "LogPath": "URL6",
                "LogSize": 269,
                "StartTime": 1717387200
            },
            {
                "EndTime": 1717390800,
                "LogName": "www.example.com_20240603120000_20240603130000_outsideChineseMainland.gz",
                "LogPath": "URL7",
                "LogSize": 2630368,
                "StartTime": 1717387200
            },
            {
                "EndTime": 1717387200,
                "LogName": "www.example.com_20240603110000_20240603120000_outsideChineseMainland.gz",
                "LogPath": "URL8",
                "LogSize": 2584924,
                "StartTime": 1717383600
            },
            {
                "EndTime": 1717383600,
                "LogName": "www.example.com_20240603100000_20240603110000_outsideChineseMainland.gz",
                "LogPath": "URL9",
                "LogSize": 3587479,
                "StartTime": 1717380000
            },
            {
                "EndTime": 1717380000,
                "LogName": "www.example.com_20240603090000_20240603100000.gz",
                "LogPath": "URL10",
                "LogSize": 592,
                "StartTime": 1717376400
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "TotalCount": 50
    }
}
```


&nbsp;
