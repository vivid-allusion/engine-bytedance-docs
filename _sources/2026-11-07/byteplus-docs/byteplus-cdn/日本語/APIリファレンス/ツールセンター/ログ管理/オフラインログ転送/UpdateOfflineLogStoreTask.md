---
title: "UpdateOfflineLogStoreTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateOfflineLogStoreTask_ja"
---

オフラインログストレージタスクの設定を変更します。このAPIを呼び出す際に、特定のパラメータが指定されていない場合、そのパラメータはデフォルト値に設定されます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UpdateOfflineLogStoreTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUpdateOfflineLogStoreTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Bucket |String |はい |バケット内のログファイルを保存するディレクトリパスを示します。末尾に「/」を付けることはできません。形式は`<バケット名>/<ディレクトリパス>`です。<br><br>パスにディレクトリが存在しない場合、CDNはバケット内に対応するディレクトリを作成します。 |`mybucket/new/logs` |
|Domain |String |はい |タスクが関連付けられるドメインのリストを示します。<br><br><br>* アカウント内のすべてのドメインを関連付ける場合は、`*`を渡してください。ここでのすべてのドメインには、後でCDNに追加するドメインも含まれます。<br><br>* 指定したドメインを関連付ける場合は、関連付けるドメインのリストを渡してください。リストには最大200個のドメインを含めることができ、複数のドメインはカンマ（,）で区切ります。<br><br><br>注意<br><br>指定したドメインを関連付ける他のタスクがすでに存在する場合、`Domain`を`*`に指定することはできません。<br><br>[ListOfflineLogStoreTask](https://docs.byteplus.com/en/docs/byteplus-cdn/ListRealtimeLogDeliveryTask_ja)を呼び出し、このドメインをフィルタ条件として指定することで、ドメインがタスクに関連付けられているかどうかを確認できます。 |`www.example.com` |
|Endpoint |String |はい |オブジェクトストレージサービスのパブリックアクセスポイントを示します。バケット名は含まれません。<br><br><br>* `TaskId`が示すタスクのストレージターゲットが`s3`の場合、アクセスポイントは`https://`で始まる必要があり、バケット名は含まず、長さは1,024文字を超えることはできません。<br><br>* ストレージターゲットが`tos`の場合、このパラメータには次の値があり、`Region`の値に対応します。<br><br>   * `tos-cn-hongkong.volces.com`<br><br>   * `tos-ap-southeast-1.volces.com`<br><br>   * `tos-ap-southeast-3.volces.com` |`tos-ap-southeast-1.volces.com` |
|Region |String |はい |バケットが配置されているリージョンコードを示します。長さは64文字を超えることはできません。<br><br><br>* `TaskId`が示すタスクのストレージターゲットが`s3`の場合、バケットのオブジェクトストレージサービスプロバイダーに問い合わせて、バケットのリージョンコードを取得してください。<br><br>* ストレージターゲットが`tos`の場合、リージョンコードには次の値があります。<br><br>   * `cn-hongkong`：香港を表します。<br><br>   * `ap-southeast-1`：アジア太平洋南東（ジョホール）を表します。<br><br>   * `ap-southeast-3`：アジア太平洋南東（ジャカルタ）を表します。 |`ap-southeast-1` |
|TaskID |String |はい |変更するタスクのIDを示します。 |`dPFEQ8vwbRShTdW5kNbZe3` |
|AuthInformation |Object |いいえ |ストレージターゲットのアクセス資格情報を示します。`PrivateBucketAccess`が`true`で、`TaskType`が`s3`の場合にのみ、この構造体を指定する必要があります。 | |
|AccessKeyID |String |いいえ |資格情報内のAccessKey IDを示します。 |`xxxxxxxxxx` |
|AccessKeySecret |String |いいえ |資格情報内のAccessKey Secretを示します。 |`xxxxxx` |
|Desc |String |いいえ |タスクの説明を示します。長さは3～45文字で、漢字、英字、数字を含めることができますが、アンダースコア（_）で始まったり終わったりすることはできません。 |`newDesc` |
|PrivateBucketAccess |Boolean |いいえ |バケットがプライベートかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`<br><br>* `false`<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=UpdateOfflineLogStoreTask&Version=2021-03-01
{
    "Bucket": "mybucket/new/log",
    "Desc": "myDesc_new",
    "Domain": "www.example.com",
    "Endpoint": "https://mybucket.s3-website-us-east-1.amazonaws.com",
    "PrivateBucketAccess": true,
    "Region": "us-east-1",
    "TaskID": "dPFEQ8vwbRShTdW5kNbZe3",
    "AuthInformation": {
        "AccessKeyID": "xxxxxxxxxxxxxxxxxxx",
        "AccessKeySecret": "xxxxxxxxxx"
    }
}
```


&nbsp;
