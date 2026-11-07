---
title: "SubmitPreloadTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/SubmitPreloadTask_jp"
---

BytePlus CDNでプリフェッチタスクを送信し、1つまたは複数のファイルを事前にCDNのキャッシュノードにキャッシュします。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

デフォルトでは、各BytePlusプライマリーアカウントのタスククォータは以下の通りです：


* 1日あたり最大1,000個のURLをプリフェッチできます。

* 各タスクで最大100個のURLをプリフェッチできます。


<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はSubmitPreloadTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Urls |String |いいえ |1つまたは複数のファイルURLを表します。CDNはこれらのファイルを事前にキャッシュノードにキャッシュします。<br><br>各URLは必ず`http://`または`https://`で始まる必要があります。複数のURLはで区切ります。<br><br>说明<br><br>URLにワイルドカードドメインを含めることはできません。ワイルドカードドメインの下の複数のサブドメインに対してプリフェッチタスクを送信する必要がある場合、各サブドメインに対してプリフェッチする必要があるURLを個別に指定する必要があります。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg`<br><br> |
|Area |String |いいえ |サービスを表します。CDNは`Urls`内の各ファイルを事前にこのリージョンのキャッシュノードにキャッシュします。このパラメータには以下の値があります：<br><br><br>* `chinese_mainland`：中国本土を表します。<br><br>* `outside_chinese_mainland`：中国本土を除くグローバルを表します。<br><br>* `global`：グローバルを表します。<br><br><br>このパラメータを指定しない場合、`Urls`内のURLについて、このサービス地域はそのURLに含まれるドメイン名のサービス地域となります。 |`outside_chinese_mainland`<br><br> |
|ConcurrentLimit |Long |いいえ |CDNがプリフェッチタスクを実行する際に、オリジンサーバーにリクエストする最大ファイル数を表します。デフォルト値は`10`で、このパラメータの値の範囲は1\-1000です。 |`20` |
|Layer |String |いいえ |コンテンツをどのキャッシュレイヤーにプリフェッチするかを表します。このパラメータには以下の値があります：<br><br><br>* `edge`：エッジレイヤーを表します。<br><br><br>このパラメータを指定しない場合、コンテンツをリージョナルレイヤーにプリフェッチすることを表します。<br><br>このパラメータを使用するには、[チケットを送信](https://console.volcengine.com/ticket/createTicketV2/)してください。 |`edge` |
|RequestHeaderInstances |Object[] |いいえ |CDNがプリフェッチタスクを実行する際に送信するオリジンリクエストに追加で含める必要があるリクエストヘッダーリストを表します。リスト内のリクエストヘッダー数は10個を超えてはいけません。 | |
|Key |String |いいえ |リスト内のリクエストヘッダーの名前を表します。名前には以下の要件があります：<br><br><br>* 名前は`User-Agent`であってはいけません。<br><br>* 名前は`x-bdcdn-`で始まってはいけません。<br><br>* 名前は1,024文字を超えてはいけません。<br><br>* 名前はリスト内で一意である必要があります。 |`Hello` |
|Value |String |いいえ |そのリクエストヘッダーの値を表し、長さは1,024文字を超えてはいけません。 |`World` |
|UrlList |String[] |いいえ |プリフェッチURLリストで、Urlsより優先度が高いです | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TaskID |String |このタスクのIDを表します。[DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeContentTasks_jp)を呼び出して、`Urls`内の各URLのプリフェッチ結果を確認できます。 |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=SubmitPreloadTask&Version=2021-03-01
{
    "Urls": "https://www.a.com/1.txt\nhttps://www.b.com/2.txt"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202406300908245F2C63BC765D774F1CB0",
        "Action": "SubmitPreloadTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871"
    }
}
```


&nbsp;
