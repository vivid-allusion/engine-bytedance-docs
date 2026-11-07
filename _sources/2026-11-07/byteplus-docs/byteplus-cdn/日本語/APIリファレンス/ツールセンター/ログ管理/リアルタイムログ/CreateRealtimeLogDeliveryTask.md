---
title: "CreateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateRealtimeLogDeliveryTask_ja"
---

CDNでリアルタイムログ配信タスクを作成します。マスターアカウントには最大20個のタスクを作成できます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はCreateRealtimeLogDeliveryTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Area |String |はい |どのサービスリージョン内のCDNノードからログを収集するかを示します。現在、このパラメータ値は `outside_chinese_mainland` のみ可能で、グローバル（中国本土を除く）を表します。 |`outside_chinese_mainland` |
|Domain |String |はい |どのドメイン名のリアルタイムログを配信するか、つまりタスクが関連付けられるドメイン名を示します。<br><br><br>* アカウント内のすべてのドメイン名を関連付ける場合は、`*` を渡してください。ここでのすべてのドメイン名には、後でCDNに追加するドメイン名も含まれます。<br><br>* 指定したドメイン名を関連付ける場合は、関連付けるドメイン名のリストを渡してください。リストには最大200個のドメイン名を含めることができ、複数のドメイン名はカンマ（,）で区切ります。<br><br><br>注意<br><br>アカウント内のすべてのドメイン名を関連付けるタスクを既に作成している場合、指定したドメイン名を関連付けるタスクをさらに作成することはできません。逆も同様です。<br><br>[ListRealtimeLogDeliveryTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_ja) を呼び出し、このドメイン名をフィルタ条件として指定することで、ドメインがタスクに関連付けられているかどうかを確認できます。 |`www.example.com,img.example.com` |
|TaskType |String |はい |配信先を示します。以下の値があります：<br><br><br>* `tls`：BytePlus Log Service（TLS）を示します。<br><br>* `sls`：Alibaba Cloud Log Service（SLS）を示します。<br><br>* `http_server`：HTTPサーバーを示します。 |`sls` |
|Desc |String |いいえ |タスクの説明を示します。このパラメータの入力要件は次のとおりです：<br><br><br>* 長さは3～64文字で、中国語、英字、数字、アンダースコア（_）、ハイフン（\-）を含めることができます。中国語は3文字としてカウントされます。<br><br>* ハイフン（\-）またはアンダースコア（_）で開始または終了することはできません。 |`my desc` |
|HttpServer |Object |いいえ |`TaskType` が `http_server` の場合、この構造体はHTTPサーバー側の対応する設定を示します。 | |
|AuthMechanism |Boolean |いいえ |HTTPサーバーで認証が有効になっているかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |いいえ |CDNがログを配信する際に使用する圧縮アルゴリズムを示します。このパラメータには次の値があります：<br><br><br>* `gzip`：Gzip圧縮アルゴリズムを示します。<br><br><br>このパラメータが指定されていない場合、圧縮は使用されません。 |`gzip` |
|RequestHeader |Object[] |いいえ |CDNがHTTPサーバーにログを配信する際に、リクエストに含める必要がある追加のヘッダーのリストを示します。リストには最大10個のヘッダーを含めることができます。<br><br>このパラメータが指定されていない場合、リクエストに追加のヘッダーは追加されません。 | |
|Key |String |いいえ |リスト内のヘッダーのキーを示します。長さは1,024文字を超えることはできません。`Key` は `User-Agent` であってはならず、`x-bdcdn-` で始まってはなりません。 |`mykey` |
|Value |String |いいえ |`Key` の値を示します。長さは1,024文字を超えることはできません。 |`myvalue` |
|SecretKey |String |いいえ |トークンを計算するための認証キーを示します。このパラメータの長さは6～40文字です。<br><br>`AuthMechanism` が `true` の場合、`SecretKey` を指定する必要があります。<br><br>認証プロセスとトークンアルゴリズムの詳細については、[タスク設定](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_jp) を参照してください。 |`xxxxxxxxxx` |
|Url |String |いいえ |HTTPサーバーのアクセスポイント、ポート、およびログの保存パスを示します。ポートはオプションです。アクセスポイントは `http://` または `https://` で始まる必要があり、長さは1,024文字を超えることはできません。 |`https://www.example.com:8080/cdn-logs` |
|SampleRate |Double |いいえ |ログのサンプリングレートを示します。範囲は0.00～100.00で、小数点以下2桁までです。<br><br>サンプリングレートとは、配信されるログの割合を指します。たとえば、サンプリングレートを10に設定すると、CDNノードで100件のログが収集されるごとに、CDNはランダムに10件のログを選択して指定した場所に配信します。 |`50.55` |
|Sls |Object |いいえ |`TaskType` が `sls` の場合、この構造体はSLS側の対応する設定を示します。 | |
|AccessKeyId |String |いいえ |Alibaba CloudアカウントのAccessKey IDを示します。長さは128文字を超えることはできません。 |`xxxxxxxxxxxx` |
|AccessKeySecret |String |いいえ |Alibaba CloudアカウントのAccessKey Secretを示します。長さは128文字を超えることはできません。 |`xxxxxxxxx` |
|Endpoint |String |いいえ |`Project` のパブリックドメイン名を示します。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |いいえ |ログを保存するLogStoreを示します。 |`myStore` |
|Project |String |いいえ |`LogStore` が属するログプロジェクトを示します。 |`myProject` |
|Tls |Object |いいえ |`TaskType` が `tls` の場合、この構造体はTLS側の対応する設定を示します。 | |
|Endpoint |String |いいえ |`Project` のパブリックドメイン名を示します。このパラメータには、`Region` の値に対応する以下の値があります。<br><br><br>* `tls-cn-hongkong.volces.com`<br><br>* `tls-ap-southeast-1.volces.com`<br><br>* `tls-ap-southeast-3.volces.com` |`tls-ap-southeast-1.volces.com` |
|ProjectID |String |いいえ |ログトピックが属するログプロジェクトIDを示します。 |`a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747` |
|TopicName |String |いいえ |ログを保存するログトピックの名前を示します。このログトピックが存在しない場合、CDNはそれを作成します。このパラメータの入力要件は次のとおりです：<br><br><br>* 長さは3～64文字です。<br><br>* 中国語、小文字の英字、数字、アンダースコア（_）、ハイフン（\-）のみを含めることができます。<br><br>* アンダースコア（_）またはハイフン（\-）で開始または終了することはできません。<br><br>* `tls_`、`tos_`、`tls-` で始まることはできません。<br><br><br>说明<br><br>このログトピックが他の配信タスクで既に指定されている場合、このログトピックを指定することはできません。<br><br>[ListRealtimeLogDeliveryTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_ja) を呼び出して、特定のログトピックが他のタスクによって既に指定されているかどうかを判断できます。 |`test_topic` |
|Ttl |Long |いいえ |ログの保存期間を示します。範囲は1～3649日で、単位は日です。<br><br>`3650` を入力すると、ログは永久に保存されます。 |`3` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TaskID |String |タスクのIDを示します。 |`b23298e8-c262-4cb6-8138-2c311230b972` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

