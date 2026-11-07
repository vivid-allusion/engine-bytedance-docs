---
title: "SubmitRefreshTask"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/SubmitRefreshTask_jp"
---

BytePlus CDNでパージタスクを送信します。タスクでファイルURLを指定した場合、CDNは実行時にこれらのファイルを削除します。タスクでディレクトリを指定した場合、CDNはデフォルトでこれらのディレクトリ内のファイルを期限切れとしてマークします。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はSubmitRefreshTaskです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Type |String |いいえ |パージタイプを表します。このパラメータには以下の値があります：<br><br><br>* `file`：URLパージを表し、1つまたは複数のファイルに対してパージ操作を実行します。<br><br>* `dir`：ディレクトリパージを表し、1つまたは複数のディレクトリ内のすべてのファイル（サブディレクトリ内のファイルを含む）に対してパージ操作を実行します。<br><br><br>このパラメータのデフォルト値は`file`です。 |`file` |
|Prefix |Boolean |いいえ |プレフィックスパージを使用するかどうかを表します。このパラメータは`Type`が`dir`の場合にのみ有効で、以下の値があります：<br><br><br>* `true`：プレフィックスパージを使用し、指定されたプレフィックスで始まるディレクトリ内のすべてのファイルに対してパージ操作を実行します。<br><br>* `false`：プレフィックスパージを使用しません。<br><br><br>このパラメータのデフォルト値は`false`です。 |`true` |
|Urls |String |いいえ |パージ対象の1つまたは複数のURLを表し、複数のURLはで区切ります。各URLは必ず`http://`または`https://`で始まる必要があります。<br><br><br>* `Type`が`file`の場合、ファイルURLを指定します。<br><br>* `Type`が`dir`の場合、<br><br>* `Prefix`が`false`の場合、`/`で終わるディレクトリを指定します。例：`http://www.example.com/image/`。<br><br>* `Prefix`が`true`の場合、ディレクトリプレフィックスを指定します。例：`http://www.example.com/im`は`http://www.example.com/image/`と`http://www.example.com/ime/`の両方のディレクトリにマッチします。<br><br>* `Type`が`regex`の場合、ファイルURLをマッチングするための正規表現を指定します。[キャッシュパージ](https://docs.byteplus.com/en/docs/byteplus-cdn/purge-cache-jp)を参照してください。このパラメータ値を指定するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。<br><br><br>说明<br><br>ワイルドカードドメインの下のファイルとディレクトリに直接パージ操作を実行することはできません。代わりに、各サブドメインに対してこれらの操作を実行する必要があります。 |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg`<br><br> |
|Delete |Boolean |いいえ |ディレクトリ内のすべてのファイルをキャッシュから削除するかどうかを表します。このパラメータは`Type`が`dir`の場合にのみ有効です。このパラメータを使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。<br><br>このパラメータには以下の値があります：<br><br><br>* `true`：これらのファイルを削除します。その後、これらのファイルへのリクエストを受信した場合、CDNはオリジンサーバーにこれらのファイルをリクエストします。<br><br>* `false`：これらのファイルを削除せず、これらのファイルを期限切れとしてマークするだけです。その後、これらのファイルへのリクエストを受信した場合、CDNは[キャッシュルール](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules-jp)を実行します。<br><br><br>このパラメータのデフォルト値は`false`です。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TaskID |String |このタスクのIDを表します。[DescribeContentTasks](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeContentTasks_jp)を呼び出して、`Urls`リスト内の各オブジェクトのパージ結果を確認できます。 |`refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=SubmitRefreshTask&Version=2021-03-01
{
    "Type": "file",
    "Urls": "https://www.example.com/1.txt\nhttps://www.example.com/2.txt"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202201141648440102100180260E003ABA",
        "Action": "SubmitRefreshTask",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskID": "refresh_url_bbd36e1cb5154f52b648b07ee119223e2971399f5a1075c0"
    }
}
```


&nbsp;
