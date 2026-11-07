---
title: "ListOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_ja"
---

オフラインログストレージタスクのリストを取得します。一連のフィルタリング条件を指定して、タスクリストをフィルタリングできます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はListOfflineLogStoreTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Bucket |String |いいえ |フィルタリング条件として、バケットにログファイルを保存するパスを指定します。形式は`<バケット名>/<ログファイルパス>`です。 |`mybucket/storage/logs` |
|Desc |String |いいえ |フィルタリング条件として`Desc`を指定します。あいまい一致をサポートします。 |`myDesc` |
|Domain |String |いいえ |フィルタリング条件としてドメインを指定し、そのドメインのログを保存するタスク、つまりそのタスクに関連付けられているドメインを取得します。 |`www.example.com` |
|Region |String |いいえ |フィルタリング条件として、バケットが配置されているリージョンコードを指定します。リージョンコードの長さは64文字を超えることはできません。<br><br><br>* `TaskType`が`s3`の場合、指定できるリージョンコードについては、バケットのオブジェクトストレージサービスプロバイダーにお問い合わせください。<br><br>* `TaskType`が`tos`の場合、次のリージョンコードを指定できます：<br><br>   * `cn-hongkong`：中国香港を表します。<br><br>   * `ap-southeast-1`：アジア太平洋南東（ジョホール）を表します。<br><br>   * `ap-southeast-3`：アジア太平洋南東（ジャカルタ）を表します。 |`cn-beijing` |
|Status |String |いいえ |フィルタリング条件としてタスクのステータスを指定します。このパラメータには次の値があります：<br><br><br>* `enable`：有効を示します。<br><br>* `disable`：無効を示します。 |`enable` |
|TaskID |String |いいえ |フィルタリング条件としてタスクIDを指定します。 |`nj2S29or5KaAeEiwcGWA5S` |
|TaskType |String |いいえ |フィルタリング条件としてストレージターゲットを指定します。このパラメータには次の値があります：<br><br><br>* `tos`：BytePlus Object Storage（TOS）を表します。<br><br>* `s3`：AWS S3またはS3互換の認証方法を使用するオブジェクトストレージサービスを表します。 |`s3` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TaskInfo |Object[] |フィルタリング条件に一致するタスクのリストを示します。 | |
|AuthInformation |Object |ストレージターゲットのアクセス資格情報を示します。 | |
|AccessKeyID |String |資格情報内のAccessKey IDを示します。 |`xxxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |資格情報内のAccessKey Secretを示します。 |`xxxxxxxxx` |
|Bucket |String |バケットにログファイルを保存するパスを示します。 |`mybucket/log` |
|CreateTime |Long |タスクの作成時刻をUnixタイムスタンプ形式で示します。 |`1761908274` |
|Desc |String |タスクの説明を示します。 |`myDesc` |
|Domain |String |タスクに関連付けられているドメインを示します。 |`www.example.net` |
|Endpoint |String |オブジェクトストレージサービスのパブリックアクセスポイントを示します。 |`tos-cn-shanghai.volces.com` |
|PrivateBucketAccess |Boolean |バケットがプライベートであるかどうかを示します。 |`true` |
|Region |String |バケットが配置されているリージョンコード（region code）を示します。 |`us-east-1` |
|Status |String |タスクのステータスを示します。このパラメータには次の値があります：<br><br><br>* `enable`：タスクが有効であることを示します。<br><br>* `disable`：タスクが無効であることを示します。 |`enable` |
|StatusDetail |Object[] |タスクで最近発生した例外のリストを示します。リストには最大10個の例外が記録されます。 | |
|Detail |String |例外の詳細を示します。 |`exception details` |
|Time |Long |例外が発生した時刻をUnixタイムスタンプ形式で示します。 |`1761815000` |
|TaskID |String |タスクのIDを示します。 |`dPFEQ8vwbRShTdW5kNbZe3` |
|TaskType |String |ログストレージのターゲットを示します。次の値があります：<br><br><br>* `tos`：BytePlus Object Storage（TOS）を表します。<br><br>* `s3`：AWS S3またはS3互換の認証方法を使用するオブジェクトストレージサービスを表します。 |`s3` |
|UpdateTime |Long |タスクの最終更新時刻をUnixタイムスタンプ形式で示します。 |`1761908274` |
|Total |Long |リスト内のタスクの数を示します。 |`1` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=ListOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "mybucket/log",
    "Desc": "myDesc",
    "Domain": "www.example.net",
    "Region": "us-east-1",
    "Status": "enable",
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
    "TaskType": "s3"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20251103163008001C7913418610FF31AA",
        "Action": "ListOfflineLogStoreTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskInfo": [
            {
                "AuthInformation": {
                    "AccessKeyID": "xxxxxxxxxxxxxxx",
                    "AccessKeySecret": "xxxxxxxx"
                },
                "Bucket": "mybucket/log",
                "CreateTime": 1761908274,
                "Desc": "myDesc",
                "Domain": "www.example.net",
                "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
                "PrivateBucketAccess": true,
                "Region": "us-east-1",
                "Status": "enable",
                "StatusDetail": [],
                "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
                "TaskType": "s3",
                "UpdateTime": 1761908274
            }
        ],
        "Total": 1
    }
}
```


&nbsp;
