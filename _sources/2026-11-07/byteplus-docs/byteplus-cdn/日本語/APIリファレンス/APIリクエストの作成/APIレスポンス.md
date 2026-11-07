---
title: "APIレスポンス"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/api-response-jp"
---

このドキュメントでは、BytePlus CDNがAPIリクエストにどのように応答するかについて説明します。

<span id="レスポンスステータスコード"></span>
## レスポンスステータスコード

CDNのレスポンスステータスコードは以下のように説明されます：


* 2xx：CDNがAPIリクエストに正常に応答したことを示します。ただし、正常な応答がAPIリクエストの成功を必ずしも保証するものではありません。[APIリクエストが成功したかどうかの判断](https://docs.byteplus.com/en/docs/18/35856#api%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%81%8C%E6%88%90%E5%8A%9F%E3%81%97%E3%81%9F%E3%81%8B%E3%81%A9%E3%81%86%E3%81%8B%E3%81%AE%E5%88%A4%E6%96%AD) を参照してください。

* 4xx：コンテンツ配信ネットワークがクライアントによって要求されたコンテンツを返すことができないことを示します。理由は、クライアントリクエストが無効であるためです。例えば：

* 要求されたファイルが存在しない。

* リクエストメソッドが正しくない。

* リクエストに必要なパラメータが欠けている。例えば、`Action`パラメータが欠けている。

* リクエスト者がターゲットリソースを操作する権限を持っていない。

* 5xx：リクエストが失敗したことを示します。失敗はコンテンツ配信ネットワークの内部エラーによるものです。例えば、コンテンツ配信ネットワークサービスが利用できない場合です。


<span id="apiリクエストが成功したかどうかの判断"></span>
## APIリクエストが成功したかどうかの判断

APIリクエストが成功したかどうかを判断する際に、CDNレスポンスステータスコードを使用することはお勧めしません。以下の基準を使用することをお勧めします：


* APIリクエストが成功した場合、レスポンスボディの`ResponseMetadata`構造に`Error`フィールドが含まれません。

* それ以外の場合はリクエスト失敗とみなされます。`ResponseMetadata`構造の`Error`フィールドで対応するエラーメッセージを確認できます。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">APIリクエストで以下のような状況に遭遇する可能性があります：</div>



* <div data-tips="true" data-tips-type="tip">CDNレスポンスステータスコードが2xxであるが、<code>ResponseMetadata</code>構造に<code>Error</code>フィールドが含まれている。</div>



<div data-tips="true" data-tips-type="tip">この場合、APIリクエストは失敗です。理由は、クライアントリクエストがCDNの設定を満たしていないためです。例えば：</div>



* <div data-tips="true" data-tips-type="tip">リクエストパラメータの値が無効である。</div>


* <div data-tips="true" data-tips-type="tip">エッジノードに証明書を設定する際、証明書ファイルに完全な証明書チェーンが含まれていない。</div>



CDNの一般的なエラーについては、[APIエラーコード](https://docs.byteplus.com/docs/byteplus-cdn/api-reference-error-codes-jp)を参照してください。

<span id="レスポンス例"></span>
## レスポンス例

<span id="成功したapiリクエストのレスポンス例"></span>
### 成功したAPIリクエストのレスポンス例

```json
{
        "ResponseMetadata": {
                "RequestId": "2021041510110201022510703416005FB0",
                "Action": "DescribeCdnData",
                "Version": "2021-03-01",
                "Service": "CDN",
                "Region": "singapore"
        },
        "Result": {...}
}
```


<span id="失敗したapiリクエストのレスポンス例"></span>
### 失敗したAPIリクエストのレスポンス例

```json
{
        "ResponseMetadata": {
                "RequestId": "2021041510110201022510703416005FB0",
                "Action": "DescribeCdnData",
                "Version": "2021-03-01",
                "Service": "CDN",
                "Region": "singapore",
                "Error": {
                        "Code": "ResourceNotFound",
                        "Message": "resource is not found"
                }
        }
}
```