**配信先は HTTP サーバー** 

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Domain": "img.example.com",
    "Desc": "mydesc",
    "HttpServer": {
        "Url": "http://www.example.com:8000/mylogs",
        "AuthMechanism": true,
        "SecretKey": "xxxxxxxxxx",
        "CompressType": "gzip",
        "RequestHeader": [
            {
                "key": "header1",
                "value": "value1"
            },
            {
                "key": "header2",
                "value": "value2"
            }
        ]
    },
    "SampleRate": 50.55,
    "TaskType": "http_server"
}
```


**配信先は TLS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com,img.example.com",
    "SampleRate": 100,
    "TaskType": "tls",
    "Tls": {
        "Endpoint": "tls-ap-southeast-1.volces.com`",
        "ProjectID": "a9db2fef-d7f8-47a3-aa0a-c52ef7ef4747",
        "TopicName": "topic2",
        "Ttl": 7
    }
}
```


**配信先は SLS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "SampleRate": 100,
    "Sls": {
        "AccessKeyId": "xxxxxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxxxxxxx",
        "Endpoint": "ap-southeast-1.log.aliyuncs.com",
        "LogStore": "my_store",
        "Project": "my_project"
    },
    "TaskType": "sls"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20251030172232277BC0277930A92087E9",
        "Action": "CreateRealtimeLogDeliveryTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "b23298e8-c262-4cb6-8138-2c311230b972"
    }
}
```


&nbsp;
