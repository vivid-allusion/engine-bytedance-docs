---
title: "DescribeCdnConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_jp"
---

BytePlus CDNのドメイン名の設定を取得します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20件のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeCdnConfigです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Domain |String |はい |ドメイン名を表し、そのドメイン名の設定を取得します。 |`www.example.com` |
|LockInfo |Boolean |いいえ |ロック情報を照会します。 | |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|DomainConfig |Object |`Domain` の設定を表します。 | |
|Domain |String |リクエストパラメータの `Domain` を表します。 |`www.example.com` |
|OriginProtocol |String |オリジンリクエストで使用されるプロトコルを表します。このパラメータは次の値を取ることができます：<br><br><br>* `http`：オリジンリクエストがHTTPプロトコルを使用することを示します。<br><br>* `https`：オリジンリクエストがHTTPSプロトコルを使用することを示します。<br><br>* `followclient`：オリジンリクエストのプロトコルがユーザーからのリクエストで使用されたプロトコルと同じであることを示します。 |`http` |
|AreaAccessRule |Object |「地理的制限」機能の設定を表します。 | |
|Area |String[] |国と地域のリストを表し、このリストに地域アクセス制限を適用します。国と地域の名前は略称で表されます。[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出し、`Area`を`Global`に指定して国と地域の略称を取得できます。 |`["CHE","AZE"]` |
|RuleType |String |`Area` のタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `deny`：`Area` がブロックリストであることを示します。CDN はこれらの国や地域からのリクエストをブロックします。<br><br>* `allow`：`Area` がアローリストであることを示します。CDN はこれらの国や地域からのリクエストのみを許可します。 |`allow` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|BrowserCache |Object[] |「ブラウザキャッシュ」機能の設定を表します。ルールリストが含まれており、説明は以下の通りです：<br><br><br>* 各ルールにはマッチング条件設定と操作設定が含まれます。<br><br>* ルールがリストに表示される順序は、ルールの優先順位を表します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとルールとリクエストをマッチングさせます。ルールがリクエストにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|CacheAction |Object |リクエストが `Condition` のマッチング条件を満たす場合、CDN はリクエストされたファイルに対して指定された操作を実行します。このパラメータは、その操作に関連する設定を定義します。 | |
|IgnoreCase |Boolean |`Value` が大文字と小文字を区別するかどうかを示します。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。 |`true` |
|Ttl |Long |ブラウザがリクエストファイルをキャッシュする必要がある期間を秒単位で表します。CDNはレスポンスヘッダーに`Cache-Control: max-age`ヘッダーを含め、ヘッダー値はこのパラメータ値になります。 |`100` |
|DefaultPolicy |String |ブラウザがリクエストされたファイルをどのようにキャッシュするかを示します。このパラメータは次の値を取ります：<br><br><br>* `cache`：リクエストされたファイルをキャッシュする必要があることを示します。<br><br>* `origin_first`：オリジンサーバーからのキャッシュポリシーに従うことを示します。このポリシーはCDNのレスポンスに含まれます。<br><br>* `no_cache`：リクエストされたファイルをキャッシュする必要がないことを示します。<br><br><br>ブラウザキャッシュポリシーの詳細については、[ブラウザキャッシュ](https://docs.byteplus.com/en/docs/byteplus-cdn/browser-cache-jp)を参照してください。 |`cache` |
|Condition |Object |マッチング条件の設定を表します。リクエストが特定の条件にマッチした場合、CDNはそのリクエストに対して `CacheAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチ条件のリストを表します。現在、リストには1つのマッチ条件のみ含めることができます。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。 |`directory` |
|Operator |String |マッチタイプを表します。このパラメータの値は `match` のみで、`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`png` |
|Name |String | | |
|Cache |Object[] |「キャッシュルール」機能の設定を表します。ルールリストが含まれており、説明は以下の通りです：<br><br><br>* リスト内のルールの順序は、ルールの優先順位を定義します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとルールとリクエストをマッチングさせます。ルールがリクエストにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|CacheAction |Object |リクエストが `Condition` のマッチング条件を満たす場合、CDN はリクエストされたファイルに対して指定された操作を実行します。このパラメータは、その操作に関連する設定を定義します。 | |
|IgnoreCase |Boolean |`Value` が大文字と小文字を区別するかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。 |`true` |
|Ttl |Long |リクエストされたファイルのキャッシュTTLを `秒` 単位で表します。このパラメータ値が `0` の場合、CDNはリクエストされたファイルをキャッシュする必要がないことを示します。 |`100` |
|DefaultPolicy |String |CDNのリクエストファイルに対するキャッシュ動作を表します。このパラメータは次の値を取ることができます：<br><br><br>* `force_cache`：CDNコンソールの **CDNキャッシュ**  + **強制キャッシュ（オン）**  の設定の組み合わせに対応します。<br><br>* `default`：CDNコンソールの **CDNキャッシュ**  + **強制キャッシュ（オフ）**  の設定の組み合わせに対応します。<br><br>* `origin_first`：CDNコンソールの  **オリジンサーバーに従う**  + **補足キャッシュ（オン）**  の設定の組み合わせに対応します。<br><br>* `origin_first_Replenish`：CDNコンソールの  **オリジンサーバーに従う**  + **補足キャッシュ（オフ）**  の設定の組み合わせに対応します。<br><br><br>これらのキャッシュポリシーの説明については、[キャッシュルール](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/caching-rules)を参照してください。 |`force_cache` |
|Condition |Object |マッチング条件の設定を表します。リクエストが特定の条件にマッチした場合、CDNはそのリクエストに対して `CacheAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。 |`directory` |
|Operator |String |マッチタイプを表します。このパラメータの値は `match` のみで、`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`png` |
|Name |String |1つまたは複数のマッチング値を表します。複数のマッチング値はセミコロン(;)で区切られます。 | |
|Connective |String |複数の `ConditionRule` 間の論理関係を表します。現在、このパラメータを設定することはできません。このパラメータを指定しないか、値を `OR` に設定することができます。 | |
|CacheHost |Object |「共有キャッシュ」機能の設定を表します。 | |
|CacheHostRule |Object[] |共有キャッシュの設定一式を表します。 | |
|CacheHostAction |Object |ある設定の詳細を表します。 | |
|CacheHost |String |ターゲットドメイン名を表します。このターゲットドメイン名は、あなたのアカウント下の別のドメイン名でなければなりません。このパラメータは、`Domain`が`CacheHost`のCDNキャッシュを共有することを示します。 |`www.test.com` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|CacheKey |Object[] |「キャッシュキールール」機能の設定を表し、以下の説明を含むルールリストが含まれています：<br><br><br>* 各ルールには、マッチング条件の設定と操作の設定が含まれています。<br><br>* リスト内のルールの順序は、ルールの優先順位を示します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ると、CDNはルールの優先順位に従って、高いものから低いものへとリクエストをマッチングさせます。リクエストがルールにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|CacheKeyAction |Object |リクエストが `Condition` のマッチング条件を満たす場合、CDN はリクエストファイルにキャッシュキーを設定します。このパラメータはキャッシュキーの設定を表します。 | |
|CacheKeyComponents |Object[] |キャッシュキーは、リクエストのホスト、パス、クエリ文字列などの部分から構成されます。このパラメータは、これらの各構成要素の設定を表します。 | |
|IgnoreCase |Boolean |`Value` が大文字と小文字を区別するかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。 |`true` |
|Object |String |キャッシュキーの構成要素を表します。現在、このパラメータ値は `querystring` のみで、クエリ文字列を表します。 |`queryString` |
|Subobject |String |このパラメータは `Action` に対応し、CDNがキャッシュキーに含める具体的なクエリパラメータを示します。このパラメータの説明は以下の通りです：<br><br><br>* `Action`が`include`または`exclude`の場合、`Subobject`は`*`で、リクエストのすべてのクエリパラメータを表します。<br><br>* `Action`が`includePart`または`excludePart`の場合、保持または保持しないクエリパラメータを表します。複数のクエリパラメータはセミコロン（;）で区切られます。 |`sign;testParams` |
|Condition |Object |マッチング条件の設定を表します。リクエストが特定の条件にマッチした場合、CDNはそのリクエストに対して `CacheKeyAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチ条件のリストを表します。リストには1つのマッチ条件のみ含めることができます。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。 |`directory` |
|Operator |String |マッチタイプを表します。このパラメータの値は `match` のみで、`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`png` |
|Name |String | | |
|Compression |Object |「ファイル圧縮」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|CompressionRules |Object[] |ルールのグループを表します。各ルールには、マッチング条件の設定と操作の設定が含まれます。 | |
|CompressionAction |Object |ユーザーからのリクエストが `Condition` を満たしたときに、CDNがリクエストファイルに対して実行する圧縮操作の設定を表します。 | |
|CompressionType |String[] |CDNが使用する1つ以上の圧縮アルゴリズムを表します。このパラメータは次の値を取ることができます：<br><br><br>* `br`：Brotli圧縮アルゴリズムを表します。<br><br>* `gzip`：Gzip圧縮アルゴリズムを表します。<br><br><br>CDNはユーザーからのリクエストの`Accept-Encoding`ヘッダーに基づいて、リクエストファイルを圧縮するかどうか、および使用する圧縮アルゴリズムを決定することに注意してください。 |`["gzip","br"]` |
|CompressionFormat |String |CDNがリクエストの `Content-Type` ヘッダーに基づいてリクエストをマッチングすることを示します。このパラメータは次の値を取ります：<br><br><br>* `default`：`Content-Type` ヘッダー値が以下のデフォルトリストにある場合、CDN はリクエストファイルに対して `CompressionAction` で設定された操作を実行します。<br><br>* `customize`：`Content-Type` ヘッダー値が `CompressionFormat` で指定されたヘッダー値にある場合、CDN はリクエストファイルに対して `CompressionAction` で設定された操作を実行します。<br><br><br> **デフォルトリスト** <br><br>text/html、text/xml、text/plain、text/css、application/javascript、application/x\-javascript、application/rss+xml、text/javascript、image/tiff、image/svg+xml、application/json、application/xml、text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |`Content-Type` のフィルタ値を表します。<br><br><br>* `CompressionFormat` が `default` または `all` の場合、このパラメータは `*` です。<br><br>* `CompressionFormat` が `customize` の場合、このパラメータは1つ以上のファイルタイプを含みます。複数のファイルタイプはカンマ（,）で区切られます。 |`application/xml,hello/world` |
|MinFileSizeKB |Long |ファイルの最小サイズを表し、CDNは`MinFileSizeKB`と`MaxFileSizeKB`で示される範囲内のサイズのファイルのみを圧縮します。このパラメータの単位はKBで、1,024進数を使用します。 |`10` |
|MaxFileSizeKB |Long |ファイルの最大サイズをKB単位で表し、1,024進数を使用します。このパラメータを指定しない場合、ファイルサイズの上限は制限されません。 | |
|Condition |Object |マッチング条件の設定を表します。リクエストが特定の条件にマッチした場合、CDNはそのリクエストに対して `CompressionAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。 |`directory` |
|Operator |String |マッチタイプを表します。このパラメータの値は `match` のみで、`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`/img/` |
|Name |String | | |
|Connective |String |`ConditionRule` 内の各フィルタ条件間の論理関係を表します。現在、1つのフィルタ条件しか指定できないため、このパラメータは実際には意味を持ちません。 | |
|CustomErrorPage |Object |「カスタムエラーページ」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|ErrorPageRule |Object[] |設定ルールのリストを表します。 | |
|ErrorPageAction |Object |ルール関連の設定を表します。 | |
|RedirectCode |String |リダイレクトのレスポンスステータスコードを表します。このパラメータの値には `301`、`302`、`303`、`307`、`308` があります。<br><br>注意点：<br><br><br>* 301と302の場合、元のリクエストがGET以外のメソッドを使用していると、クライアントが新しいURLにリクエストを送信する際に、新しいリクエストのメソッドがGETに変わることがあります。<br><br>* 303の場合、新しいリクエストのメソッドはGETです。<br><br>* 307と308の場合、新しいリクエストのメソッドは元のリクエストと同じで、変更されません。 |`302` |
|RedirectUrl |String |リダイレクト先のURLを表します。 |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |4xxまたは5xxのステータスコードを表します。4xxは400〜499のすべてのステータスコードを、5xxは500〜599のすべてのステータスコードを表します。 |`4xx` |
|CustomizeAccessRule |Object |「カスタムヘッダーブロックリスト/アローリスト」機能の設定モジュールを表します。この機能はデフォルトで無効になっています。この機能を使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。 | |
|CustomizeInstances |Object[] |ルールリストを表します。リストの各ルールには、ブロックリストまたはアローリストの設定が定義されています。<br><br>リストには最大10個のルールを含めることができます。 | |
|CustomizeRule |Object |リスト内の1つのルールの設定を表します。 | |
|AccessAction |Object |このルール内のブロックリストまたはアローリストの設定を表します。 | |
|AllowEmpty |Boolean |CDNが `RequestHeader` の値が空のユーザーからのリクエストを受け入れるかどうかを示します。<br><br>ヘッダー値が空とは、以下のいずれかの状況を指します：<br><br><br>* ユーザーからのリクエストに `RequestHeader` が含まれていない。<br><br>* ユーザーからのリクエストに `RequestHeader` が含まれているが、ヘッダー値が空（""）である。 | |
|ListRules |String[] |リクエストヘッダーの値を照合するための正規表現のリストを表します。<br><br>リスト内の正規表現は20個を超えてはならず、すべての正規表現の総長は1,024文字を超えてはなりません。正規表現間の関係はORです。つまり、ユーザーからのリクエストの`RequestHeader`の値がいずれかの正規表現に一致する場合、このルールはそのリクエストに一致します。 | |
|RequestHeader |String |指定されたリクエストヘッダーを表します。ヘッダー名は大文字と小文字を区別せず、以下の要件があります：<br><br><br>* 名前の長さは1,024文字を超えないこと。<br><br>* 名前は `Referer`、`User-Agent`、`Origin` であってはならないこと。<br><br>* 名前には英字、数字、アンダースコア（_）、ハイフン（\-）を含めることができること。<br><br>* 名前は数字で始まってはならないこと。 | |
|RuleType |String |リストのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `allow`：このルールで定義されているのがアローリストであることを示します。ユーザーからのリクエストがアローリストに一致しない場合、CDNはそのリクエストを拒否し、403ステータスコードを応答します。<br><br>* `deny`：このルールで定義されているのがブロックリストであることを示します。ユーザーからのリクエストがブロックリストに一致する場合、CDNはそのリクエストを拒否し、403ステータスコードを応答します。 | |
|Condition |Object |なし | |
|ConditionRule |Object[] | | |
|Object |String | | |
|Operator |String |@desc: マッチオブジェクト. choices: [path, directory, filetype] | |
|Type |String |@desc: マッチ方法. choices: [match, not_match] | |
|Value |String |@desc: マッチ値 複数ある場合はセミコロン; で区切る@desc: マッチオブジェクトタイプ. choices: [url] | |
|Name |String | | |
|Connective |String |@desc: 複数の条件がある場合の論理接続詞、ConditionRuleが1つしかない場合は省略可能. choices: [AND, OR]@desc: 条件ルール、現在1つのルールのみサポート | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 | |
|DownloadSpeedLimit |Object |「データレートスロットリング」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|DownloadSpeedLimitRules |Object[] |スロットリングルールのリストを表します。このパラメータのその他の説明は以下の通りです：<br><br><br>* 各ルールには、マッチング条件の設定とスロットリングの設定が含まれます。<br><br>* リスト内のルールの出現順序は、ルールの優先順位を示します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ると、CDNはルールの優先順位に従って、高いものから低いものへとリクエストをマッチングさせます。リクエストがルールにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|DownloadSpeedLimitAction |Object |スロットリング設定を表します。 | |
|SpeedLimitRate |Long |CDNが単一のリクエストに応答する際の最大データ転送速度を`B/S`単位で表し、`1,024`進数を使用します。 |`500000` |
|SpeedLimitRateAfter |Long |初期データ量を `bytes` 単位で表し、`1,024` の基数を使用します。<br><br>CDNがリクエストのデータ転送を開始する際、転送されたデータ量がこの初期データ量に達するまで、このレート制限ルールは有効になりません。<br><br>このパラメータ値が `0` の場合、CDNがリクエストの最初のバイトを転送開始した時点で、このレート制限ルールが有効になります。 |`1000` |
|SpeedLimitTime |Object |スロットリングルールが有効になる日付と時間帯を表します。 | |
|DayWeek |String |このスロットリングルールが有効になる日付を表します。`monday`、`tuesday`、`wednesday`、`thursday`、`friday`、`saturday`、`sunday`、`unlimited` の値があります。<br><br>`unlimited` は毎日を意味します。複数の日付はセミコロン（;）で区切られます。 |`monday;friday` |
|BeginTime |String |このスロットリングルールが有効になる開始時間を `mm:ss` 形式で表します。 |`23:01` |
|EndTime |String |このスロットリングルールが有効になる終了時間を `mm:ss` 形式で表します。 |`16:48` |
|Condition |Object |マッチング条件の設定を表します。リクエストが条件にマッチした場合、CDNはそのリクエストに対して `DownloadSpeedLimitAction` で指定された操作を実行します。<br><br>このパラメータが存在しないか `null` の場合、CDNはすべてのリクエストに対して `DownloadSpeedLimitAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：完全なリクエストパスを表します。<br><br>* `unlimited`：ドメイン名下のすべてのファイルを表します。<br><br>* `regex`：正規表現を使用してマッチする完全なリクエストパスを表します。 |`filetype` |
|Operator |String |マッチタイプを表します。このパラメータの値は `match` のみで、`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。 | |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`/www/img/volc/;/www/doc/` |
|Name |String | | |
|FollowRedirect |Boolean |「リダイレクトフォロー」機能の設定を表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|HTTPS |Object |HTTPS暗号化サービスの設定を表します。 | |
|Switch |Boolean |HTTPS暗号化サービスを有効にするかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：HTTPS暗号化サービスを有効にすることを示します。<br><br>* `false`：HTTPS暗号化サービスを無効にすることを示します。 |`true` |
|CertInfo |Object |ドメイン名に関連付ける証明書を表します。 | |
|CertId |String |関連付ける証明書のIDを表します。 |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
|Certificate |Object |アップロードする証明書を表します。アップロードされた証明書はCDNでホストされます。 | |
|Certificate |String |証明書ファイルの内容を表します。内容の改行は  | |
|`-----BEGIN CERTIFICATE----- MIIEBj....9X/eM4= -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- MI....Es= -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- M...g== -----END CERTIFICATE-----` | | で置き換える必要があります。この証明書ファイルの拡張子は .crt または .pem であり、証明書ファイルには完全な証明書チェーンが含まれている必要があります。<br><br><br>&nbsp;<br><br>* この証明書がRSAまたはECC暗号アルゴリズムを使用している場合、このファイルはアップロードするサーバー証明書の証明書ファイルです。ファイル名は `<domain>.crt` のようになります。<br><br>* この証明書がSM2暗号アルゴリズムを使用している場合、このファイルはアップロードする国密証明書の証明書ファイルで、署名の検証に使用されます。ファイル名は `<domain>_sign.crt` のようになります。<br><br><br>アップロードする証明書の場合、このパラメータは必須です。 | |
|PrivateKey |String |秘密鍵ファイルの内容を表します。内容の改行は  | |
|`-----BEGIN RSA PRIVATE KEY----- cdvfvg....cdcd== -----END RSA PRIVATE KEY-----` | | に置き換える必要があります。この秘密鍵ファイルの拡張子は .key または .pem です。<br><br><br>&nbsp;<br><br>* この証明書が使用する暗号化アルゴリズムが RSA または ECC の場合、このファイルはアップロードするサーバー証明書の秘密鍵ファイルです。ファイル名は `<domain>.key` のようになります。<br><br>* この証明書が使用する暗号化アルゴリズムが SM2 の場合、このファイルはアップロードする国密証明書の秘密鍵ファイルで、署名の生成に使用されます。ファイル名は `<domain>_sign.key` のようになります。<br><br><br>アップロードする証明書の場合、このパラメータは必須です。 | |
|EncryptionCert |String |国密証明書の証明書ファイルの内容を表します。内容の改行は  | |
| | | で置き換える必要があります。このファイルは暗号化に使用され、拡張子は .crt または .pem です。ファイル名は `<domain>_encrypt.crt` のようになります。<br><br>&nbsp;<br><br>アップロードする証明書が国密証明書でない場合、このパラメータは無効です。 | |
|EncryptionKey |String |国密証明書の秘密鍵ファイルの内容を表します。内容の改行は | |
| | |で置き換える必要があります。このファイルは復号に使用され、拡張子は.keyまたは.pemです。ファイル名は`<domain>_encrypt.key`のようになります。<br><br>&nbsp;<br><br>アップロードする証明書が国密証明書でない場合、このパラメータは無効です。 | |
|EncryType |String |このパラメータは無効です。無視してください。 | |
|CertInfoList |Object[] |ドメイン名に関連付けるデュアル証明書を表します。 | |
|CertId |String |デュアル証明書のうちの一つの証明書のIDを表します。<br><br>[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCertInfo_jp)を呼び出して、指定したい証明書のIDを取得できます。 | |
|CertName |String |このパラメータは無効です。無視してください。 | |
|Certificate |Object |このパラメータは無効です。無視してください。 | |
|Certificate |String |このパラメータの説明は、前述の `Certificate` 構造体下の `Certificate` と同じです。 | |
|PrivateKey |String |このパラメータの説明は、前述の `Certificate` 構造体下の `PrivateKey` と同じです。 | |
|EncryptionCert |String |このパラメータの説明は、前述の `Certificate` 構造体下の `EncryptionCert` と同じです。 | |
|EncryptionKey |String |このパラメータの説明は、前述の `Certificate` 構造体下の `EncryptionKey` と同じです。 | |
|Desc |String |このパラメータは無効です。無視してください。 | |
|EffectiveTime |Long |このパラメータは無効です。無視してください。 | |
|ExpireTime |Long |このパラメータは無効です。無視してください。 | |
|Source |String |このパラメータは無効です。無視してください。 | |
|EncryType |String |このパラメータは無効です。無視してください。 | |
|DisableHttp |Boolean |リクエストURLのスキームが`HTTP`のリクエストを許可するかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：スキームが`HTTP`のリクエストを許可することを示します。<br><br>* `false`：スキームが`HTTP`のリクエストを許可しないことを示します。 |`false` |
|ForcedRedirect |Object |「HTTPからHTTPSへのリダイレクト」機能の設定を表します。<br><br>说明<br><br>CDNは2種類のプロトコルリダイレクト機能を提供します。<br><br><br>* HTTPからHTTPSへのリダイレクト、つまり`ForcedRedirect`機能。<br><br>* HTTPSからHTTPへのリダイレクト、つまり`HttpForcedRedirect`機能。<br><br><br>これら2つのプロトコルリダイレクト機能は相互に排他的です。つまり、一方の機能が有効になると、もう一方の機能は有効にできません。 | |
|EnableForcedRedirect |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。有効にすると、CDNは受け取ったHTTPリクエストをHTTPSリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にすることを示します。無効にすると、CDNはHTTPリクエストをHTTPSリクエストにリダイレクトしません。 |`true` |
|StatusCode |String |HTTPSリクエストを受け取った際のCDNのリダイレクト応答ステータスコードを表します。このパラメータは次の値を取ることができます：<br><br><br>* `301`：返されるステータスコードが301であることを示します。<br><br>* `302`：返されるステータスコードが302であることを示します。 |`301` |
|HTTP2 |Boolean |ユーザーからのリクエストに対してHTTP/2サポートを有効にするかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：HTTP/2を有効にすることを示します。<br><br>* `false`：HTTP/2を無効にすることを示します。 |`true` |
|Hsts |Object |HSTS機能の設定を表します。 | |
|Subdomain |String |HSTS設定がドメイン名のサブドメインにも適用されるかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `include`：HSTS設定がサブドメインサイトに適用されることを示します。<br><br>* `exclude`：HSTS設定がサブドメインサイトに適用されないことを示します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|Ttl |Long |`Strict-Transport-Security` レスポンスヘッダーのブラウザでのキャッシュ有効期限を秒単位で表します。<br><br>このパラメータ値が `0` の場合、HSTS設定を無効にするのと同じ効果があります。 | |
|OCSP |Boolean |「OCSP Stapling」機能を有効にするかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|TlsVersion |String[] |「TLSバージョン」機能の設定を表します。このパラメータは、ユーザーからのリクエストが使用できるTLSバージョンを指定し、次の値があります：<br><br><br>* `tlsv1.0`：TLS 1.0を表します。<br><br>* `tlsv1.1`：TLS 1.1を表します。<br><br>* `tlsv1.2`：TLS 1.2を表します。<br><br>* `tlsv1.3`：TLS 1.3を表します。 |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |「相互認証」機能の設定を表します。「相互認証」を設定するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。 | |
|CertInfoList |Object[] |ドメイン名に関連付けるCA証明書のリストを表します。リストには最大2つのCA証明書を含めることができます。これらのCA証明書は、すでにCDNでホストされている必要があります。CA証明書が使用する暗号化アルゴリズムは、RSA、ECC、またはSM2のいずれかです。<br><br>関連付ける証明書がまだアップロードされていない場合は、[AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/AddCertificate_jp)を呼び出して証明書をCDNにアップロードし、その後`UpdateCdnConfig`を呼び出して証明書を関連付けることができます。 | |
|CertId |String |CA証明書のIDを表します。IDは `cert_hosting-` で始まります。<br><br>[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCertInfo_jp)を呼び出して、関連付けたい証明書のIDを取得できます。 | |
|CertName |String |このパラメータは無効です。無視してください。 | |
|Certificate |Object |アップロードするCA証明書を表します。アップロードされた証明書はCDNでホストされます。このパラメータを使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。 | |
|Certificate |String |CA証明書ファイルの内容を表します。内容の改行は  | |
| | | で置き換える必要があります。このファイルの拡張子は .crt または .pem です。 | |
|EncryptionCert |String |このパラメータは無効です。無視してください。 | |
|EncryptionKey |String |このパラメータは無効です。無視してください。 | |
|PrivateKey |String |このパラメータは無効です。無視してください。 | |
|Desc |String |このパラメータは無効です。無視してください。 | |
|EffectiveTime |Long |このパラメータは無効です。無視してください。 | |
|EncryType |String |このパラメータは無効です。無視してください。 | |
|ExpireTime |Long |このパラメータは無効です。無視してください。 | |
|Source |String |このパラメータは無効です。無視してください。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 | |
|HttpForcedRedirect |Object |「HTTPSからHTTPへのリダイレクト」機能の設定を表します。 | |
|EnableForcedRedirect |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。有効にすると、CDNは受け取ったHTTPSリクエストをHTTPリクエストにリダイレクトします。<br><br>* `false`：この機能を無効にすることを示します。CDNはHTTPSリクエストをHTTPリクエストにリダイレクトしません。 |`true` |
|StatusCode |String |HTTPSリクエストを受け取った際、CDNが返すリダイレクトステータスコードを表します。このパラメータは次の値を取ります：**301**、**302**、**303**、**307**、**308**。<br><br>注意点：<br><br><br>* 301と302の場合、元のリクエストがGET以外のメソッドを使用していた場合、クライアントが新しいURLにリクエストを送信する際、新しいリクエストのメソッドがGETに変わることがあります。<br><br>* 303の場合、新しいリクエストのメソッドはGETです。<br><br>* 307と308の場合、新しいリクエストのメソッドは元のリクエストと同じで、変更されません。 |`302` |
|IPv6 |Object |IPv6設定を表します。 | |
|Switch |Boolean |ユーザーからのリクエストに対してIPv6サポートを有効にするかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：IPv6を有効にすることを示します。<br><br>* `false`：IPv6を無効にすることを示します。 |`true` |
|IpAccessRule |Object |「IPブロックリスト/アローリスト」機能の設定を表します。<br><br>この機能には2つの設定方法があります：<br><br><br>* 通常設定：`RuleType`と`Ip`を指定して現在のドメイン名を設定します。<br><br>* ユニバーサルカタログ：`SharedConfig`を指定してユニバーサルカタログを使用します。 | |
|Ip |String[] |ブロックリストまたはアローリストのIPアドレスを表します。 |`["78.201.79.19","2.2.2.2"]` |
|RuleType |String |IPリストのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `allow`：アローリストを表します。<br><br>* `deny`：ブロックリストを表します。 |`deny` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|SharedConfig |Object |ユニバーサルカタログを表します。 |`["78.201.79.19","2.2.2.2"]` |
|ConfigName |String |ユニバーサルカタログの名前を表します。このユニバーサルカタログの`ConfigType`は`deny_ip_access_rule`または`allow_ip_access_rule`でなければなりません。<br><br><br>* `deny_ip_access_rule`：IPブロックリストを表します。<br><br>* `allow_ip_access_rule`：IPアローリストを表します。<br><br><br>[ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn)を呼び出してユニバーサルカタログのリストを取得できます。 |`my_whitelist` |
|MethodDeniedRule |Object |「HTTPメソッドを無効にする」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|Methods |String |無効にされた1つ以上のHTTPリクエストメソッドを表します。複数のメソッドはカンマ（,）で区切られます。このパラメータは次の値を取ることができます：<br><br><br>* `get`：GETリクエストメソッドを無効にすることを示します。<br><br>* `post`：POSTリクエストメソッドを無効にすることを示します。<br><br>* `delete`：DELETEリクエストメソッドを無効にすることを示します。<br><br>* `put`：PUTリクエストメソッドを無効にすることを示します。<br><br>* `head`：HEADリクエストメソッドを無効にすることを示します。<br><br>* `patch`：PATCHリクエストメソッドを表します。<br><br>* `connect`：CONNECTリクエストメソッドを表します。<br><br>* `options`：OPTIONSリクエストメソッドを表します。 |`delete,put` |
|NegativeCache |Object[] |「ステータスコードキャッシュ」機能の設定を表し、ルールリストが含まれています。説明は以下の通りです：<br><br><br>* 各ルールには、マッチング条件設定と操作設定が含まれています。<br><br>* リスト内のルールの順序は、ルールの優先順位を示します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ると、CDNはルールの優先順位に従って、高いものから低いものへとリクエストをマッチングさせます。リクエストがルールにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|NegativeCacheRule |Object |リクエストが `Condition` のマッチング条件を満たす場合、CDN はリクエストされたファイルに対して指定された操作を実行します。このパラメータは、その操作に関連する設定を定義します。 | |
|StatusCode |String |キャッシュするステータスコードを表し、範囲は `400-599` です。`4xx` または `5xx` も可能です。`4xx` は400から499までのすべてのステータスコードを、`5xx` は500から599までのすべてのステータスコードを表します。 |`403` |
|Ttl |Long |ステータスコードのキャッシュ時間を `秒` 単位で表します。 |`100` |
|IgnoreCase |Boolean |`Value` が大文字と小文字を区別するかどうかを示します。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。 |`true` |
|Condition |Object |マッチング条件の設定を表します。リクエストが特定の条件にマッチした場合、CDNはそのリクエストに対して `NegativeCacheRule` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。 |`directory` |
|Operator |String |マッチタイプを表します。このパラメータの値は `match` のみで、`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`png` |
|Name |String | | |
|OriginAccessRule |Object |「オリジンブロックリスト/アローリスト」機能の設定を表します。 | |
|AllowEmpty |Boolean |ユーザーリクエストヘッダーのOriginヘッダーが空（""）の場合に、リクエストを許可するかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：許可することを示します。<br><br>* `false`：許可しないことを示します。 |`true` |
|IgnoreCase |Boolean |Originリストが大文字と小文字を区別するかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：Originリストが大文字と小文字を区別しないことを示します。<br><br>* `false`：Originリストが大文字と小文字を区別することを示します。 |`true` |
|Origins |String[] |Originのリストを表します。 |`["www.test.com"]` |
|RuleType |String |Originリストのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `allow`：アローリストを表します。<br><br>* `deny`：ブロックリストを表します。 |`deny` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|OriginArg |Object[] |「オリジンリクエストのパラメータ」設定のルールリストを表します。<br><br><br>* 各ルールには、マッチング条件（`Condition`）とCDNが実行する操作（`OriginArgAction`）が含まれます。<br><br>* リスト内のルールの順序は、ルールの優先順位を定義します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとルールとリクエストをマッチングさせます。ルールがリクエストにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|Condition |Object |マッチング条件の設定を表します。リクエストがこのマッチング条件を満たす場合、CDNは `OriginArgAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチングタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。<br><br>* `regex`：正規表現を使用してリクエストURLの完全なパスをマッチングします。 |`directory` |
|Operator |String |マッチングタイプを表します。現在、このパラメータ値は `match` のみで、マッチングが成功した場合にのみマッチング条件を満たしたとみなされます。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 |`/` |
|Name |String | | |
|Connective |String |現在、このパラメータを設定することはできません。このパラメータを指定しないか、値を `OR` に設定することができます。 | |
|OriginArgAction |Object |リクエストが `Condition` を満たすときにCDNが実行する操作を表します。 | |
|OriginArgComponents |Object[] |操作のリストを表します。これらの操作は、CDNがオリジンリクエストのクエリパラメータをどのように処理するかを定義します。 | |
|Object |String |CDNが `Action` をどのオブジェクトに対して実行するかを示します。現在、このパラメータ値は `queryString` のみで、リクエストURLのクエリ文字列を表します。 |`queryString` |
|Subobject |String |1つ以上のクエリパラメータを表します。複数のクエリパラメータはセミコロン（;）で区切られます。<br><br>リクエストURLのクエリパラメータと照合する際、`Subobject` のパラメータは大文字と小文字を区別します。<br><br>`Subobject` が `*` の場合、リクエストURLのすべてのクエリパラメータを表します。 |`*` |
|OriginHost |String |オリジンサーバーに複数のサイトがある場合、このパラメータはオリジンリクエストがアクセスするサイトのドメイン名を表します。このパラメータはすべてのオリジンサーバー設定に有効ですが、オリジンサーバー設定の`OriginHost`パラメータよりも優先度は低いです。 |`www.test.com` |
|OriginRange |Boolean |「レンジGET」機能の設定を表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|OriginRewrite |Object |「オリジンURL書き換え」機能の設定を表します。 | |
|OriginRewriteRule |Object[] |ルールリストを表します。`Switch` が `true` の場合、このパラメータは必須です。<br><br><br>* リスト内のルールの順序は、ルールの優先順位を定義します。リストの最初のルールが最も優先順位が高いです。<br><br>* ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとリクエストをルールとマッチングさせようとします。リクエストがルールにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|OriginRewriteAction |Object |CDNが実行するアクションを表します。 | |
|SourcePath |String |ユーザーからのリクエストURLのパスに一致する正規表現を表します。[設定例](https://docs.byteplus.com/en/docs/byteplus-cdn/url-rewrite-jp)を参照してください。 |`/img/volcano.png` |
|TargetPath |String |書き換え後のパスを表します。[設定例](https://docs.byteplus.com/en/docs/byteplus-cdn/url-rewrite-jp)を参照してください。 |`/png/volcano.png` |
|RewriteType |String |書き換えタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `rewrite_path`：リクエストURLのパスを書き換えることを示します。<br><br>* `rewrite_url`：リクエストURLのパスとクエリ文字列を書き換えることを示します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|OriginSni |Object |「オリジンサーバーのSNI」機能の設定を表します。 | |
|SniDomain |String |オリジンサーバーのSNIのドメイン名を指定します。 |`img.example.com` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|PageOptimization |Object |「ファイル最小化」機能の設定を表します。 | |
|OptimizationType |String[] |最適化の対象を表します。このパラメータは次の値を取ることができます：<br><br><br>* `html`：HTMLページを表します。<br><br>* `js`：Javascriptコードを表します。<br><br>* `css`：CSSコードを表します。 |`["html","js"]` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|Quic |Object |QUIC設定を表します。 | |
|Switch |Boolean |ユーザーからのリクエストに対してQUICを有効にするかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：QUICを有効にすることを示します。<br><br>* `false`：QUICを無効にすることを示します。 |`true` |
|RedirectionRewrite |Object |「URLリダイレクト」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|RedirectionRule |Object[] |URLリダイレクトルールのリストを表します。リストの最初のルールが最も優先順位が高いです。<br><br>ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとルールとリクエストをマッチングさせます。ルールがリクエストにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|RedirectionAction |Object |URLリダイレクトルールを表します。 | |
|RedirectCode |String |URLリダイレクトのレスポンスステータスコードを表します。このパラメータの値には `301`、`302`、`303`、`307`、`308` があります。<br><br>注意点：<br><br><br>* 301と302の場合、元のリクエストがGET以外のメソッドを使用していると、クライアントが新しいURLにリクエストを送信する際に、新しいリクエストのメソッドがGETに変わることがあります。<br><br>* 303の場合、新しいリクエストのメソッドはGETです。<br><br>* 307と308の場合、新しいリクエストのメソッドは元のリクエストと同じで、変更されません。 |`301` |
|SourcePath |String |ファイルの元のパスを表します。つまり、リクエストに含まれるパスです。 |`/img/volcano.png` |
|TargetHost |String |ターゲットパスが属するドメイン名またはIPアドレスを表します。 |`www.test.com` |
|TargetPath |String |リダイレクト後のターゲットパスを表します。 |`/png/volcano.png` |
|TargetProtocol |String |URLリダイレクト後の新しいリクエストが使用するプロトコルを表します。このパラメータは次の値を取ることができます：<br><br><br>* `followclient`：元のリクエストのプロトコルを使用することを示します。<br><br>* `http`：新しいリクエストが強制的にHTTPプロトコルを使用することを示します。<br><br>* `https`：新しいリクエストが強制的にHTTPSプロトコルを使用することを示します。 |`followclient` |
|TargetQueryComponents |Object |元のリクエストURLのクエリパラメータの処理方法を表します。 | |
|Value |String |保持または削除するクエリパラメータを表します。複数のクエリパラメータは英語のセミコロン（;）で区切られます。`Value` が `*` の場合、すべてのクエリパラメータを表します。 |`seq` |
|RefererAccessRule |Object |「Refererブロックリスト/アローリスト」機能の設定を表します。異なる設定がリクエストマッチング結果に与える影響については、[Referer制限](https://docs.byteplus.com/en/docs/byteplus-cdn/referer-restrictions-jp#%E9%85%8D%E7%BD%AE%E7%A4%BA%E4%BE%8B)を参照してください。 | |
|AllowEmpty |Boolean |ユーザーからのリクエストにRefererヘッダーが含まれていない場合、CDNがリクエストを処理する方法を示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：リクエストにRefererヘッダーが含まれていない場合、そのリクエストは設定されたRefererリストに一致すると見なされることを示します。<br><br>* `false`：リクエストにRefererヘッダーが含まれていない場合、そのリクエストは設定されたRefererリストに一致しないと見なされることを示します。 |`true` |
|Referers |String[] |Refererのリストを表します。Referersは`ReferersType`でも指定できます。 |`["www.test.com","11.11.11.11","12.12.12.0/24"]` |
|ReferersType |Object |`ReferersType` オブジェクトを表します。これには、`CommonType` オブジェクトと `RegularType` オブジェクトが含まれ、それぞれ通常のRefererリストとRefererを照合するための正規表現リストを表します。`CommonType` と `RegularType` は同時に存在できます。 | |
|CommonType |Object |`CommonType` オブジェクトを表し、通常のRefererリストを含みます。 | |
|IgnoreCase |Boolean |`CommonType`下の`Referers`リストが大文字と小文字を区別するかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。 |`true` |
|Referers |String[] |通常のRefererリストを表します。 |`["www.test.com","11.11.11.11","12.12.12.0/24"]` |
|IgnoreScheme |Boolean |CDNがRefererのスキームを検証するかどうか、つまりRefererに`http://`または`https://`が含まれているかを検証するかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：CDNはRefererにスキームが含まれているかどうかを検証しません。この場合、Refererにスキームが含まれているかどうかに関わらず、CDNはRefererを設定されたリストと照合します。<br><br>* `false`：CDNはまずRefererにスキームが含まれているかどうかを検証します。Refererにスキームが含まれている場合にのみ、CDNはRefererを設定されたリストと照合します。そうでない場合、CDNはリクエストが設定されたリストと一致しないと判断します。<br><br><br>この設定は`RegularType`下の正規表現リストには適用されません。なぜなら、CDNは正規表現に依存してRefererが正規表現リストに一致するかどうかを判断するためです。 |`false` |
|RegularType |Object |`RegularType` オブジェクトを表し、リクエスト内のRefererヘッダーを照合するための正規表現リストを含みます。 | |
|Referers |String[] |Refererに一致する正規表現のリストを表します。 |`^http://a.com` |
|RuleType |String |Refererリストのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `allow`：アローリストを表します。<br><br>* `deny`：ブロックリストを表します。 |`deny` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|SharedConfig |Object |ユニバーサルカタログを表します。 | |
|ConfigName |String |ユニバーサルカタログの名前を表します。このユニバーサルカタログの`ConfigType`は`deny_referer_access_rule`または`allow_referer_access_rule`でなければなりません。<br><br><br>* `deny_referer_access_rule`：Refererブロックリストを表します。<br><br>* `allow_referer_access_rule`：Refererアローリストを表します。<br><br><br>[ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_cn)を呼び出してユニバーサルカタログのリストを取得できます。 | |
|RemoteAuth |Object |「リモート認証」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|RemoteAuthRules |Object[] |認証ルールのリストを表します。各ルールには、マッチング条件の設定と認証設定が含まれます。 | |
|Condition |Object |マッチング条件の設定を表します。リクエストがマッチング条件を満たす場合、CDNはそのリクエストに対して `RemoteAuthRuleAction` で指定された操作を実行します。 | |
|ConditionRule |Object[] |マッチ条件のリストを表します。<br><br>これらのマッチ条件間の関係は「OR」であり、リクエストが任意のマッチ条件を満たす場合、CDNはそのリクエストに対して`RemoteAuthRuleAction`で指定された操作を実行します。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストURLの拡張子を表します。<br><br>* `directory`：リクエストURLの特定のディレクトリを表します。<br><br>* `path`：リクエストURLの完全なパスを表します。 |`directory` |
|Operator |String |マッチタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `match`：`Value` がリクエスト内の `Object` にマッチした場合、そのリクエストはこのマッチ条件を満たすことを示します。<br><br>* `not_match`：`Value` がリクエスト内の `Object` にマッチしない場合、そのリクエストはこのマッチ条件を満たすことを示します。 |`match` |
|Type |String |このパラメータ値は `url` のみで、「リクエストURL」を表します。 |`url` |
|Value |String |1つまたは複数のマッチ値を表し、複数の値はセミコロン（;）で区切られます。 | |
|Name |String | | |
|Connective |String |複数の `ConditionRule` 間の論理関係を表します。現在、このパラメータを設定することはできません。このパラメータを指定しないか、値を `OR` に設定することができます。 |`OR` |
|RemoteAuthRuleAction |Object |認証関連の設定を表します。<br><br>リクエストが `Condition` のマッチング条件を満たすと、CDNはそれを認証サーバーに送信して認証を行い、認証結果に基づいてリクエストを受け入れるか拒否します。 | |
|AuthModeConfig |Object |認証サーバーの設定を表します。 | |
|MasterRemoteAddr |String |認証サーバーのプライマリアドレスを表します。 | |
|PathType |String |認証リクエストのパスを表します。認証アドレスとリクエストパスが完全な認証URLを構成します。CDNはユーザーのリクエストをこの認証URLに転送します。このパラメータは次の値を取ることができます：<br><br><br>* `constant`：認証リクエストのパスがユーザーリクエストのパスと同じであることを示します。<br><br>* `variable`：`pathValue`で指定されたパスを示します。 | |
|RequestMethod |String |認証リクエストを送信する際にCDNが使用するリクエストメソッドを表します。このパラメータは次の値を取ることができます：<br><br><br>* `default`：認証リクエストが使用するメソッドがユーザーのリクエストと同じであることを示します。<br><br>* `get`：認証リクエストがGETメソッドを使用することを示します。<br><br>* `post`：認証リクエストがPOSTメソッドを使用することを示します。<br><br>* `head`：認証リクエストがHEADメソッドを使用することを示します。 | |
|BackupRemoteAddr |String |認証サーバーのバックアップアドレスを表します。 | |
|PathValue |String |認証リクエストのパスを表します。 | |
|AuthResponseConfig |Object |CDNは認証サーバーから返された認証ステータスコードを処理する必要があります。このパラメータは関連する設定を表します。 | |
|CacheAction |Object |CDNは認証ステータスコードをキャッシュできます。このパラメータは関連する設定を表します。 | |
|Ttl |Long |認証ステータスコードのキャッシュ時間を秒単位で表します。 |`5` |
|CacheKey |String[] |キャッシュキーは、異なるリクエストURIを区別するために使用されるクエリパラメータを指定します。各パラメータは `$` で始まる必要があります。[リモート認証](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication-jp#variables)のパラメータを参照してください。 |`[$URI,$host]` |
|ResponseAction |Object |認証が失敗した場合、CDNがユーザーにどのように応答するかを示します。 | |
|StatusCode |String |認証が失敗したときにCDNがユーザーに応答するステータスコードを表します。 |`403` |
|StatusCodeAction |Object |CDNが認証ステータスコードを処理する方法を表します。 | |
|DefaultAction |String |認証ステータスコードが `FailCode` でも `SuccessCode` でもない場合、CDNが認証リクエストを処理する方法を示します。このパラメータは次の値を取ることができます：<br><br><br>* `reject`：CDNが認証失敗と見なすことを示します。<br><br>* `pass`：CDNが認証成功と見なすことを示します。 |`pass` |
|FailCode |String |認証失敗時の認証ステータスコードを表します。複数のステータスコードは英語のセミコロン（;）で区切られます。 |`403` |
|SuccessCode |String |認証成功時の認証ステータスコードを表します。複数のステータスコードは英語のセミコロン（;）で区切られます。 |`200` |
|TimeOutAction |Object |認証タイムアウト後、CDNが認証リクエストをどのように処理するかを示します。 | |
|Time |Long |認証タイムアウト時間をミリ秒単位で表します。 |`200` |
|QueryStringRules |Object |認証リクエストのパラメータ設定を表します。 | |
|QueryStringComponents |Object |認証リクエストパラメータの設定ポリシーを表します。 | |
|Value |String |`Action` パラメータに対応するパラメータ値を表します。`*` はすべてのクエリパラメータを表します。 |`*` |
|QueryStringInstances |Object[] |認証リクエストの追加パラメータ設定を表します。 | |
|Key |String |設定する認証リクエストパラメータを表します。 |`sign` |
|Value |String |認証リクエストパラメータの値を表し、大文字と小文字を区別します。 |`1235565` |
|ValueType |String |`Key` で指定された認証リクエストパラメータのタイプ。`ValueType` は次の値を取ります：<br><br><br>* `constant`：認証リクエストパラメータが定数であることを示します。<br><br>* `variable`：認証リクエストパラメータの値が変数から来ることを示します。`Value` の説明を参照してください。<br><br>* `customize`：認証リクエストパラメータの値が変数と固定文字列を連結した文字列であることを示します。 |`variable` |
|RequestBodyRules |String |認証リクエストの本文ルールを表します。このパラメータを指定しないか、値を `default` に設定することができます。`default` はリクエスト本文が空（""）であることを示します。 |`default` |
|RequestHeaderRules |Object |認証リクエストヘッダーの設定を表します。 | |
|RequestHeaderComponents |Object |認証リクエストヘッダーの設定ポリシーを表します。 | |
|Value |String |`Action` パラメータに対応するパラメータ値を表します。パラメータ値が `*` の場合、すべてのリクエストヘッダーを表します。 |`*` |
|RequestHeaderInstances |Object[] |認証リクエストヘッダーの設定一式を表します。<br><br>CDNが認証リクエストを開始する際、リクエストにはすでに以下のヘッダーが含まれている可能性があることに注意してください：<br><br><br>* `X-Forwarded-Protocol`、`X-Forwarded-Proto`、`X-Client-Scheme`：これら3つのヘッダーはすべてユーザーリクエストが使用するプロトコルを表し、違いはありません。<br><br>* `X-Real-IP`：ユーザーの実際のIPアドレスを表します。このヘッダーの値はプロキシサーバーの影響を受けません。<br><br>* `X-Forwarded-For`：ユーザーのIPアドレスを表します。ユーザーのリクエストがプロキシサーバーを経由した場合、このヘッダーの値はプロキシサーバーのIPアドレスになります。 | |
|Key |String |設定するリクエストヘッダーを表します。 |`x-test-header` |
|ValueType |String |リクエストヘッダーのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `constant`：リクエストヘッダーの値が定数であることを示します。<br><br>* `variable`：リクエストヘッダーの値が変数から来ることを示します。<br><br>* `customize`：リクエストヘッダーの値が変数と固定文字列を連結した文字列であることを示します。 |`variable` |
|Value |String |リクエストヘッダーの値を表します。 |`1234fdf` |
|RequestHost |String |認証リクエストのHOSTヘッダーの値を表します。このパラメータのデフォルト値は `default` で、HOSTヘッダーの値がドメイン名と同じであることを示します。 |`www.example.com` |
|RequestHeader |Object[] |「オリジンリクエストのヘッダー」機能の設定を表します。 | |
|RequestHeaderAction |Object |リクエストヘッダーの設定ルールリストを表します。各ルールには、ヘッダー関連の操作設定が含まれます。 | |
|RequestHeaderInstances |Object[] |リクエストヘッダーの設定ルールリストを表します。各ルールには、ヘッダー関連の操作設定が含まれます。 | |
|Key |String |ヘッダー名を表し、大文字と小文字を区別しません。 |`Cdn-provider` |
|ValueType |String |`Key` の値のタイプを表します。このパラメータは `Action` が `set` の場合にのみ有効です。このパラメータは次の値を取ることができます：<br><br><br>* `constant`：`Key` の値が固定文字列であることを示します。<br><br>* `variable`：`Key` の値が変数から来ることを示します。<br><br>* `customize`：`Key` の値が変数と固定文字列を連結した文字列であることを示します。 |`constant` |
|Value |String |`Key` の値を表します。 |`volc-cdn` |
|ResponseHeader |Object[] |「HTTPレスポンスヘッダー」機能の設定を表します。 | |
|ResponseHeaderAction |Object |CDNがユーザーからのリクエストに応答する際、レスポンスヘッダーに対する操作を表します。 | |
|ResponseHeaderInstances |Object[] |レスポンスヘッダーの設定ルールリストを表します。各ルールには、ヘッダー関連の操作設定が含まれています。 | |
|Key |String |ヘッダーの名前を表します。 |`Content-Disposition` |
|ValueType |String |`Key` の値のタイプを表します。このパラメータは `Action` が `set` の場合にのみ有効です。このパラメータは次の値を取ることができます：<br><br><br>* `constant`：`Key` の値が文字列であることを示します。<br><br>* `variable`：`Key` の値が変数から来ることを示します。<br><br>* `customize`：`Key` の値が変数と文字列を連結した文字列であることを示します。 |`constant` |
|AccessOriginControl |Boolean |CDNがユーザーからのリクエストに応答する際、リクエストのOriginヘッダーを検証するかどうかを示します。<br><br>このパラメータは次の値を取ります：<br><br><br>* `true`：CDNがOriginヘッダーを検証することを示します。検証が成功した場合、CDNはレスポンスにAccess\-Control\-Allow\-Originヘッダーを含めます。ヘッダー値はOriginヘッダー値と同じです。検証が失敗した場合、レスポンスにAccess\-Control\-Allow\-Originヘッダーは含まれません。<br><br>* `false`：CDNがOriginヘッダーを検証しないことを示します。レスポンスで、CDNはAccess\-Control\-Allow\-Originヘッダーを含めます。ヘッダー値は設定されたAccess\-Control\-Allow\-Originの内容です。<br><br><br>このパラメータは以下のすべての条件が満たされた場合にのみ有効です：<br><br><br>* `Action`が`set`である。<br><br>* `Key`が`Access-Control-Allow-Origin`である。<br><br>* `ValueType`が`constant`である。 | |
|Value |String |`Key` の値を表します。 |`attachment;filename=FileName.xls` |
|ServiceRegion |String |ドメイン名のサービス地域を表します。このパラメータは次の値を取ることができます：<br><br><br>* `chinese_mainland`：中国本土を表します。<br><br>* `global`：全世界を表します。<br><br>* `outside_chinese_mainland`：全世界（中国本土を除く）を表します。 |`outside_chinese_mainland` |
|SignedUrlAuth |Object |「URL認証」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|SignedUrlAuthRules |Object[] |ルールリストを表します。各ルールには、マッチング条件の設定と認証設定が含まれます。 | |
|Condition |Object |マッチング条件の設定を表します。CDNは条件を満たすユーザーからのリクエストを認証します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチング条件のマッチングタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：URLパス末尾の拡張子を表します。<br><br>* `directory`：URLパスのディレクトリを表します。<br><br>* `path`：完全なURLパスを表します。<br><br>* `regex`：正規表現を使用して完全なURLパスをマッチングします。 |`directory` |
|Operator |String |マッチング条件のマッチング方法を表します。このパラメータは次の値を取ることができます：<br><br><br>* `match`：`object`が`Value`に一致する場合、このリクエストはこのマッチング条件を満たすことを示します。<br><br>* `not_match`：`object`が`Value`に一致しない場合、このリクエストはこのマッチング条件を満たすことを示します。 |`match` |
|Type |String |マッチオブジェクトを表します。現在、このパラメータ値は`url`である必要があり、URLリクエストリンクを表します。 |`url` |
|Value |String |マッチング条件のマッチング値を表します。 |`png;jpg` |
|Name |String | | |
|Connective |String |複数の`ConditionRule`間の論理関係を表します。このパラメータは次の値を取ることができます：<br><br><br>* `AND`：論理関係が「AND」であることを示します。<br><br>* `OR`：論理関係が「OR」であることを示します。 |`OR` |
|SignedUrlAuthAction |Object |署名計算の設定を表します。 | |
|Duration |Long |署名の有効期間を秒単位で表します。このパラメータはリクエストに含まれるタイムスタンプと組み合わせて使用され、署名の有効期限を計算します。署名の有効期限 = タイムスタンプ + `Duration`。CDNがあるリクエストを受け取ったとき、署名の有効期限が現在時刻より前の場合、CDNは署名が期限切れであると判断します。 |`1000` |
|MasterSecretKey |String |マスターキーを表します。 |`123abc` |
|URLAuthType |String |署名タイプ。このパラメータは`typea`、`typeb`、`typec`、`typed`、`typee`の値を持ち、各タイプの認証説明は[署名付きURL認証の概要](https://docs.byteplus.com/en/docs/byteplus-cdn/signed-url-authentication-jp)を参照してください。 | |
|BackupSecretKey |String |バックアップキーを表します。 |`abc123` |
|CustomVariableRules |Object |カスタム署名計算変数を表します。 | |
|CustomVariableInstances |Object[] |変数のリストを表します。 | |
|Operator |String |変数のマッチング方法を表します。このパラメータの値は `match` のみです。 |`match` |
|Type |String |変数のタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `queryString`：この変数がリクエストのクエリパラメータであることを示します。<br><br>* `requestHeader`：この変数がリクエストのヘッダーフィールドであることを示します。 | |
|Value |String |変数の名前を表します。 | |
|RewriteM3u8 |Boolean |HLSマニフェスト(.m3u8)のリクエストに対し、CDNがマニフェストを修正して各ビデオセグメントの署名を生成し、その署名をURIに追加するかどうかを示します。<br><br>このパラメータは次の値を取ります：<br><br><br>* `true`：マニフェストの修正が必要であることを示します。<br><br>* `false`：マニフェストの修正が不要であることを示します。<br><br><br>说明<br><br>現在、CDNは圧縮ファイルを修正しません。したがって、以下のいずれかの状況では、CDNはマニフェストを修正しません。<br><br><br>* オリジンサーバーのレスポンスに`Content-Encoding`ヘッダーが含まれている。このヘッダーはマニフェストが圧縮されていることを示します。<br><br>* ユーザーからのリクエストが「ファイル圧縮」機能のルールに一致する。 |`true` |
|SignName |String |署名パラメータの名前を表します。 |`sign` |
|SignatureRule |String[] |`URLAuthType`が`typee`の場合、このパラメータは有効で、署名計算に含める必要があるフィールドを示します。署名計算に必ず含める必要があるフィールドは以下の通りです：<br><br><br>* `key`：`MasterSecretKey`または`BackupSecretKey`で指定されたキーを表します。<br><br>* `uri`：ユーザーリクエストのURIを表し、パスとクエリパラメータのみを含みます。<br><br>* `TimeName`：`TimeFormat`で指定されたタイムスタンプを表します。<br><br><br>署名計算に選択的に含めることができるフィールドは以下の通りです：<br><br><br>* `domain`：ドメイン名を表します。<br><br>* `referer`：ユーザーリクエストに含まれるReferer値を表します。<br><br>* `ua`：ユーザーリクエストに含まれるUser\-Agent値を表します。<br><br>* `ip`：ユーザーリクエストのクライアントIPを表します。<br><br>* `origin`：ユーザーリクエストに含まれるOrigin値を表します。<br><br>* カスタム変数：`CustomVariableInstances`で定義した変数の値を表します。<br><br><br>CDNはリストのフィールドの順にこれらのフィールドを連結して文字列を作成し、その文字列のMD5値を計算します。このMD5値が署名となります。 |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |`TimeName` が使用する基数を表します。このパラメータは次の値を取ることができます：<br><br><br>* `decimal`：10進数を表します。<br><br>* `heximal`：16進数を表します。 |`heximal` |
|TimeName |String |タイムスタンプパラメータの名前を表します。 |`t` |
|AuthAlgorithm |String |署名計算に使用されるアルゴリズムを表します。この設定は次の値を取ることができます：<br><br><br>* `md5`：MD5アルゴリズムを表します。<br><br>* `sha256`：SHA\-256アルゴリズムを表します。<br><br><br>このパラメータのデフォルト値は `md5` です。 | |
|AuthRulesF |Object[] |Type\-F設定を表し、ルールリストを含みます。リストの最初のルールが最も優先順位が高いです。<br><br>ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとルールとリクエストをマッチングさせます。ルールがリクエストにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|RuleName |String |ルールリスト内のルールの名前を表します。 | |
|Condition |Object |マッチング条件の設定を表します。リクエストがマッチング条件に適合する場合、CDNはそのリクエストに対してURL認証を実行します。 | |
|ConditionRule |Object[] |マッチング条件のリストを表します。 | |
|Object |String |マッチオブジェクトを表します。このパラメータは次の値を取ることができます：<br><br><br>* `filetype`：リクエストファイルの拡張子を表します。<br><br>* `directory`：リクエストパスの特定のディレクトリを表します。<br><br>* `path`：クエリ文字列を含まない完全なリクエストパスを表します。<br><br>* `regex`：完全なパスに一致する正規表現を表します。 | |
|Operator |String |マッチング演算子を表します。このパラメータは次の値を取ることができます：<br><br><br>* `match`：`Value`がリクエストの`Object`に一致する場合、そのリクエストはこのマッチング条件を満たすことを示します。<br><br>* `not_match`：`Value`がリクエストの`Object`に一致しない場合、そのリクエストはこのマッチング条件を満たすことを示します。 | |
|Type |String |マッチオブジェクトのソースを表します。現在、このパラメータ値は `url` のみで、リクエストURLを表します。 | |
|Value |String |1つまたは複数のマッチ値を表します。複数のマッチ値はセミコロン（;）で区切られます。 | |
|Name |String | | |
|Connective |String |マッチング条件間の関係を表します。このパラメータは次の値を取ることができます：<br><br><br>* `OR`：「OR」関係を表します。<br><br>* `AND`：「AND」関係を表します。 | |
|SecretKey |Object |トークンを計算するためのキーを表します。マスターキーとバックアップキーが含まれます。 | |
|MasterSecretKey |String |マスターキーを表します。 | |
|BackupSecretKey |String |バックアップキーを表します。 | |
|SignCapRule |Object |ユーザーからのリクエストからトークンを取得する方法を表します。 | |
|ArgSegment |Object |`ParamName`または`UriLevel`に基づいて取得したコンテンツを分割して、特定のレベルのセグメントを抽出する必要があるかどうかを示します。このレベルのセグメントが取得すべきトークンです。 | |
|Switch |Boolean |取得したコンテンツを分割する必要があるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。 | |
|Level |Long |コンテンツを複数のレベルのセグメントに分割した後、トークンが存在するレベルを表します。<br><br>レベルが負の整数の場合、右端のセグメントから左に数えることを示します。 | |
|SplitSymbol |String |コンテンツを分割するために使用される区切り文字を表します。 | |
|CapMode |String |トークンのソースを表します。このパラメータは次の値を取ることができます：<br><br><br>* `name`：クエリパラメータを表します。関連する設定は `ParamName` で指定されます。<br><br>* `uri`：リクエストパスのディレクトリを表します。関連する設定は `UriLevel` で指定されます。<br><br>* `header`：リクエストのヘッダーを表します。関連する設定は `CustomValue` で指定されます。<br><br>* `cookie`：リクエストのクッキーを表します。関連する設定は `CustomValue` で指定されます。 | |
|CustomValue |String |このパラメータの意味は以下の通りです：<br><br><br>* `CapMode`が`header`の場合、このパラメータは指定されたリクエストヘッダーを表します。<br><br>* `CapMode`が`cookie`の場合、このパラメータは指定されたクッキーのキーを表し、CDNはそのクッキーの値を取得します。 | |
|ParamName |String |`CapMode` が `name` の場合、このパラメータは指定するクエリパラメータを表します。 | |
|UriLevel |Long |`CapMode` が `uri` の場合、このパラメータは指定されたディレクトリレベルを表します。<br><br>レベルが負の整数の場合、パスの右端のディレクトリから左に数えることを意味します。 | |
|ExpireTimeRule |Object |トークンの有効期限に関する設定を表します。 | |
|Duration |Long |トークンの有効期間（TTL）を秒単位で表します。<br><br><br>* トークンの有効期限 = `ExpTimeCapRule`に基づいて取得されたトークンのタイムスタンプ + `Duration` | |
|ExpTimeCapRule |Object |トークンタイムスタンプの取得方法を表します。トークンタイムスタンプはUnixタイムスタンプです。 | |
|CapMode |String |トークンタイムスタンプのソースを表します。このパラメータは次の値を取ることができます：<br><br><br>* `name`：クエリパラメータを表します。関連する設定は`ParamName`および`ArgSegment`で指定されます。<br><br>* `uri`：リクエストパス内のディレクトリを表します。関連する設定は`UriLevel`および`ArgSegment`で指定されます。<br><br>* `header`：リクエスト内のヘッダーを表します。関連する設定は`CustomValue`で指定されます。<br><br>* `cookie`：リクエスト内のクッキーを表します。関連する設定は`CustomValue`で指定されます。 | |
|ParamName |String |`ParamType`が`ReqHeader`の場合、このパラメータは指定されたクエリパラメータを表します。 | |
|UriLevel |Long |`ParamType` が `uri` の場合、このパラメータは指定されたディレクトリレベルを表します。<br><br>レベルが負の整数の場合、パスの右端のディレクトリから左に数えることを意味します。 | |
|ArgSegment |Object |`ParamName`または`UriLevel`に基づいて取得したコンテンツを分割して、特定のレベルのセグメントを抽出する必要があるかどうかを示します。このレベルのセグメントが取得すべきトークンタイムスタンプです。 | |
|Switch |Boolean |取得したコンテンツを分割する必要があるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。 | |
|Level |Long |コンテンツを複数のレベルのセグメントに分割した後、トークンタイムスタンプが存在するレベルを表します。<br><br>レベルが負の整数の場合、右端のセグメントから左に数えることを示します。 | |
|SplitSymbol |String |コンテンツを分割するために使用される区切り文字を表します。 | |
|CustomValue |String |このパラメータの意味は以下の通りです：<br><br><br>* `CapMode`が`header`の場合、このパラメータは指定されたリクエストヘッダーを表します。<br><br>* `CapMode`が`cookie`の場合、このパラメータは指定されたクッキーのキーを表し、CDNはそのクッキーの値を取得します。 | |
|TimeFormat |String |トークンタイムスタンプのフォーマットを表します。<br><br><br>* `octal`：8進数を表します。例：`14751410031`。<br><br>* `decimal`：10進数を表します。例：`1738936345`。<br><br>* `heximal`：16進数を表します。例：`67a61019`。 | |
|AuthTokenCalRule |Object |トークン計算の設定を表します。<br><br>CDNは`SignJoinSymbol`を使用して`SignParam`内の各オブジェクトを連結し、その後、連結されたオブジェクトに`ParamCalRules`で指定されたアルゴリズムを適用してトークンを計算し、ユーザーリクエストに含まれるトークンと比較します。 | |
|ParamCalRules |String[] |トークンの計算に使用されるアルゴリズムのリストを表します。CDNはリスト内のアルゴリズムの出現順にトークンの計算式を生成します。<br><br>このパラメータは次の値を取ります：`md5_bin`、`base64url`、`sha256`、`md5`、`base64_encode`、`sha1`、`sha224`、`sha384`、`sha512`、`sha3_224`、`sha3_256`、`sha3_384`、`sha3_512`、`upper_case`、`lower_case`。 | |
|SignJoinSymbol |String |`SignParam`内の各オブジェクトを連結するために使用する結合記号を表します。 | |
|SignParam |Object[] |CDNがトークンを計算する際に使用するオブジェクトのリストを表します。各オブジェクトは `ParamType` と関連設定で構成されます。例えば、以下の例はオブジェクトが文字列であり、文字列の値が `str-for-token-calc` であることを示します。<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|ParamType |String |オブジェクトのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `SecretKey`：`SecretKey`構造体の`MasterSecretKey`または`BackupSecretKey`を表します。認証が失敗した場合、CDNは`BackupSecretKey`を使用してトークンを計算し、ユーザーからのリクエストを再認証します。<br><br>* `SupString`：文字列を表します。関連する設定は`SupContent`で指定されます。<br><br>* `URI`：リクエストパス内の連続したセグメントを表します。パスにはクエリ文字列は含まれません。関連する設定は`UriParamSup`と`ParamSource`で指定されます。<br><br>* `URLParam`：リクエストURL内の特定のオブジェクトを表します。オブジェクトはクエリパラメータまたは特定のディレクトリです。関連する設定は`UriParam`と`ParamSource`で指定されます。<br><br>* `ClientDomain`：リクエストドメイン名を表します。<br><br>* `Referer`：ユーザーからのリクエストのRefererヘッダーの値を表します。<br><br>* `Origin`：ユーザーからのリクエストのOriginヘッダーの値を表します。<br><br>* `ClientIP`：ユーザーからのリクエストを送信したクライアントのIPアドレスを表します。<br><br>* `UA`：ユーザーからのリクエストのUser\-Agentヘッダーの値を表します。<br><br>* `ReqHeader`：ユーザーからのリクエストの特定のヘッダーの値を表します。関連する設定は`RequestHeader`で指定されます。<br><br>* `Cookie`：リクエストのクッキーを表します。関連する設定は`CookieToken`で指定されます。<br><br>* `FullURI`：クエリ文字列を含まない完全なリクエストパスを表します。関連する設定は`ParamSource`で指定されます。 | |
|CookieToken |String |`ParamType` が `Cookie` の場合、このパラメータは指定されたクッキーのキーを表します。CDNはそのクッキーの値を取得します。 | |
|RequestHeader |String |`ParamType` が `ReqHeader` の場合、このパラメータは指定されたリクエストヘッダーを表します。 | |
|SupContent |String |`ParamType` が `SupString` の場合、このパラメータは指定された文字列を表します。 | |
|UriParamSup |Object |リクエストパスから連続したセグメントを取得する方法を表します。<br><br>このパラメータは以下の設定を含む構造体です：<br><br><br>* リクエストパスを分割するために使用される区切り文字。<br><br>* 必要な連続パスセグメントの開始レベルと終了レベル。<br><br>* これらのパスセグメントを結合するために使用される結合文字。結合されたパスセグメントはトークンの計算に使用されます。 | |
|SplitSymbol |String |リクエストパスを分割するために使用する区切り文字を表します。 | |
|StartLevel |Long |開始セグメントが存在する階層を表します。 | |
|TermLevel |Long |終了セグメントが存在するレベルを表します。<br><br>`TermLevel` が負の整数の場合、右端のセグメントから左に数えることを示します。 | |
|JoinSymbol |String |これらのパスセグメントを結合するために使用する結合文字を表します。 | |
|UrlParam |Object |URLから必要なオブジェクトを取得する方法を表します。<br><br>このパラメータは、オブジェクトのソースと関連する設定を含む構造体です。 | |
|CapMode |String |オブジェクトのソースを表します。このパラメータは次の値を取ることができます：<br><br><br>* `name`：クエリパラメータを表します。関連する設定は`ParamName`および`ArgSegment`で指定されます。<br><br>* `uri`：リクエストパスで指定されたディレクトリを表します。関連する設定は`UriLevel`および`ArgSegment`で指定されます。 | |
|ParamName |String |`ParamType` が `name` の場合、このパラメータは指定されたクエリパラメータを表します。 | |
|UriLevel |Long |`ParamType` が `uri` の場合、このパラメータは指定されたディレクトリレベルを表します。<br><br>レベルが負の整数の場合、パスの右端のディレクトリから左に数えることを意味します。 | |
|ArgSegment |Object |`ParamName`または`UriLevel`に基づいて取得したコンテンツを分割して、特定のレベルのセグメントを抽出する必要があるかどうかを示します。このセグメントが取得すべきオブジェクトです。 | |
|Switch |Boolean |取得したコンテンツを分割する必要があるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。 | |
|Level |Long |取得したコンテンツを複数のレベルのセグメントに分割した後、必要なオブジェクトが存在するレベルを表します。<br><br>レベルが負の整数の場合、右端のレベルのセグメントから左に数えることを示します。 | |
|SplitSymbol |String |コンテンツを分割するために使用される区切り文字を表します。 | |
|CustomValue |String |ヘッダーモードとクッキーモードで使用 | |
|ParamSource |String |マニフェストに追加されたトークンについて、CDNがそのオブジェクトを使用してトークンを計算する際のオブジェクトのソースを示します。<br><br>このパラメータは次の値を取ります：<br><br><br>* `ParentLink`：オブジェクトがユーザーリクエストのURLから来ていることを示します。<br><br>* `ChildLink`：オブジェクトがマニフェストのビデオセグメントのURIから来ていることを示します。 | |
|RewriteM3U8 |Object |HLSマニフェスト書き換えの設定、つまりマニフェストのビデオセグメントURIにトークンを追加する方法を設定します。 | |
|Switch |Boolean |HLSマニフェストを書き換える必要があるかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：マニフェストの書き換えが必要であることを示します。<br><br>* `false`：マニフェストの書き換えが不要であることを示します。<br><br><br>デフォルトでは、CDNはマニフェストの`EXTINF`タグ下のビデオセグメントURIにのみトークンを追加します。 | |
|RewriteM3U8Tag |Object |追加のタグを表します。`Tags`に含まれるタグについては、CDNはこれらのタグ下のURLにトークンを追加します。[タイプF](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を参照してください。 | |
|Switch |Boolean |追加のタグを設定する必要があるかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：追加のタグを設定する必要があることを示します。<br><br>* `false`：追加のタグを設定する必要がないことを示します。 | |
|Tags |String[] |追加タグのリストを表します。 | |
|RewriteMPD |Object |DASHマニフェストの書き換え設定、つまりマニフェストのビデオセグメントURIにトークンを追加する方法を設定します。 | |
|Switch |Boolean |DASHマニフェストを書き換える必要があるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：マニフェストの書き換えが必要であることを示します。<br><br>* `false`：マニフェストの書き換えが不要であることを示します。 | |
|MpdVarExpand |Boolean |`SegmentTemplate`下のURIの変数を実際の値に置き換えるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：この設定を有効にすることを示します。この設定を有効にすると、CDNはまずビデオセグメントURIの変数を実際の値に置き換え、次に実際の値を含むURIに基づいてトークンを生成し、最後にトークンをURIに追加します。<br><br>* `false`：この設定を有効にしないことを示します。変数名自体が固定文字列としてトークン生成に使用されます。<br><br><br>この設定を有効にした後、現在、以下のすべての条件を満たす変数のみが実際の値に置き換えられます：<br><br><br>* 変数が`$RepresentationID$`である。<br><br>* `SegmentTemplate`下に少なくとも1つのURIが以下の条件を満たす：<br><br>   * そのURIで、少なくとも1つの`$RepresentationID$`の出現位置がURIパスの最後のセグメントではない。<br><br>* `<SegmentTemplate ... />`と`<Representation .../>`の間に他のコンテンツがあってはならない。<br><br><br>また、書き換え後のDASHマニフェストでは、元の`SegmentTemplate`は保持されます。<br><br>[タイプF](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を参照してください。 | |
|CustomRewrite |Object |ビデオマニフェストの拡張書き換え設定を表します。この設定を有効にすると、CDNは[タイプF](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を使用して[タイプF](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を上書きします。 | |
|Switch |Boolean |拡張書き換え設定を有効にするかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：拡張書き換え設定を有効にすることを示します。<br><br>* `false`：拡張書き換え設定を有効にしないことを示します。 | |
|RewriteParam |Object[] |オブジェクトのリストを表します。CDNはこれらのオブジェクトを連結してトークンを生成し、ビデオセグメントのURLに追加します。 | |
|ParamType |String |オブジェクトのタイプを表します。このパラメータは次の値を取ることができます：<br><br><br>* `ParentLinkUrlParam`：ユーザーリクエストURLの特定のオブジェクトを表します。オブジェクトはクエリパラメータまたは特定のレベルのパスディレクトリです。関連する設定は`ParentLinkUrlParam`構造体で指定されます。<br><br>* `SupString`：文字列を表します。関連する設定は`SupContent`で指定されます。<br><br>* `ParentLinkURI`：ユーザーリクエストパスの連続したセグメントを表します。パスにはクエリ文字列は含まれません。関連する設定は`ParentLinkUriParamSup`で指定されます。<br><br>* `ParentLinkExpire`：ユーザーリクエストのトークンのタイムスタンプを表します。`ExpireTimeRule`下の`Duration`パラメータの説明を参照してください。<br><br>* `AuthToken`：`AuthTokenCalRule`に基づいて計算されたトークンを表します。<br><br>* `ParentFullURI`：ユーザーリクエストの完全なパスを表し、クエリ文字列は含まれません。 | |
|SupContent |String |`ParamType` が `SupString` の場合、このパラメータは指定された文字列を表します。 | |
|ParentLinkUriParamSup |Object |ユーザーリクエストパスからオブジェクトを取得する方法を表します。<br><br>このパラメータは以下の設定を含む構造体です：<br><br><br>* リクエストパスを分割するために使用される区切り文字。<br><br>* 連続パスセグメントの開始レベルと終了レベル。<br><br>* これらのパスセグメントを結合するために使用される結合文字。結合されたパスセグメントはトークンを生成するために使用されます。 | |
|SplitSymbol |String |リクエストパスを分割するために使用する区切り文字を表し、`JoinSymbol`と同じであることが要求されます。 | |
|StartLevel |Long |開始セグメントが存在する階層を表します。 | |
|TermLevel |Long |終了セグメントが存在するレベルを表し、以下の要件があります：<br><br><br>* 0以外の整数のみ。<br><br>* 絶対値は総レベル数より大きくないこと。<br><br><br>`TermLevel` が負の整数の場合、右端のセグメントから左に数えることを示します。 | |
|JoinSymbol |String |これらのパスセグメントを結合するために使用する結合文字を表します。 | |
|ParentLinkUrlParam |Object |URLからオブジェクトを取得する方法を表します。<br><br>このパラメータは、オブジェクトのソースと関連する設定を含む構造体です。 | |
|CapMode |String |オブジェクトのソースを表します。このパラメータは次の値を取ることができます：<br><br><br>* `name`：クエリパラメータを表します。関連する設定は`ParamName`および`ArgSegment`で指定されます。<br><br>* `uri`：リクエストパスで指定されたディレクトリを表します。関連する設定は`UriLevel`および`ArgSegment`で指定されます。 | |
|ParamName |String |`CapMode` が `name` の場合、このパラメータは指定するクエリパラメータを表します。 | |
|UriLevel |Long |`CapMode` が `uri` の場合、このパラメータは指定されたディレクトリレベルを表します。<br><br>レベルが負の整数の場合、パスの右端のディレクトリから左に数えることを意味します。 | |
|ArgSegment |Object |`ParamName`または`UriLevel`に基づいて取得したコンテンツを分割して、特定のレベルのセグメントを抽出する必要があるかどうかを示します。このセグメントが取得すべきオブジェクトです。 | |
|Switch |Boolean |取得したコンテンツを分割する必要があるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。 | |
|Level |Long |取得したコンテンツを複数のレベルのセグメントに分割した後、必要なセグメントが存在するレベルを表します。<br><br>レベルが負の整数の場合、右端のセグメントから左に数えることを示します。 | |
|SplitSymbol |String |コンテンツを分割するために使用される区切り文字を表します。 | |
|CustomValue |String | | |
|RewriteRule |Object |CDNがビデオセグメントURIにトークンを追加する方法を表します。 | |
|CapMode |String |CDNが生成されたトークンをビデオセグメントURIにどのように追加するかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `name`：URIで指定されたクエリパラメータをトークンに設定することを示します。関連する設定は`ParamName`で指定されます。<br><br>* `uri`：URIで指定されたディレクトリレベルにディレクトリを挿入し、そのディレクトリをトークンに設定することを示します。関連する設定は`UriLevel`で指定されます。 | |
|ParamName |String |`CapMode`が`name`の場合、指定されたクエリパラメータを表します。 | |
|UriLevel |Long |`CapMode` が `uri` の場合、指定されたディレクトリレベルを表します。<br><br>レベルが負の整数の場合、右端のレベルのディレクトリから左に数えることを意味します。 | |
|SignJoinSymbol |String |`RewriteParam` 内の各オブジェクトを連結するために使用する連結記号を表します。 | |
|ArgumentRule |Object |オリジンパラメータ関連の設定を表します。 | |
|KeepOriginArg |Boolean |`AuthTokenCalRule`に基づいて計算されたトークンをオリジンリクエストに含めるかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：オリジンリクエストにトークンを含めることを示します。オリジンリクエストにおけるトークンの出現位置は`SignCapRule`の設定と同じです。<br><br>* `false`：オリジンリクエストにトークンを含めないことを示します。 | |
|GeneralParamRule |Object |CDNがビデオセグメントURIのクエリパラメータを設定する方法を表します。 | |
|ParentLinkParamInherit |String |書き換え後のビデオセグメントURIが、ユーザーリクエストURLのトークンとトークンタイムスタンプを表すパラメータ以外のすべてのクエリパラメータを含むかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `not_inherit`：書き換え後のセグメントURIがこれらのクエリパラメータを含まないことを示します。<br><br>* `inherit`：書き換え後のセグメントURIがこれらのクエリパラメータを含むことを示します。 | |
|SubLinkParamRule |Object |この構造体には、追加のクエリパラメータ設定が含まれています。この構造体には、追加のクエリパラメータ設定が含まれています。 | |
|InheritMode |String |ビデオセグメントURIとユーザーリクエストURLに同じクエリパラメータが存在する場合、CDNがビデオセグメントURIのそのパラメータの値をどのように設定するかを示します。<br><br>このパラメータは次の値を取ります：<br><br><br>* `sub_link_first`：ビデオセグメントURIのパラメータ値を使用することを示します。<br><br>* `inherit_first`：ユーザーリクエストURLのパラメータ値を使用することを示します。 | |
|KeepSubLinkArg |String |書き換え後のビデオセグメントURIがURIの元のクエリパラメータを保持するかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `delete`：書き換え後のセグメントURIがこれらのクエリパラメータを保持しないことを示します。<br><br>* `keep`：書き換え後のセグメントURIがこれらのクエリパラメータを保持することを示します。 | |
|RewriteFormat |String |書き換え後のビデオセグメントURIのフォーマットを表します。このパラメータは次の値を取ることができます：<br><br><br>* `default`：このパラメータ値の意味は`absolute`と同じです。<br><br>* `relative`：URIの現在のフォーマットを維持します。<br><br>* `absolute`：URIのフォーマットが相対パスの場合、CDNはフォーマットを絶対パスに変換します。URIが絶対パスまたは完全URLの場合は、現在のフォーマットを維持します。<br><br>* `full`：URIのフォーマットが絶対パスまたは相対パスの場合、CDNはフォーマットを完全URLに変換します。 | |
|Timeout |Object |「オリジンリクエストタイムアウト」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。この場合、TCPリクエストとHTTPリクエストのタイムアウト時間はデフォルト値である2秒と60秒が使用されます。 |`true` |
|TimeoutRules |Object[] |タイムアウト時間の設定一式を表します。 | |
|TimeoutAction |Object |タイムアウト時間の設定を表します。 | |
|HttpTimeout |Long |HTTPリクエストのタイムアウト時間を表します。 |`60` |
|TcpTimeout |Long |TCPリクエストのタイムアウト時間を表します。 |`2` |
|UaAccessRule |Object |「UAブロックリスト/アローリスト」機能の設定を表します。 | |
|AllowEmpty |Boolean |UAが空（""）であるか、UAフィールドを含まないリクエストがドメイン名にアクセスすることを許可するかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：許可することを示します。<br><br>* `false`：許可しないことを示します。 |`true` |
|IgnoreCase |Boolean |UA文字列が大文字と小文字を区別するかどうかを示します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：UA文字列が大文字と小文字を区別しないことを示します。<br><br>* `false`：UA文字列が大文字と小文字を区別することを示します。 |`true` |
|RuleType |String |UAリストのタイプを表します。`Switch` が `true` の場合、このパラメータは必須です。このパラメータは次の値を取ることができます：<br><br><br>* `allow`：アローリストを表します。<br><br>* `deny`：ブロックリストを表します。 |`deny` |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|UserAgent |String[] |UAのリストを表します。このパラメータの説明は以下の通りです：<br><br><br>* `RuleType`が`allow`の場合、リストに含まれるUAを持つリクエストのみがドメイン名にアクセスできることを示します。<br><br>* `RuleType`が`deny`の場合、アクセスリクエストがリストに含まれるUAを持つ場合、ドメイン名へのアクセスは許可されないことを示します。<br><br><br>UAの`*`は1つ以上の文字を表します。 |`["*curl*","*Mozilla*"]` |
|VideoDrag |Object |「ビデオシーク」機能の設定を表します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|OriginIPv6 |String |「IPv6オリジンフェッチ」の設定を表します。このパラメータは次の値を取ることができます：<br><br><br>* `ipv6_first`：CDNは常にオリジンサーバーのドメイン名のIPv6アドレスを取得しようとします。このIPアドレスを取得できない場合、CDNはオリジンサーバーのドメイン名のIPv4アドレスを取得しようとします。<br><br>* `ipv4_first`：CDNは常にオリジンサーバーのドメイン名のIPv4アドレスを取得しようとします。このIPアドレスを取得できない場合、CDNはオリジンサーバーのドメイン名のIPv6アドレスを取得しようとします。<br><br>* `followclient`：CDNはユーザーからのリクエストと同じタイプのIPアドレスを取得しようとします。<br><br><br>海外の一部のCDNリージョナルノードはIPv6アドレスへのオリジンリクエスト送信をサポートしていないため、この機能は中国本土に所在するリージョナルノードにのみ適用されます。 | |
|UrlNormalize |Object |「URL正規化」機能の設定を表します。 | |
|NormalizeObject |String[] |URL正規化オプションのリストを表します。`Switch` が `true` の場合、このパラメータは必須です。リストには以下のオプションを含めることができます：<br><br><br>* `dot_segments`：リクエストURLの以下の内容を置換することを示します：<br><br>   * `/./`：単一のスラッシュ（/）に置換。<br><br>   * `/../`：`/../` の前に別のレベルのディレクトリがある場合、`/../` とそのディレクトリを削除します。`/../` の前にディレクトリがない場合は、元のURLを保持します。<br><br>* `back_slashes`：リクエストURLのバックスラッシュ（\）を単一のスラッシュ（/）に置換することを示します。<br><br>* `successive_slashes`：リクエストURLの連続するスラッシュ（//）を単一のスラッシュ（/）に置換することを示します。 | |
|Switch |Boolean |この機能を有効にするかどうかを表します。このパラメータは次の値を取ることができます：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 | |
|RequestBlockRule |Object |「カスタムインターセプト」機能の設定を表します。 | |
|BlockRule |Object[] |ルールリストを表します。リストの最初のルールが最も優先順位が高いです。<br><br>ユーザーからのリクエストを受け取ったとき、CDNはルールの優先順位に従って、高いものから低いものへとルールとリクエストをマッチングさせます。ルールがリクエストにマッチした場合、CDNは残りのルールの処理を停止します。 | |
|BlockAction |Object |ルールにおけるCDNの動作設定を表します。 | |
|Action |String |Condition に一致するリクエストをCDNがどのように処理するかを示します。このパラメータは、次の値を取ります。<br><br><br>* `refuse`：CDNがリクエストを拒否し、4xxエラーコードを返すことを示します。エラーコードは `StatusCode` で指定されます。<br><br>* `redirect`：CDNがリクエストを `RedirectUrl` で指定されたURLにリダイレクトすることを示します。 | |
|StatusCode |String |Condition に一致するユーザーからのリクエストに対するCDNのレスポンスステータスコードを示します。<br><br><br>* `Action` が `refuse` の場合、このパラメータは400～499の範囲のエラーコードを示します。<br><br>* `Action` が `redirect` の場合、このパラメータは次の値を取ります。<br><br>   * `301`：レスポンスステータスコードが301であることを示します。<br><br>   * `302`：レスポンスステータスコードが302であることを示します。 | |
|ErrorPage |String |* `Action` が `refuse` の場合、このパラメータはオプションです。説明は次のとおりです。<br><br>   * このパラメータを指定すると、「ユニバーサルカタログ」機能のカスタムレスポンスページのページ名を表します。つまり、CDNがリクエストを拒否したときに、このカスタムページが返されます。<br><br>   * このパラメータが指定されていない場合は、CDNが `StatusCode` で指定されたエラーコードの標準レスポンスボディを使用することを示します。 | |
|RedirectUrl |String |* `Action` が `redirect` の場合、リダイレクト先のURLを示します。<br><br>* `Action` が `refuse` の場合、このパラメータは無効です。 | |
|Condition |Object |このルールで一致する条件の定義を示します。 | |
|ConditionRule |Object[] |リクエストURLのパスとクエリパラメータ、およびリクエスト元のクライアントIPアドレスに一致させるための一致条件のリストを示します。各一致条件には、一致タイプ、比較タイプ、および一致する値が含まれています。 | |
|Object |String |一致タイプを示します。<br><br><br>* `Type` が `url` の場合、このパラメータは次の値を取ります。<br><br>   * `path`：リクエストURLのパスを示します。<br><br>   * `directory`：パス内のディレクトリを示します。<br><br>   * `filetype`：パスの末尾にある拡張子を示します。<br><br>   * `regex`：正規表現に一致するリクエストURLのパスを示します。<br><br>* `Type` が `querystring` の場合、このパラメータは次の値を取ります。<br><br>   * `query_name`：リクエストURLのクエリパラメータを示します。<br><br>   * `full_querystring`：リクエストURLのクエリ文字列を示します。<br><br>* `Type` が `client_ip` の場合、このパラメータは次の値を取ります。<br><br>   * `client_ip`：クライアントのIPアドレスを示します。<br><br>* `Type` が `request_header` の場合、このパラメータは次の値を取ります。<br><br>   * `ua`：リクエストのUser\-Agentヘッダーを示します。<br><br>   * `customize`：リクエストのカスタムヘッダーを示します。 | |
|Operator |String |比較タイプを示します。<br><br><br>* `Object` が `path`、`directory`、`filetype` の場合、このパラメータは次の値を取ります。<br><br>   * `equal`：`Value` のいずれかの値に一致する場合、リクエストはこの一致条件を満たします。<br><br>   * `not_equal`：`Value` のすべての値に一致しない場合、リクエストはこの一致条件を満たします。<br><br>* `Object` が `query_name` の場合、このパラメータは次の値を取ります。<br><br>   * `exist`：存在することを示します。マッチングロジックは `equal` と同じです。<br><br>   * `not_exist`：存在しないことを示します。マッチングロジックは `not_equal` と同じです。<br><br>   * `belong_shared_config`：`Value` が示すユニバーサルカタログに含まれるいずれかの値に一致する場合、リクエストはこの一致条件を満たします。<br><br>   * `not_belong_shared_config`：`Value` が示すユニバーサルカタログに含まれるすべての値に一致しない場合、リクエストはこの一致条件を満たします。<br><br>   * `empty`：値が空であることを示します。<br><br>   * `not_empty`：値が空でないことを示します。<br><br>   * `equal`：上記の説明をご参照ください。<br><br>   * `not_equal`：上記の説明をご参照ください。<br><br>* `Object` が `regex`、`full_querystring`、`client_ip` または `ua` の場合、このパラメータは次の値を取ります。<br><br>   * `match`：`equal` の説明と同じです。<br><br>   * `not_match`：`not_equal` の説明と同じです。<br><br>* `Object` が `ua` または `customize` の場合、このパラメータには次の**追加**値があります。<br><br>   * `empty`：上記の説明をご参照ください。<br><br>   * `not_empty`：上記の説明をご参照ください。 | |
|Type |String |一致オブジェクトのタイプを示します。このパラメータは、次の値を取ります。<br><br><br>* `url`：リクエストURLを示します。<br><br>* `querystring`：リクエストURLのクエリ文字列を示します。<br><br>* `request_header`：リクエストのヘッダーを示します。 | |
|Value |String |1つ以上の一致する値を示します。<br><br><br>* `Type` が `request_header` の場合、複数の一致する値は縦線（\|）で区切られます。<br><br>* `Type` が `request_header` でない場合、複数の一致する値はセミコロン（;）で区切られます。 | |
|Name |String |`Object` が `query_name` または `customize` の場合、このパラメータは有効です。<br><br><br>* `Object` が `query_name` の場合、このパラメータはクエリパラメータの名前を示します。<br><br>* `Object` が `customize` の場合、このパラメータはカスタムリクエストヘッダーの名前を示します。 | |
|Connective |String |複数の `ConditionRule` 間の関係を示します。このパラメータは、次の値を取ります。<br><br><br>* `AND`：「And」を示します。<br><br>* `OR`：「Or」を示します。 | |
|RuleName |String |ルールの名前を示します。 | |
|Switch |Boolean |この機能を有効にするかどうかを示します。このパラメータは、次の値を取ります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 | |
|OriginCertCheck |Object |「オリジンサーバー証明書の検証」機能の設定を示します。<br><br>この機能を有効にすると、CDNはオリジンサーバー証明書の有効性を検証します。これには、証明書が失効していないか、証明書が信頼できるCAによって発行されているか、証明書がオリジンサーバーのドメイン名と一致しているかなどが含まれます。CDNには、一般的に信頼されているCAのルート証明書が組み込まれています。オリジンサーバー証明書の検証に失敗した場合、CDNは[オリジンフェッチの再試行](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-fetch-retry-jp) を実行します。オリジン再試行中にオリジンサーバー証明書の検証が依然として失敗した場合、CDNはこのオリジンサーバーからファイルを取得できないと判断し、ユーザーからのリクエストに対して504ステータスコードを返します。 | |
|Switch |Boolean |この機能を有効にするかどうかを示します。このパラメータは、次の値を取ります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 | |
|CertInfoList |Object[] |CA証明書のリストを示します。リスト内のCA証明書はCDNでホストされます。CDNは、このリストのCA証明書を使用して、オリジンサーバーからのサーバー証明書を検証します。 | |
|CertId |String |リスト内のCA証明書のIDを示します。`cert_hosting` で始まります。 | |
|ConditionalOrigin |Object |「条件付きオリジンサーバー」機能の設定を示します。 | |
|OriginRules |Object[] |ルールのリストを示します。リスト内の各ルールは、一連の一致条件と、一致条件を満たすリクエストに対してCDNが実行するアクションを定義します。<br><br>ユーザーからのリクエストを受信すると、CDNはルールの優先度順に、高いものから低いものへとリクエストを照合します。ルールがリクエストに一致した場合、CDNは残りのルールの処理を停止します。 | |
|Actions |Object |ルールで定義されたアクション設定を示します。 | |
|OriginLines |Object[] |オリジンサーバーのリストを示します。 | |
|Address |String |オリジンサーバーのアドレスを示します。<br><br><br>* `InstanceType` が `ip` の場合、`Address` はIPv4またはIPv6アドレスを示します。<br><br>* `InstanceType` が `domain` の場合、`Address` はドメイン名を示します。 | |
|HttpPort |String |CDNがHTTPプロトコルを使用してこのオリジンサーバーにアクセスするときに使用するポートを示します。 | |
|HttpsPort |String |CDNがHTTPSプロトコルを使用してこのオリジンサーバーにアクセスするときに使用するポートを示します。 | |
|InstanceType |String |オリジンサーバーのタイプを示します。このパラメータは、次の値を取ります。<br><br><br>* `ip`：IPアドレスを示します。<br><br>* `domain`：ドメイン名を示します。 | |
|OriginHost |String |オリジンサーバーに複数のサイトがある場合、このパラメータはオリジンリクエストがアクセスするサイトのドメイン名を示します。<br><br><br>* このパラメータは、グローバルな `OriginHost` パラメータよりも優先されます。<br><br>* このパラメータ値の長さは1,024文字を超えることはできません。 | |
|Condition |Object |このルールで一致する条件の設定を示します。 | |
|ConditionGroups |Object[] |一致条件のリストを示します。 | |
|Condition |Object |一致条件の設定を示します。 | |
|Object |String |一致オブジェクトを示します。このパラメータは、次の値を取ります。<br><br><br>* `path`：リクエストURLの完全なパスを示します。<br><br>* `directory`：リクエストURLの特定のディレクトリを示します。<br><br>* `filetype`：リクエストURLの拡張子を示します。<br><br>* `full_querystring`：リクエストURLのクエリ文字列を示します。<br><br>* `client_ip`：クライアントのIPアドレスまたはIPアドレスの場所を示します。 | |
|Operator |String |一致タイプを示します。`Object` によって、使用できる値は異なります。<br><br><br>* `Object` が `path`、`directory` または `filetype` の場合、このパラメータの値は `equal`、`not_equal` です。<br><br>* `Object` が `path` の場合、このパラメータには `regex_match`、`regex_not_match` という**追加**値もあります。<br><br>* `Object` が `full_querystring` の場合、このパラメータの値は `regex_match`、`regex_not_match` です。<br><br>* `Object` が `client_ip` の場合、このパラメータの値は `equal`、`not_equal`、`belong`、`not_belong` です。<br><br><br>上記の値のうち、`belong` と `not_belong` の説明は次のとおりです。<br><br><br>* `belong`：クライアントのIPアドレスの場所が `Value` で示される国と地域のリストにある場合、リクエストはこの一致条件を満たします。<br><br>* `not_belong`：クライアントのIPアドレスの場所が `Value` で示される国と地域のリストにない場合、リクエストはこの一致条件を満たします。 | |
|Value |String[] |1つ以上の一致する値を示します。複数の一致する値はセミコロン（;）で区切られます。<br><br>`Operator` が `belong` または `not_belong` の場合、一致する値は1つ以上の国または地域のコードです。[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) を呼び出すと、戻り結果の `Regions` 構造体内の `Code` パラメータから、CDNがサポートするすべての国または地域のコードを取得できます。このAPIを呼び出すときは、リクエストパラメータ `Area` を `Global` に指定する必要があります。 | |
|IsGroup |Boolean |このフィルタ条件自体が条件グループであるかどうかを示します。<br><br>条件グループはネストをサポートしていないため、このパラメータ値は `false` である必要があります。デフォルト値も `false` であり、このフィルタ条件は条件グループにできないことを示します。 | |
|Connective |String |これらの一致条件間の関係を示します。このパラメータは、次の値を取ります。<br><br><br>* `or`：「Or」の関係を示します。<br><br>* `and`：「And」の関係を示します。 | |
|Switch |Boolean |この機能を有効にするかどうかを示します。このパラメータは、次の値を取ります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 | |
|Websocket |Object |WebSocketの設定を示します。 | |
|Switch |Boolean |ユーザーからのリクエストに対してWebSocketサポートを有効にするかどうかを示します。このパラメータは、次の値を取ります。<br><br><br>* `true`：WebSocketを有効にすることを示します。この設定を有効にすると、CDNはクライアントからのWebSocketリクエストに応答できます。<br><br>* `false`：WebSocketを無効にすることを示します。 | |
|Timeout |Long |WebSocket接続のタイムアウト時間（秒単位）を示します。 | |
|MultiRange |Object |「マルチレンジ」機能の設定を示します。 | |
|Switch |Boolean |この機能を有効にするかどうかを示します。このパラメータは、次の値を取ります。<br><br><br>* `true`：この機能を有効にすることを示します。この機能を有効にすると、CDNは複数の範囲が指定されたRangeリクエストを許可します。<br><br>* `false`：この機能を有効にしないことを示します。複数の範囲が指定されたRangeリクエストを受信した場合、CDNはそのリクエストを拒否し、416レスポンスステータスコードを返します。 | |
|OfflineCache |Object |「古いコンテンツを配信」機能の設定を示します。 | |
|Object |String |この機能のトリガー条件を示します。このパラメータは、次の値を取ります。<br><br><br>* `request_error`：オリジンリクエストが異常であることを示します。オリジンリクエストで異常が発生した場合、CDNはオリジンサーバーからの応答を受信しません。<br><br>* `error_code`：オリジンサーバーのレスポンスステータスコードが5xxであることを示します。<br><br>* `request_error,error_code`：上記の両方の条件が含まれることを示します。 | |
|StatusCode |String |500～599の範囲にある1つ以上のレスポンスステータスコードを示します。複数のステータスコードはセミコロン（;）で区切られます。`5xx` は、数字5で始まる任意のステータスコードを示します。<br><br>`Object` が `error_code` または `request_error,error_code` の場合にのみ、このパラメータは有効です。 | |
|Switch |Boolean |この機能を有効にするかどうかを示します。このパラメータは、次の値を取ります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 | |
|Cname |String |CDNがこのドメイン名に割り当てたCNAMEを示します。 |`www.example.com.bpgslb.com` |
|CreateTime |Long |このドメイン名の作成時刻をUnixタイムスタンプ形式で示します。 |`1636612244` |
|Project |String |このドメイン名が属するプロジェクトを示します。 |`default` |
|Status |String |このドメイン名のステータスを示します。このパラメータは、次の値を取ります。<br><br><br>* `online`：ステータスが「実行中」であることを示します。<br><br>* `configuring`：ステータスが「設定中」であることを示します。<br><br>* `offline`：ステータスが「オフライン」であることを示します。 |`offline` |
|UpdateTime |Long |このドメイン名設定の最終更新時刻をUnixタイムスタンプ形式で示します。このドメイン名設定が作成後に更新されていない場合、このパラメータ値は `CreateTime` の値と同じです。 |`1639621409` |
|ResourceTags |Object[] |このドメイン名のタグを示します。 | |
|Key |String |タグのキーを示します。 | |
|Value |String |タグの値を表示します。 | |
|ProxyProtocol |Object |PROXYプロトコルの設定。 | |
|Switch |Boolean |ユーザーからのリクエストに対してPROXYプロトコルのサポートを有効にするかどうかを示します。このパラメータには以下の値があります。<br><br><br>* `true`: PROXYプロトコルを有効にします。この機能を有効にすると、CDNは受信したPROXYヘッダーを解析してユーザーの実際のIPアドレスを取得できます。<br><br>* `false`: PROXYプロトコルを無効にします。<br><br><br>このパラメータのデフォルト値は`false`です。 |`true` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021-03-01
{
    "Domain": "test111.example.com"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "202508160551554488555F346DC5A960D4",
        "Action": "DescribeCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainConfig": {
            "AreaAccessRule": {
                "Area": [
                    "CHN",
                    "HKG",
                    "MAC",
                    "TWN",
                    "CHE"
                ],
                "RuleType": "allow",
                "Switch": true
            },
            "BrowserCache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": true,
                        "Ttl": 216000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "no_cache",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": false,
                        "Ttl": 3000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "default",
                        "IgnoreCase": true,
                        "Ttl": 50
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "force_cache",
                        "IgnoreCase": false,
                        "Ttl": 80
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 40
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first_Replenish",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "CacheKey": [
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "exclude",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "includePart",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "excludePart",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "param3;param4"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cname": "test111.example.com.bplslb.com",
            "Compression": {
                "CompressionRules": [
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip",
                                "br"
                            ],
                            "MinFileSizeKB": 10240
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip"
                            ],
                            "MinFileSizeKB": 10000
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "br"
                            ],
                            "MinFileSizeKB": 12345
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        }
                    }
                ],
                "Switch": true
            },
            "ConditionalOrigin": {
                "OriginRules": [
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "test1.example.com",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "domain"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "directory",
                                        "Operator": "not_equal",
                                        "Value": [
                                            "/folder1/"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "not_equal",
                                        "Value": [
                                            "192.0.2.50"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "or",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "203.0.113.50",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": "myorigin3.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file1",
                                            "/docs/file2"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "full_querystring",
                                        "Operator": "regex_match",
                                        "Value": [
                                            ".*size=.*\\&.*"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "directory",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/foods/",
                                            "/dogs/ragdolls/"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "filetype",
                                        "Operator": "equal",
                                        "Value": [
                                            "jpg",
                                            "png"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "equal",
                                        "Value": [
                                            "198.51.100.0",
                                            "198.51.100.2"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "belong",
                                        "Value": [
                                            "HKG",
                                            "CHN",
                                            "AZE"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "or",
                            "IsGroup": true
                        }
                    }
                ],
                "Switch": true
            },
            "CreateTime": 1755314680,
            "CustomErrorPage": {
                "ErrorPageRule": [
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "301",
                            "RedirectUrl": "http://www.example.com/newpage1",
                            "StatusCode": "405"
                        }
                    },
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "307",
                            "RedirectUrl": "http://www.example.com/newpage2",
                            "StatusCode": "504"
                        }
                    }
                ],
                "Switch": true
            },
            "Domain": "test111.example.com",
            "DownloadSpeedLimit": {
                "DownloadSpeedLimitRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "unlimited",
                                    "Operator": "match",
                                    "Type": "url"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 100,
                            "SpeedLimitRateAfter": 50,
                            "SpeedLimitTime": {
                                "BeginTime": "01:00",
                                "DayWeek": "unlimited",
                                "EndTime": "02:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 200,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "monday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 300,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "tuesday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 400,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "wednesday",
                                "EndTime": "13:59"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 500,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "thursday",
                                "EndTime": "05:59"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "FollowRedirect": true,
            "HTTPS": {
                "CertInfo": {
                    "CertId": "cert-7fade0eb4f8d4aadbde5dd25f2ffdf35",
                    "CertName": "1000011991",
                    "EncryType": "inter_cert",
                    "ExpireTime": 1763086346,
                    "Source": "cert_center"
                },
                "DisableHttp": false,
                "ForcedRedirect": {
                    "EnableForcedRedirect": true,
                    "StatusCode": "303"
                },
                "HTTP2": true,
                "Hsts": {
                    "Subdomain": "include",
                    "Switch": true,
                    "Ttl": 50
                },
                "OCSP": true,
                "Switch": true,
                "TlsVersion": [
                    "tlsv1.1",
                    "tlsv1.2"
                ]
            },
            "HttpForcedRedirect": {
                "EnableForcedRedirect": false,
                "StatusCode": "301"
            },
            "IPv6": {
                "Switch": true
            },
            "IpAccessRule": {
                "Ip": [
                    "203.0.113.0/24",
                    "198.51.100.4"
                ],
                "RuleType": "allow",
                "Switch": true
            },
            "MethodDeniedRule": {
                "Methods": "POST,DELETE,CONNECT,OPTIONS",
                "Switch": true
            },
            "MultiRange": {
                "Switch": false
            },
            "NegativeCache": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "400",
                        "Ttl": 60
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": true,
                        "StatusCode": "401",
                        "Ttl": 59
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "402",
                        "Ttl": 70
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "404",
                        "Ttl": 60
                    }
                }
            ],
            "OfflineCache": {
                "Object": "request_error,error_code",
                "StatusCode": "504;505",
                "Switch": true
            },
            "Origin": [
                {
                    "OriginAction": {
                        "OriginLines": [
                            {
                                "Address": "203.0.113.8",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginHost": "myorigin.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginHost": "myorigin2.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "InstanceType": "tos",
                                "OriginHost": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "tos",
                                    "Switch": true
                                },
                                "Region": "ap-southeast-3",
                                "Weight": "1"
                            },
                            {
                                "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "oss",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxx"
                                    }
                                },
                                "Region": "oss-ap-southeast-1",
                                "Weight": "2"
                            },
                            {
                                "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.cos.ap-singapore.myqcloud.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "cos",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-singapore",
                                "Weight": "3"
                            },
                            {
                                "Address": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "InstanceType": "tos",
                                "OriginHost": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "aws_common",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-southeast-1",
                                "Weight": "5"
                            },
                            {
                                "Address": "myazstorage.blob.core.windows.net",
                                "BucketName": "myazstorage",
                                "InstanceType": "tos",
                                "OriginHost": "myazstorage.blob.core.windows.net",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "azure",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccountKey": "xxxxxxxxxxxxxxxx"
                                    }
                                },
                                "Weight": "1"
                            },
                            {
                                "Address": "203.0.113.9",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img2.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            }
                        ]
                    }
                }
            ],
            "OriginAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "Origins": [
                    "test.example.net",
                    "my.example.net"
                ],
                "RuleType": "deny",
                "Switch": true
            },
            "OriginArg": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "set",
                                "Object": "queryString",
                                "Subobject": "key3=val3;key4=val4"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "png;jpg"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "excludePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "includePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file3;/docs/file4"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "addPart",
                                "Object": "queryString",
                                "Subobject": "key1=val1;key2=val2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "exclude",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "include",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                }
            ],
            "OriginCertCheck": {
                "Switch": true
            },
            "OriginHost": "superhost.example.com",
            "OriginIPv6": "ipv6_first",
            "OriginProtocol": "https",
            "OriginRange": true,
            "OriginRewrite": {
                "Switch": false
            },
            "OriginSni": {
                "SniDomain": "superhost.example.com",
                "Switch": true
            },
            "PageOptimization": {
                "OptimizationType": [
                    "html",
                    "js",
                    "css"
                ],
                "Switch": true
            },
            "Project": "default",
            "Quic": {
                "Switch": true
            },
            "RedirectionRewrite": {
                "RedirectionRule": [
                    {
                        "RedirectionAction": {
                            "RedirectCode": "302",
                            "SourcePath": "^/a{1,2}(.*)g$",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food$1g",
                            "TargetProtocol": "https",
                            "TargetQueryComponents": {
                                "Action": "includePart",
                                "Value": "param1"
                            }
                        }
                    },
                    {
                        "RedirectionAction": {
                            "RedirectCode": "307",
                            "SourcePath": "aaa(.*)",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food/$1g",
                            "TargetProtocol": "followclient",
                            "TargetQueryComponents": {
                                "Action": "include",
                                "Value": "*"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RefererAccessRule": {
                "AllowEmpty": true,
                "Referers": [
                    "www.example.org",
                    "docs.example.com",
                    "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                ],
                "ReferersType": {
                    "CommonType": {
                        "IgnoreCase": true,
                        "IgnoreScheme": true,
                        "Referers": [
                            "www.example.org",
                            "docs.example.com"
                        ]
                    },
                    "RegularType": {
                        "Referers": [
                            "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                        ]
                    }
                },
                "RuleType": "allow",
                "Switch": true
            },
            "RemoteAuth": {
                "RemoteAuthRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "bmp;pdf"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RemoteAuthRuleAction": {
                            "AuthModeConfig": {
                                "BackupRemoteAddr": "https://myendpoint2.com",
                                "MasterRemoteAddr": "https://myendpoint1.com",
                                "PathType": "variable",
                                "PathValue": "/sign",
                                "RequestMethod": "post"
                            },
                            "AuthResponseConfig": {
                                "CacheAction": {
                                    "Action": "cache",
                                    "CacheKey": [
                                        "URI",
                                        "content_type"
                                    ],
                                    "IgnoreCase": false,
                                    "Ttl": 40
                                },
                                "ResponseAction": {
                                    "StatusCode": "403"
                                },
                                "StatusCodeAction": {
                                    "DefaultAction": "pass",
                                    "FailCode": "401",
                                    "SuccessCode": "200"
                                },
                                "TimeOutAction": {
                                    "Action": "pass",
                                    "Time": 200
                                }
                            },
                            "QueryStringRules": {
                                "QueryStringComponents": {
                                    "Action": "includePart",
                                    "Value": "size;color"
                                },
                                "QueryStringInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "param1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "param2",
                                        "Value": "content_type",
                                        "ValueType": "variable"
                                    }
                                ]
                            },
                            "RequestBodyRules": "default",
                            "RequestHeaderRules": {
                                "RequestHeaderComponents": {
                                    "Action": "includePart",
                                    "Value": "header1;header2"
                                },
                                "RequestHeaderInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "hd1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "hd2",
                                        "Value": "client_ip",
                                        "ValueType": "variable"
                                    }
                                ],
                                "RequestHost": "test.example.com"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RequestBlockRule": {
                "BlockRule": [
                    {
                        "BlockAction": {
                            "Action": "refuse",
                            "StatusCode": "404"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "filetype",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Name": "param1",
                                    "Object": "query_name",
                                    "Operator": "equal",
                                    "Type": "querystring",
                                    "Value": "val1"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RuleName": "myrule1"
                    },
                    {
                        "BlockAction": {
                            "Action": "redirect",
                            "RedirectUrl": "https://www.example.com/helloworld",
                            "StatusCode": "301"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "full_querystring",
                                    "Operator": "not_match",
                                    "Type": "querystring",
                                    "Value": ".*size=.*\\&.*"
                                },
                                {
                                    "Object": "client_ip",
                                    "Operator": "match",
                                    "Type": "client_ip",
                                    "Value": "203.0.113.2;203.0.113.5"
                                },
                                {
                                    "Object": "ua",
                                    "Operator": "not_empty",
                                    "Type": "request_header"
                                },
                                {
                                    "Name": "myheader",
                                    "Object": "customize",
                                    "Operator": "match",
                                    "Type": "request_header",
                                    "Value": "value1"
                                }
                            ],
                            "Connective": "AND"
                        },
                        "RuleName": "myrule2"
                    }
                ],
                "Switch": true
            },
            "RequestHeader": [
                {
                    "RequestHeaderAction": {
                        "RequestHeaderInstances": [
                            {
                                "Action": "set",
                                "Key": "header1",
                                "Value": "val1",
                                "ValueType": "constant"
                            },
                            {
                                "Action": "set",
                                "Key": "header2",
                                "Value": "uri",
                                "ValueType": "variable"
                            },
                            {
                                "Action": "set",
                                "Key": "header3",
                                "Value": "myval${http_host}is${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "Action": "delete",
                                "Key": "header4"
                            }
                        ]
                    }
                }
            ],
            "ResourceTags": [
                {
                    "Key": "key1",
                    "Value": "value1"
                },
                {
                    "Key": "key2",
                    "Value": "value2"
                }
            ],
            "ResponseHeader": [
                {
                    "ResponseHeaderAction": {
                        "ResponseHeaderInstances": [
                            {
                                "AccessOriginControl": true,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Origin",
                                "Value": "myval",
                                "ValueType": "constant"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Headers",
                                "Value": "raw_uri",
                                "ValueType": "variable"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Expose-Headers",
                                "Value": "my${host}data${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "delete",
                                "Key": "Access-Control-Max-Age"
                            }
                        ]
                    }
                }
            ],
            "RuleEngine": {
                "Rules": [],
                "Switch": false
            },
            "ServiceRegion": "outside_chinese_mainland",
            "ServiceType": "web",
            "SignedUrlAuth": {
                "AuthRulesF": [
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "inherit_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": true
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "md5_bin",
                                "base64url",
                                "sha256",
                                "md5",
                                "base64_encode"
                            ],
                            "SignJoinSymbol": "abc",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "fixstring"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "URI",
                                    "UriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 3,
                                        "TermLevel": 5
                                    }
                                },
                                {
                                    "ParamSource": "ParentLink",
                                    "ParamType": "URLParam",
                                    "UrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "uri",
                                        "UriLevel": 3
                                    }
                                },
                                {
                                    "ParamType": "ClientDomain"
                                },
                                {
                                    "ParamType": "Referer"
                                },
                                {
                                    "ParamType": "Origin"
                                },
                                {
                                    "ParamType": "ClientIP"
                                },
                                {
                                    "ParamType": "UA"
                                },
                                {
                                    "ParamType": "ReqHeader",
                                    "RequestHeader": "myheader1"
                                },
                                {
                                    "CookieToken": "mycookie1",
                                    "ParamType": "Cookie"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "FullURI"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "not_match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "CustomRewrite": {
                            "RewriteParam": [
                                {
                                    "ParamType": "ParentLinkUrlParam",
                                    "ParentLinkUrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "name",
                                        "ParamName": "param23"
                                    }
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "string2"
                                },
                                {
                                    "ParamType": "ParentLinkURI",
                                    "ParentLinkUriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 4,
                                        "TermLevel": 6
                                    }
                                },
                                {
                                    "ParamType": "ParentLinkExpire"
                                },
                                {
                                    "ParamType": "AuthToken"
                                },
                                {
                                    "ParamType": "ParentFullURI"
                                }
                            ],
                            "RewriteRule": {
                                "CapMode": "name",
                                "ParamName": "myparam1"
                            },
                            "SignJoinSymbol": "/",
                            "Switch": true
                        },
                        "ExpireTimeRule": {
                            "Duration": 30,
                            "ExpTimeCapRule": {
                                "ArgSegment": {
                                    "Level": 0,
                                    "Switch": false
                                },
                                "CapMode": "name",
                                "ParamName": "param1"
                            },
                            "TimeFormat": "heximal"
                        },
                        "RewriteFormat": "default",
                        "RewriteM3U8": {
                            "RewriteM3U8Tag": {
                                "Switch": true,
                                "Tags": [
                                    "tag1",
                                    "tag2"
                                ]
                            },
                            "Switch": true
                        },
                        "RewriteMPD": {
                            "MpdVarExpand": true,
                            "Switch": true
                        },
                        "RuleName": "Authentication rule A",
                        "SecretKey": {
                            "BackupSecretKey": "secondarykey",
                            "MasterSecretKey": "primarykey"
                        },
                        "SignCapRule": {
                            "ArgSegment": {
                                "Level": 2,
                                "SplitSymbol": "-",
                                "Switch": true
                            },
                            "CapMode": "uri",
                            "UriLevel": 2
                        }
                    },
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "not_inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "sub_link_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": false
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "base64url"
                            ],
                            "SignJoinSymbol": "45yu",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "ExpireTimeRule": {
                            "Duration": 67,
                            "ExpTimeCapRule": {
                                "CapMode": "cookie",
                                "CustomValue": "mycookie56"
                            },
                            "TimeFormat": "octal"
                        },
                        "RewriteFormat": "default",
                        "RuleName": "Authentication rule B",
                        "SecretKey": {
                            "BackupSecretKey": "sk",
                            "MasterSecretKey": "pk"
                        },
                        "SignCapRule": {
                            "CapMode": "header",
                            "CustomValue": "myheader56"
                        }
                    }
                ],
                "Switch": true
            },
            "Status": "online",
            "Timeout": {
                "Switch": true,
                "TimeoutRules": [
                    {
                        "TimeoutAction": {
                            "HttpTimeout": 10,
                            "TcpTimeout": 5
                        }
                    }
                ]
            },
            "UaAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "RuleType": "deny",
                "Switch": true,
                "UserAgent": [
                    "*curl*",
                    "*firefox*"
                ]
            },
            "UpdateTime": 1755323476,
            "UrlNormalize": {
                "NormalizeObject": [
                    "back_slashes",
                    "successive_slashes",
                    "dot_segments"
                ],
                "Switch": true
            },
            "VideoDrag": {
                "Switch": true
            },
            "Websocket": {
                "Switch": true,
                "Timeout": 60
            }
        }
    }
}
```


&nbsp;
