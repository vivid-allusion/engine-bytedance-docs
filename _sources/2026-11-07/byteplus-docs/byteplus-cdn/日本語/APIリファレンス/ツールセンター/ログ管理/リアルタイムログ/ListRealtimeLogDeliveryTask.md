---
title: "ListRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_ja"
---

リアルタイムログ配信タスクのリストを取得します。一連のフィルタ条件を指定して、タスクリストをフィルタリングできます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListRealtimeLogDeliveryTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Desc |String |いいえ |`Desc` をフィルタ条件として指定し、あいまい一致をサポートします。 |`my` |
|Domain |String |いいえ |ドメインをフィルタ条件として指定し、そのドメインのログを配信するタスクを取得します。 |`www.example.com` |
|Status |String |いいえ |タスクのステータスをフィルタ条件として指定します。このパラメータには次の値があります：<br><br><br>* `enable`: 有効を示します。<br><br>* `disable`: 無効を示します。 |`enable` |
|TaskID |String |いいえ |タスクIDをフィルタ条件として指定します。 |`33a1f4df-f384-453e-9d59-3e9ff4b04b4e` |
|TaskType |String |いいえ |配信先をフィルタ条件として指定します。このパラメータには次の値があります：<br><br><br>* `tls`：BytePlus Log Service（TLS）を示します。<br><br>* `sls`：Alibaba Cloud Log Service（SLS）を示します。<br><br>* `http_server`：HTTPサーバーを示します。 |`tls` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TaskInfo |Object[] |フィルタ条件に一致するタスクのリストを示します。 | |
|Area |String |このパラメータ値は常に `outside_chinese_mainland` です。 |`outside_chinese_mainland` |
|CreateTime |Long |タスクの作成時間を示します。形式はUnixタイムスタンプです。 |`1761816153` |
|Desc |String |タスクの説明を示します。 |`myDesc` |
|Domain |String |タスクに関連付けられているドメイン名のリスト、つまりタスクが配信するログのドメイン名を示します。 |`www.example.com` |
|HttpServer |Object |`TaskType` が `http_server` の場合、この構造体はHTTPサーバー側の対応する設定を示します。 | |
|AuthMechanism |Boolean |HTTPサーバーで認証が有効になっているかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |CDNがログを配信する際に使用する圧縮アルゴリズムを示します。このパラメータには次の値があります：<br><br><br>* `gzip`：Gzip圧縮アルゴリズムを示します。<br><br><br>このパラメータ値が空（""）の場合、圧縮は使用されません。 |`gzip` |
|RequestHeader |Object[] |CDNがHTTPサーバーにログを配信する際に、リクエストに含める追加のヘッダーのリストを示します。 | |
|Key |String |リスト内のヘッダーのキーを示します。 |`key1` |
|Value |String |`Key` の値を示します。 |`value1` |
|SecretKey |String |トークンを計算するための認証キーを示します。このパラメータは `AuthMechanism` が `true` の場合にのみ有効です。<br><br>認証プロセスとトークンアルゴリズムの詳細については、[タスク設定](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_jp) を参照してください。 |`xxxxxxxxxxx` |
|Url |String |HTTPサーバーのアクセスポイント、ポート、およびログの保存パスを示します。 |`http://www.example.com:8080/mylog` |
|SampleRate |Double |ログのサンプリングレートを示します。 |`50` |
|Sls |Object |`TaskType` が `sls` の場合、この構造体はSLS側の対応する設定を示します。 | |
|AccessKeyId |String |Alibaba CloudアカウントのAccessKey IDを示します。 |`xxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |Alibaba CloudアカウントのAccessKey Secretを示します。 |`xxxxxxxxxxxxx` |
|Endpoint |String |`Project` のパブリックドメイン名を示します。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |ログを保存するLogStoreを示します。 |`my_store` |
|Project |String |`LogStore` が属するログプロジェクトを示します。 |`my_project` |
|Status |String |タスクのステータスを示します。このパラメータには次の値があります：<br><br><br>* `enable`：タスクが有効であることを示します。<br><br>* `disable`：タスクが無効であることを示します。 |`enable` |
|StatusDetail |Object[] |タスクで最近発生した例外のリストを示します。リストには最大10個の例外が記録されます。 | |
|Detail |String |例外の詳細を示します。 |`exception details` |
|Time |Long |例外が発生した時間を示します。形式はUnixタイムスタンプです。 |`1761815000` |
|TaskID |String |タスクのIDを示します。 |`42de0332-b6e0-4fe1-9a5a-847bb7471def` |
|TaskType |String |配信先を示します。以下の値があります：<br><br><br>* `tls`：BytePlus Log Service（TLS）を示します。<br><br>* `sls`：Alibaba Cloud Log Service（SLS）を示します。<br><br>* `http_server`：HTTPサーバーを示します。 |`tls` |
|Tls |Object |`TaskType` が `tls` の場合、この構造体はTLS側の対応する設定を示します。 | |
|Endpoint |String |`Project` のパブリックドメイン名を示します。 |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |ログトピックが属するログプロジェクトIDを示します。このプロジェクトは `Endpoint` に対応する配信リージョンにあります。 |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|ProjectName |String |ログトピックが属するログプロジェクト名を示します。 |`test` |
|Region |String |ログプロジェクトが配置されているリージョンを示します。 |`ap-southeast-1` |
|TopicID |String |ログを保存するログトピックIDを示します。 |`b23298e8-c262-4cb6-8138-2c311230b972` |
|TopicName |String |ログを保存するログトピックの名前を示します。 |`test4` |
|Ttl |Long |ログの保存期間を日で示します。<br><br>このパラメータ値が `3650` の場合、ログは永久に保存されます。 |`3` |
|UpdateTime |Long |タスクの最終更新時間を示します。形式はUnixタイムスタンプです。 |`1761816153` |
|Total |Long |リスト内のタスクの数を示します。 |`3` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Desc": "my",
    "Domain": "www.example.com",
    "TaskType": "tls",
    "Status": "enable",
    "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20251030175056FC7B92C49D1494225A51",
        "Action": "ListRealtimeLogDeliveryTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskInfo": [
            {
                "Area": "outside_chinese_mainland",
                "CreateTime": 1761816153,
                "Desc": "myDesc",
                "Domain": "www.example.com",
                "HttpServer": null,
                "SampleRate": 100,
                "Sls": null,
                "Status": "enable",
                "StatusDetail": [],
                "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972",
                "TaskType": "tls",
                "Tls": {
                    "Endpoint": "tls-ap-southeast-1.volces.com",
                    "ProjectID": "a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747",
                    "ProjectName": "test",
                    "Region": "ap-southeast-1",
                    "TopicID": "b23298e8-c262-4cb6-8138-2c311230b972",
                    "TopicName": "test4",
                    "Ttl": 7
                },
                "UpdateTime": 1761816153
            }
        ],
        "Total": 1
    }
}
```


&nbsp;
