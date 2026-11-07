---
title: "UpdateRealtimeLogDeliveryTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRealtimeLogDeliveryTask_ja"
---

リアルタイムログ配信タスクの設定を変更します。

このAPIを呼び出す際、


* `HttpServer`、`Sls`、`Tls` の3つの構造体のうち1つを指定する必要があります。

* パラメータが指定されていない場合、そのパラメータはデフォルト値に設定されます。


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUpdateRealtimeLogDeliveryTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Area |String |はい |このパラメータ値は `outside_chinese_mainland` のみ可能で、中国本土を表します。 |`outside_chinese_mainland` |
|Domain |String |はい |タスクが関連付けられるドメイン名のリストを示します。<br><br><br>* アカウント内のすべてのドメイン名を関連付ける場合は、`*` を渡してください。ここでのすべてのドメイン名には、後でCDNに追加するドメイン名も含まれます。<br><br>* 指定したドメイン名を関連付ける場合は、関連付けるドメイン名のリストを渡してください。リストには最大200個のドメイン名を含めることができ、複数のドメイン名はカンマ（,）で区切ります。<br><br><br>注意<br><br>指定したドメイン名に関連付けられた他のタスクが既に存在する場合、`Domain` を `*` に指定することはできません。<br><br>ListRealtimeLogDeliveryTask を呼び出し、このドメイン名をフィルタ条件として指定することで、ドメインがタスクに関連付けられているかどうかを確認できます。 |`www.example.com,img.example.com` |
|TaskID |String |はい |変更するタスクのIDを示します。 |`b23298e8-c262-4cb6-8138-2c311230b972` |
|Desc |String |いいえ |タスクの説明を示します。このパラメータの入力要件は次のとおりです：<br><br><br>* 長さは3～64文字で、中国語、英字、数字、アンダースコア（_）、ハイフン（\-）を含めることができます。中国語は3文字としてカウントされます。<br><br>* ハイフン（\-）またはアンダースコア（_）で開始または終了することはできません。 |`newDesc` |
|HttpServer |Object |いいえ |`TaskType` が `http_server` の場合、この構造体はHTTPサーバー側の対応する設定を示します。<br><br>`HttpServer` を指定した場合、特に明記されていない限り、この構造体内のすべてのパラメータを指定する必要があります。 | |
|AuthMechanism |Boolean |いいえ |HTTPサーバーで認証が有効になっているかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`<br><br>* `false` |`true` |
|CompressType |String |いいえ |CDNがログを配信する際に使用する圧縮アルゴリズムを示します。このパラメータには次の値があります：<br><br><br>* `gzip`：Gzip圧縮アルゴリズムを示します。<br><br><br>このパラメータが指定されていない場合、圧縮は使用されません。 |`gzip` |
|RequestHeader |Object[] |いいえ |CDNがHTTPサーバーにログを配信する際に、リクエストに含める必要がある追加のヘッダーのリストを示します。リストには最大10個のヘッダーを含めることができます。<br><br>このパラメータが指定されていない場合、リクエストに追加のヘッダーは追加されません。 | |
|Key |String |いいえ |リスト内のヘッダーのキーを示します。長さは1,024文字を超えることはできません。`Key` は `User-Agent` であってはならず、`x-bdcdn-` で始まってはなりません。 |`mykey` |
|Value |String |いいえ |`Key` の値を示します。長さは1,024文字を超えることはできません。 |`myvalue` |
|SecretKey |String |いいえ |トークンを計算するための認証キーを示します。このパラメータの長さは6～40文字です。<br><br>`AuthMechanism` が `true` の場合、`SecretKey` を指定する必要があります。<br><br>認証プロセスとトークンアルゴリズムの詳細については、[タスク設定](https://docs.byteplus.com/en/docs/byteplus-cdn/log-streaming-task-config_jp) を参照してください。 |`xxxxxxxxx` |
|Url |String |いいえ |HTTPサーバーのアクセスポイント、ポート、およびログの保存パスを示します。ポートはオプションです。アクセスポイントは `http://` または `https://` で始まる必要があり、長さは1,024文字を超えることはできません。 |`https://img.example.com:8090/cdn-logs` |
|SampleRate |Double |いいえ |ログのサンプリングレートを示します。範囲は0.00～100.00で、小数点以下2桁までです。<br><br>サンプリングレートとは、配信されるログの割合を指します。たとえば、サンプリングレートを10に設定すると、CDNノードで100件のログが収集されるごとに、CDNはランダムに10件のログを選択して指定した場所に配信します。 |`70` |
|Sls |Object |いいえ |`TaskType` が `sls` の場合、この構造体はSLS側の対応する設定を示します。<br><br>`Sls` を指定した場合、この構造体内のすべてのパラメータを指定する必要があります。 | |
|AccessKeyId |String |いいえ |Alibaba CloudアカウントのAccessKey IDを示します。長さは128文字を超えることはできません。 |`xxxxxxxxxxxx` |
|AccessKeySecret |String |いいえ |Alibaba CloudアカウントのAccessKey Secretを示します。長さは128文字を超えることはできません。 |`xxxxxxxxx` |
|Endpoint |String |いいえ |`Project` のパブリックドメイン名を示します。 |`ap-southeast-1.log.aliyuncs.com` |
|LogStore |String |いいえ |ログを保存するLogStoreを示します。 |`myStore` |
|Project |String |いいえ |`LogStore` が属するログプロジェクトを示します。このプロジェクトは `Endpoint` に対応する配信リージョンにあります。 |`myProject` |
|Tls |Object |いいえ |`TaskType` が `tls` の場合、この構造体はTLS側の対応する設定を示します。<br><br>`Tls` を指定した場合、この構造体内のすべてのパラメータを指定する必要があります。 | |
|Ttl |Long |いいえ |ログの保存期間を示します。範囲は1～3649日で、単位は日です。<br><br>`3650` を入力すると、ログは永久に保存されます。 |`3` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateRealtimeLogDeliveryTask&Version=2021-03-01
{
    "Area": "outside_chinese_mainland",
    "TaskID": "6af98494-c4fd-4c1b-bc36-88c4de0b5b9e",
    "Domain": "www.example.com",
    "Sls": {
        "AccessKeyId": "yyyyyyyyyyyyyyyyyy",
        "AccessKeySecret": "yyyyyyyyyy",
        "Endpoint": "ap-southeast-1.log.aliyuncs.com",
        "LogStore": "my_store",
        "Project": "my_project"
    }
}
```


&nbsp;
