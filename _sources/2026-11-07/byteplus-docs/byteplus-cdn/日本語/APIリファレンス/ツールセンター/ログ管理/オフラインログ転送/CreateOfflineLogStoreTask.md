---
title: "CreateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateOfflineLogStoreTask_ja"
---

CDNでオフラインログストレージタスクを作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はCreateOfflineLogStoreTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Bucket |String |はい |バケット内のログファイルを保存するディレクトリパスを示します。末尾に「/」を付けることはできません。形式は`<バケット名>/<ディレクトリパス>`です。<br><br>パスにディレクトリが存在しない場合、CDNはバケット内に対応するディレクトリを作成します。 |`mybucket/storage/logs` |
|Domain |String |はい |どのドメインのリアルタイムログを配信するか、つまりタスクが関連付けられるドメインを示します。<br><br><br>* アカウント内のすべてのドメインを関連付ける場合は、`*`を渡してください。ここでのすべてのドメインには、後でCDNに追加するドメインも含まれます。<br><br>* 指定したドメインを関連付ける場合は、関連付けるドメインのリストを渡してください。リストには最大200個のドメインを含めることができ、複数のドメインはカンマ（,）で区切ります。<br><br><br>注意<br><br>アカウント内のすべてのドメインを関連付けるタスクをすでに作成している場合、指定したドメインを関連付けるタスクを作成することはできません。逆も同様です。<br><br>[ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListOfflineLogStoreTask_ja)を呼び出し、このドメインをフィルタ条件として指定することで、ドメインがタスクに関連付けられているかどうかを確認できます。 |`www.example.com,img.example.com` |
|Endpoint |String |はい |オブジェクトストレージサービスのパブリックアクセスポイントを示します。バケット名は含まれません。<br><br><br>* `TaskType`が`s3`の場合、アクセスポイントは`https://`で始まる必要があり、バケット名は含まず、長さは1,024文字を超えることはできません。<br><br>* `TaskType`が`tos`の場合、このパラメータには次の値があり、`Region`の値に対応します。<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`https://oss-ap-southeast-1.aliyuncs.com` |
|Region |String |はい |バケットが配置されているリージョンコードを示します。長さは64文字を超えることはできません。<br><br><br>* `TaskType`が`s3`の場合、バケットのオブジェクトストレージサービスプロバイダーに問い合わせて、バケットのリージョンコードを取得してください。<br><br>* `TaskType`が`tos`の場合、リージョンコードには次の値があります。<br><br>   * `cn-hongkong`：香港を表します。<br><br>   * `ap-southeast-1`：アジア太平洋南東（ジョホール）を表します。<br><br>   * `ap-southeast-3`：アジア太平洋南東（ジャカルタ）を表します。 |`ap-southeast-1` |
|TaskType |String |はい |ログストレージのターゲットを示します。次の値があります。<br><br><br>* `tos`：BytePlusオブジェクトストレージ（TOS）を表します。<br><br>* `s3`：AWS S3またはS3互換の認証方法を使用するオブジェクトストレージサービスを表します。 |`s3` |
|AuthInformation |Object |いいえ |ストレージターゲットのアクセス資格情報を示します。`PrivateBucketAccess`が`true`で、`TaskType`が`s3`の場合にのみ、この構造体を指定する必要があります。 | |
|AccessKeyID |String |いいえ |資格情報内のAccessKey IDを示します。 |`xxxxxxxxxxxxx` |
|AccessKeySecret |String |いいえ |資格情報内のAccessKey Secretを示します。 |`xxxxx` |
|Desc |String |いいえ |タスクの説明を示します。長さは3～45文字で、漢字、英字、数字を含めることができますが、アンダースコア（_）で始まったり終わったりすることはできません。 |`myDesc` |
|PrivateBucketAccess |Boolean |いいえ |バケットがプライベートかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`<br><br>* `false`<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TaskID |String |タスクのIDを示します。 |`nj2S29or5KaAeEiwcGWA5S` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

 **ログの保管先は TOS**

```json
POST https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "myBucket/logfile",
    "Desc": "myDesc",
    "Domain": "www.example.com,img.example.com",
    "Endpoint": "tos-ap-southeast-1.volces.com",
    "PrivateBucketAccess": true,
    "Region": "ap-southeast-1",
    "TaskType": "tos"
}
```


 **ログの保管先は AWS S3**

```json
POST https://cdn.byteplusapi.com/?Action=CreateOfflineLogStoreTask&Version=2021-03-01
{
    "AuthInformation": {
        "AccessKeyID": "xxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxx"
    },
    "Bucket": "mybucket/log",
    "Desc": "myDesc",
    "Domain": "www.example.com",
    "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
    "PrivateBucketAccess": true,
    "Region": "us-east-1",
    "TaskType": "s3"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202510311813528D239468E6A7A99DA92C",
        "Action": "CreateOfflineLogStoreTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "5daCXtLTDpRYDDhFruQ9hP"
    }
}
```


&nbsp;
