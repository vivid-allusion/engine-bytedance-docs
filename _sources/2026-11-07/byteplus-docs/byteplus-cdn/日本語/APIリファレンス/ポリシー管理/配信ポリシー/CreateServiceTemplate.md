---
title: "CreateServiceTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CreateServiceTemplate_jp"
---

配信ポリシーを作成します。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=CreateServiceTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このAPIを呼び出す際、Bodyリストのパラメータに加えて、他の設定モジュールのパラメータを指定することもできます。他のモジュールのパラメータの説明については、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateServiceTemplate_jp">UpdateServiceTemplate</a>を参照してください。</div>


<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はCreateServiceTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター

<span id="一般設定"></span>
## 一般設定

<span id="ポリシー名"></span>
### ポリシー名


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Title |String |はい |作成する配信ポリシーの名前を示し、長さは100文字を超えることはできません。 |`TestPolicy` |


<span id="ポリシー説明"></span>
### ポリシー説明


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Message |String |いいえ |この配信ポリシーの説明を示し、長さは120文字を超えることはできません。 |`This is a test` |


<span id="プロジェクト"></span>
### プロジェクト


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Project |String |いいえ |この配信ポリシーが属するプロジェクトを示します。このパラメータのデフォルト値は `default` で、Defaultプロジェクトを示します。 |`default` |


<span id="オリジンサーバーの設定"></span>
### オリジンサーバーの設定


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Origin |Object[] |はい |オリジンサーバー設定を示します。 | |
|OriginAction |Object |はい |すべてのユーザーリクエストに適用されるオリジンサーバー設定を示します。 | |
|OriginLines |Object[] |はい |オリジンサーバーのリストを示します。リストには最大50のオリジンサーバーを含めることができます。 | |
|Address |String |はい |リスト内のオリジンサーバーのアドレスを示します。このパラメータには次の説明があります：<br><br><br>* `InstanceType` が `ip` の場合、オリジンサーバーのIPアドレスを指定します。IPアドレスはIPv4またはIPv6アドレスにすることができます。<br><br>* `InstanceType` が `domain` の場合、オリジンサーバーのドメイン名を指定します。このドメイン名はワイルドカードドメイン名であってはならず、このポリシーがバインドされるドメイン名と同じであってはなりません。<br><br>* `InstanceType` が `tos` の場合、クラウドプロバイダーがストレージバケットに割り当てたドメイン名を指定します。ドメイン名に `https://` は含まれず、長さは100文字を超えることはできません。ストレージバケットは、BytePlus TOS、Alibaba Cloud OSS、Tencent Cloud COS、Azure Blob Storage、AWS S3、またはAWS S3認証と互換性のあるサードパーティのオブジェクトストレージサービスから取得できます。<br><br><br>说明<br><br><br>* ストレージバケットがアカウントのTOSサービスからのものである場合、このAPIを呼び出す前に、CDNコンソールでドメイン名の設定ページを開く必要があります。そのページで、**承認** をクリックして、CDNがBytePlusアカウントのストレージバケットにアクセスすることを承認します。<br><br>* Azure Blob Storageでは、オブジェクトストレージバケットはコンテナーと呼ばれます。 |`www.example.com` |
|InstanceType |String |はい |オリジンサーバーのタイプを示します。このパラメータには次の値があります：<br><br><br>* `ip`：IPアドレスを示します。<br><br>* `domain`：ドメイン名を示します。<br><br>* `tos`：オブジェクトストレージバケットを示します。<br><br><br>注意<br><br>CDNがオブジェクトストレージオリジンサーバーにオリジンリクエストを送信する場合、オリジンリクエストで使用されるメソッドはユーザーリクエストと同じです。デフォルトでは、ユーザーリクエストで使用できるリクエストメソッドは、DELETE、GET、HEAD、POST、PUT、PATCH、OPTIONS、CONNECTです。オリジンリクエストで特定のメソッドを使用したくない場合（たとえば、DELETEメソッドを使用してオリジンサーバー上のファイルを誤って削除したくない場合）、次の手順を実行することをお勧めします：<br><br><br>1. ストレージバケットが配置されているオブジェクトストレージサービスで権限を設定して、予期しない操作を防ぎます。<br><br>2. CDNの `MethodDeniedRule` 機能で、CDNがサポートしていないリクエストメソッドを指定します。 |`ip` |
|OriginType |String |はい |このオリジンサーバーのカテゴリを示します。このパラメータには次の値があります：<br><br><br>* `primary`：プライマリオリジンサーバーを示します。<br><br>* `backup`：バックアップオリジンサーバーを示します。<br><br><br>オリジンサーバーリストには、少なくとも1つのプライマリオリジンサーバーが含まれている必要があります。バックアップオリジンサーバーはオプションです。 |`primary` |
|HttpPort |String |いいえ |CDNがHTTPプロトコルを使用してこのオリジンサーバーにアクセスするときにアクセスするポートを示します。値の範囲は1〜65535で、デフォルト値は `80` です。オリジンサーバーがこのポートを開いていない場合は、このパラメータを指定する必要はありません。<br><br>このパラメータは、`InstanceType` が `ip` または `domain` の場合にのみ有効です。 |`80` |
|HttpsPort |String |いいえ |CDNがHTTPSプロトコルを使用してこのオリジンサーバーにアクセスするときにアクセスするポートを示します。値の範囲は1〜65535で、デフォルト値は `443` です。オリジンサーバーがこのポートを開いていない場合は、このパラメータを指定する必要はありません。<br><br>このパラメータは、`InstanceType` が `ip` または `domain` の場合にのみ有効です。 |`443` |
|OriginHost |String |いいえ |このパラメータの説明は次のとおりです：<br><br><br>* `InstanceType` が `ip` または `domain` の場合、このパラメータはオリジンリクエストがアクセスするサイトドメイン名を示し、オリジンサーバーに複数のサイトがある場合に適用されます。このパラメータのデフォルト値は、グローバルな `OriginHost` と同じです。<br><br>* `InstanceType` が `tos` の場合、このパラメータは主に、クラウドプロバイダーでストレージバケットに追加したカスタムドメイン名を指定するために使用されます。このパラメータのデフォルト値は `Address` と同じです。<br><br><br>さらに、<br><br><br>* このパラメータの優先度は、グローバルな `OriginHost` パラメータよりも高くなります。<br><br>* このパラメータ値の長さは1,024文字を超えることはできません。<br><br>* `Address` が変更されておらず、`OriginHost` を指定していない場合、`OriginHost` はデフォルト値で上書きされず、現在の値のままになります。 |`img.example.com` |
|PrivateBucketAccess |Boolean |いいえ |ストレージバケットがプライベートバケットであるかどうかを示します。このパラメータは、`InstanceType` が `tos` の場合にのみ有効です。このパラメータには次の値があります：<br><br><br>* `true`：ストレージバケットがプライベートバケットであることを示します。<br><br>* `false`：ストレージバケットがプライベートバケットではないことを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`false` |
|PrivateBucketAuth |Object |いいえ |ストレージバケットにアクセスするための認証情報を示します。ストレージバケットがBytePlusアカウントに属している場合は、このパラメータを指定する必要はありません。CDNは、認証情報なしでアカウントのTOSストレージバケットにアクセスできます。ストレージバケットがプライベートであっても同様です。 | |
|Switch |Boolean |はい |ストレージバケットへのアクセスに認証情報が必要かどうかを示します。`PrivateBucketAuth` 構造体を指定した場合、このパラメータ値は `true` である必要があります。 |`false` |
|AuthType |String |いいえ |オブジェクトストレージバケットが配置されているサードパーティのクラウドプロバイダーを示します。このパラメータには次の値があります：<br><br><br>* `tos`：BytePlusを示します。<br><br>* `cos`：Tencent Cloudを示します。<br><br>* `oss`：Alibaba Cloudを示します。<br><br>* `azure`：Microsoft Azureを示します。<br><br>* `aws`：Amazon AWSおよびAWS S3と同じ認証方法を提供するサードパーティのオブジェクトストレージサービスプロバイダーを示します。<br><br><br>说明<br><br><br>* ストレージバケットのクラウドプロバイダーが `AuthType` パラメータの説明に記載されていない場合、またはストレージが別のBytePlusプライマリアカウントのTOSサービスからのものである場合は、AWS S3ストレージバケットを設定するのと同じ方法でストレージバケットをオリジンサーバーとして設定し、`TosAuthInformation` を設定します。<br><br>* TOSコンソールは、ストレージバケットのS3アクセスポイントとストレージバケットのリージョンコードを提供します。 |`cos` |
|TosAuthInformation |Object |いいえ |ストレージバケットのアクセス認証情報を示します。次のいずれかの条件が満たされる場合、このパラメータを指定する必要があります。<br><br><br>* `AuthType` が `tos` ではありません。<br><br>* `AuthType` が `tos` であり、同時にストレージバケットが別のBytePlusプライマリアカウントのTOSサービスに属している。 | |
|AccessKeyId |String |いいえ |アクセス認証情報のアクセスキーIDを示します。<br><br>说明<br><br><br>* `AuthType` が `cos` の場合、このパラメータに Tencent Cloud アカウントの SecretId を指定します。<br><br>* `AuthType` が `azure` の場合、このパラメータを指定する必要はありません。代わりに `AccountKey` パラメータを指定します。 |`xxxxxxxx` |
|AccessKeySecret |String |いいえ |アクセス認証情報のアクセスキーシークレットを示します。<br><br>说明<br><br><br>* `AuthType` が `cos` の場合、このパラメータに Tencent Cloud アカウントの SecretKey を指定します。<br><br>* `AuthType` が `azure` の場合、このパラメータを指定する必要はありません。代わりに `AccountKey` パラメータを指定します。 |`xxxxxx` |
|AccountKey |String |いいえ |Azureストレージアカウントの共有キーを示します。このパラメータは、`AuthType` が `azure` の場合にのみ有効です。 |`xxxxxx` |
|Region |String |いいえ |ストレージバケットが配置されているリージョン情報、つまりストレージバケットのリージョンコードを示します。リージョンコードは署名の計算に関与します。<br><br>`AuthType` が `aws` で `PrivateBucketAccess` が `true` の場合は、このパラメータを指定する必要があります。 |`us-east-1` |
|Weight |String |いいえ |このオリジンサーバーの重みを示します。値の範囲は1〜100で、デフォルト値は `1` です。重みが大きいほど、CDNがオリジンリクエストを送信するときにこのオリジンサーバーが選択される確率が高くなります。<br><br>このパラメータは、`InstanceType` が `ip` または `domain` の場合にのみ有効です。 |`100` |
|BucketName |String |いいえ |Azureストレージアカウントの名前を示します。このパラメータは、`AuthType` が `azure` の場合にのみ有効です。 |`mystorageaccount` |


<span id="条件付きオリジンサーバー"></span>
### 条件付きオリジンサーバー


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ConditionalOrigin |Object |いいえ |"条件付きオリジンサーバー" 機能の設定を示します。 | |
|OriginRules |Object[] |いいえ |ルールリストを示します。リスト内の各ルールは、一致条件のセットと、CDNが一致条件を満たすリクエストに対して実行する操作を定義します。<br><br>リストには最大20個のルールを含めることができます。<br><br>ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。 | |
|Actions |Object |いいえ |1つのルールで定義された操作設定を示します。 | |
|OriginLines |Object[] |いいえ |オリジンサーバーのリストを示します。現在、リストには1つのオリジンサーバーしか含めることができません。 | |
|Address |String |いいえ |オリジンサーバーのアドレスを示します。<br><br><br>* `InstanceType` が `ip` の場合、`Address` はIPv4またはIPv6アドレスを示します。<br><br>* `InstanceType` が `domain` の場合、`Address` はドメイン名を示します。このドメイン名はワイルドカードドメイン名にすることはできません。 |`203.0.113.8` |
|HttpPort |String |いいえ |CDNがHTTPプロトコルを使用してこのオリジンサーバーにアクセスするときに使用するポートを示します。値の範囲は1〜65535で、デフォルト値は `80` です。オリジンサーバーがこのポートを開いていない場合は、このパラメータを指定する必要はありません。 |`80` |
|HttpsPort |String |いいえ |CDNがHTTPSプロトコルを使用してこのオリジンサーバーにアクセスするときに使用するポートを示します。値の範囲は1〜65535で、デフォルト値は `443` です。オリジンサーバーがこのポートを開いていない場合は、このパラメータを指定する必要はありません。 |`443` |
|InstanceType |String |いいえ |オリジンサーバーのタイプを示します。このパラメータには次の値があります。<br><br><br>* `ip`：IPアドレスを示します。<br><br>* `domain`：ドメイン名を示します。<br><br><br>`OriginLines` を指定した場合、`InstanceType` は必須です。 |`ip` |
|OriginHost |String |いいえ |オリジンサーバーに複数のサイトがある場合、このパラメータはオリジンリクエストがアクセスするサイトのドメイン名を示します。<br><br><br>* このパラメータの優先度は、グローバルな `OriginHost` パラメータよりも高くなります。<br><br>* このパラメータ値の長さは1,024文字を超えることはできません。<br><br><br>このパラメータのデフォルト値は、グローバルな `OriginHost` と同じです。 |`img.example.com` |
|BucketSource |String |いいえ |bucket类型, tos,cos, oss, aws, aws_common | |
|PrivateBucketAccess |Boolean |いいえ |源站为tos时，是否开启私有桶访问 | |
|TosAuthInformation |Object |いいえ |鉴权配置 | |
|AccessKeyId |String |いいえ |AK | |
|AccessKeySecret |String |いいえ |SK | |
|Region |String |いいえ |bucket区域，当前仅在aws_common下生效。 | |
|AccountName |String |いいえ |账户名，azure专用 | |
|OriginType |String |いいえ |源站类型，主源还是备源 | |
|Weight |String |いいえ |权重，【1\-100校验】 | |
|Condition |Object |いいえ |このルールの一致条件の設定を示します。 | |
|ConditionGroups |Object[] |いいえ |一致条件のリストを示します。リストには最大50個の一致条件を含めることができます。 | |
|Condition |Object |いいえ |1つの一致条件の設定を示します。 | |
|Object |String |いいえ |一致オブジェクトを示します。このパラメータには次の値があります。<br><br><br>* `path`：リクエストURLの完全なパスを示します。<br><br>* `directory`：リクエストURLのディレクトリを示します。<br><br>* `filetype`：リクエストURLの拡張子を示します。<br><br>* `full_querystring`：リクエストURLのクエリ文字列を示します。<br><br>* `client_ip`：クライアントのIPアドレスまたはIPアドレスの場所を示します。 |`path` |
|Operator |String |いいえ |一致タイプを示します。`Object` によって値が異なります。<br><br><br>* `Object` が `path`、`directory`、または `filetype` の場合、このパラメータの値は `equal`、`not_equal` です。<br><br>* `Object` が `path` の場合、このパラメータには**追加**の値 `regex_match`、`regex_not_match` があります。<br><br>* `Object` が `full_querystring` の場合、このパラメータの値は `regex_match`、`regex_not_match` です。<br><br>* `Object` が `client_ip` の場合、このパラメータの値は `equal`、`not_equal`、`belong`、`not_belong` です。<br><br><br>上記の値のうち、`belong` と `not_belong` の説明は次のとおりです。<br><br><br>* `belong`：クライアントIPアドレスの場所が `Value` で示される国と地域のリストにある場合、このリクエストはこの一致条件を満たすことを示します。<br><br>* `not_belong`：クライアントIPアドレスの場所が `Value` で示される国と地域のリストにない場合、このリクエストはこの一致条件を満たすことを示します。 |`equal` |
|Value |String[] |いいえ |1つまたは複数のマッチ値を表します。マッチ値はセミコロン（;）で区切られます。このパラメータの入力要件は次のとおりです。<br><br><br>* `Object` が `path`、`directory`、または `filetype` の場合、すべてのマッチ値の合計長は 1,024 文字を超えることはできず、次の文字を含めることはできません。<br><br>   * ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br>* `Object` が `path` の場合、このパラメータには次の**追加**要件があります。<br><br>   * 各マッチ値はスラッシュ（/）で始まる必要がありますが、/で終わることはできません。マッチ値には 1 つ以上の星印（\*）を使用でき、各星印は 1 つ以上の文字を表します。例：`/www/img/my*image.png`。<br><br>* `Object` が `directory` の場合、このパラメータには次の**追加**要件があります。<br><br>   * 各マッチ値はスラッシュ（/）で始まり、スラッシュ（/）で終わる必要があります。例：`/www/img/`。<br><br>* `Object` が `filetype` の場合、このパラメータには次の**追加**要件があります。<br><br>   * 各マッチ値はピリオド（.）で始めることはできません。例：`png;txt`。<br><br>* `Object` が `full_querystring` の場合、このパラメータの入力要件は次のとおりです。<br><br>   * すべてのマッチ値の合計長は 256 文字を超えることはできません。<br><br>   * マッチ値には、数字、文字、パーセント記号（%）、アンダースコア（_）、ハイフン（\-）を含めることができます。<br><br>* `Object` が `client_ip` の場合、<br><br>   * `Operator` が `equal` または `not_equal` の場合、このパラメータの入力要件は次のとおりです。<br><br>      * IP アドレスの数は 5 を超えることはできません。<br><br>      * IP アドレスは IPv4 アドレスである必要があります。<br><br>   * `Operator` が `belong` または `not_belong` の場合、マッチ値は 1 つ以上の国または地域のコードです。[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp) を呼び出して、返された結果の `Regions` 構造体の `Code` パラメータから CDN がサポートするすべての国または地域のコードを取得できます。この API を呼び出すときは、リクエストパラメータ `Area` を `Global` に指定する必要があります。 |`/www/img/my*image.png;/doc` |
|Name |String |いいえ |当匹配对象为query_string时具体的参数名; 当匹配对象为request_header时具体的头部名 | |
|Type |String |いいえ |匹配对象类型, enums: query_string, request_header | |
|Connective |String |いいえ |これらのマッチ条件間の関係を示します。このパラメータには次の値があります。<br><br><br>* `or`：関係が「または」であることを示します。<br><br>* `and`：関係が「かつ」であることを示します。<br><br><br>このパラメータのデフォルト値は `or` です。 |`and` |
|IsGroup |Boolean |いいえ |このパラメータ値は `true` である必要があります。 |`true` |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |


<span id="オリジンリクエストのプロトコル"></span>
### オリジンリクエストのプロトコル


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginProtocol |String |はい |オリジンリクエストで使用されるプロトコルを示します。このパラメータには次の値があります。<br><br><br>* `http`：オリジンリクエストがHTTPプロトコルを使用することを示します。<br><br>* `https`：オリジンリクエストがHTTPSプロトコルを使用することを示します。<br><br>* `followclient`：オリジンプロトコルがユーザーからのリクエストで使用されるプロトコルと同じであることを示します。 |`http` |


<span id="オリジンサーバーの証明書検定"></span>
### オリジンサーバーの証明書検定


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginCertCheck |Object |いいえ |"オリジンサーバー証明書検証" 機能の設定を示します。この機能を使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。<br><br>この機能が有効になると、CDNはオリジンサーバー証明書の有効性を検証します。これには、証明書が失効しているかどうか、証明書が信頼できるCAによって発行されているかどうか、証明書がオリジンサーバーのドメイン名と一致しているかどうかなどが含まれます。CDNには、一般的な信頼できるCAのルート証明書が組み込まれています。オリジンサーバー証明書が検証に失敗した場合、CDNは [オリジンフェッチの再試行](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-fetch-retry-jp) を実行します。オリジンリトライ中にオリジンサーバー証明書がまだ検証に失敗した場合、CDNはこのオリジンサーバーからファイルを取得できないと判断し、ユーザーからのリクエストに504ステータスコードで応答します。 | |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|CertInfoList |Object[] |いいえ |CA証明書のリストを示します。リスト内のCA証明書はCDNでホストされており、すべて国際証明書である必要があります。CDNはこのリスト内のCA証明書を使用して、オリジンサーバーからのサーバー証明書を検証します。<br><br>現在、このリストには1つのCA証明書しか含めることができません。 | |
|CertId |String |いいえ |リスト内のCA証明書のIDを示します。`cert_hosting` で始まります。<br><br>[ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/ListCertInfo_jp) を呼び出して、CDNでホストされているCA証明書のリストを照会し、指定する証明書のIDを取得できます。 |`cert_hosting-104663` |
|ClientCertInfoList |Object[] |いいえ |双向认证时的客户端证书 | |
|CertId |String |いいえ |证书ID | |
|CertName |String |いいえ |证书名 | |
|Certificate |Object |いいえ |证书信息 | |
|Certificate |String |いいえ |证书内容 | |
|EncryptionCert |String |いいえ |加密公私钥 | |
|EncryptionKey |String |いいえ |无 | |
|PrivateKey |String |いいえ |密钥 | |
|Desc |String |いいえ |证书描述信息 | |
|EffectiveTime |Long |いいえ |证书生效起始时间 | |
|EncryType |String |いいえ |证书类型 国际/国密 | |
|ExpireTime |Long |いいえ |证书过期时间 | |
|Source |String |いいえ |证书来源 | |
|Type |String |いいえ |类型，单向还是双向认证。不填表示单向 | |


<span id="ipv6オリジンフェッチ"></span>
### IPv6オリジンフェッチ


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|


<span id="オリジンリクエストのホスト名"></span>
### オリジンリクエストのホスト名


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginHost |String |いいえ |オリジンサーバーに複数のサイトがある場合、このパラメータはオリジンリクエストがアクセスするサイトのドメイン名を示します。このパラメータはすべてのオリジンサーバー設定に有効ですが、優先度はオリジンサーバー設定の `OriginHost` パラメータよりも低くなります。<br><br>このパラメータのデフォルト値は `Domain` と同じです。<br><br>オリジンサーバーがオブジェクトストレージバケットの場合は、このパラメータを指定する必要はありません。そのデフォルト値は、オリジンサーバー設定の `Address` と同じです。 |`img.example.com` |


<span id="アクセス制限"></span>
## アクセス制限

<span id="ipv6"></span>
### IPv6


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|IPv6 |Object |いいえ |IPv6 機能の設定を表します。 | |
|Switch |Boolean |はい |ユーザーからのリクエストに対してIPv6サポートを有効にするかどうかを示します。このパラメータには次の値があります。<br><br><br>* `true`：IPv6を有効にすることを示します。<br><br>* `false`：IPv6を無効にすることを示します。 |`true` |


<span id="websocket"></span>
### WebSocket


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Websocket |Object |いいえ |WebSocket設定を示します。 | |
|Switch |Boolean |いいえ |ユーザーからのリクエストに対してWebSocketサポートを有効にするかどうかを示します。このパラメータには、次の値を指定できます。<br><br><br>* `true`：WebSocketを有効にすることを示します。この機能を有効にすると、CDNはクライアントからのWebSocketリクエストに応答できます。<br><br>* `false`：WebSocketを無効にすることを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|Timeout |Long |いいえ |WebSocket接続のタイムアウト時間を示します。単位は秒で、値の範囲は1～300です。<br><br>このパラメータのデフォルト値は60秒です。 |`60` |


<span id="proxy-protocol"></span>
### PROXY Protocol


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ProxyProtocol |Object |いいえ |PROXYプロトコルの設定。 | |
|Switch |Boolean |いいえ |ユーザーからのリクエストに対してPROXYプロトコルのサポートを有効にするかどうかを示します。このパラメータには以下の値があります。<br><br><br>* `true`: PROXYプロトコルを有効にします。この機能を有効にすると、CDNは受信したPROXYヘッダーを解析してユーザーの実際のIPアドレスを取得できます。<br><br>* `false`: PROXYプロトコルを無効にします。<br><br><br>このパラメータのデフォルト値は`false`です。 |`true` |


<span id="url正規化"></span>
### URL正規化


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|UrlNormalize |Object |いいえ |「URL正規化」機能の設定。 | |
|NormalizeObject |String[] |いいえ |有効にする必要があるURL正規化オプションのリスト。`Switch`が`true`の場合、このパラメーターは必須です。リストには次のオプションを含めることができます。<br><br><br>* `dot_segments`：リクエストURLの次の内容を置き換えることを示します。<br><br>   * `/./`：単一のスラッシュ（/）に置き換えます。<br><br>   * `/../`：`/../`の前に別のレベルのディレクトリがある場合は、`/../`とそのディレクトリを削除します。`/../`の前にディレクトリがない場合は、元のURLを保持します。<br><br>* `back_slashes`：リクエストURLのバックスラッシュ（\）を単一のスラッシュ（/）に置き換えることを示します。<br><br>* `successive_slashes`：リクエストURLの連続するスラッシュ（//）を単一のスラッシュ（/）に置き換えることを示します。 |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメーターのデフォルト値は `false` です。 |`true` |


<span id="地理的制限"></span>
### 地理的制限


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|AreaAccessRule |Object |いいえ |「地理的制限」機能の設定。 | |
|Area |String[] |いいえ |このリストにアローリストまたはブロックリストを適用する国のリスト。`Switch`が`true`の場合、このパラメーターは必須です。国の名前は略語で表されます。[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp) を呼び出して、`Area` を `Global` に指定すると、国と地域の略語を取得できます。 |`["CHE","AZE"]` |
|RuleType |String |いいえ |ルールの種類。`Switch`が`true`の場合、このパラメーターは必須です。このパラメーターには次の値を指定できます。<br><br><br>* `deny`: ブロックリストを指定することを示します。<br><br>* `allow`: アローリストを指定することを示します。 |`allow` |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |


<span id="httpメゾット拒否"></span>
### HTTPメゾット拒否


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|MethodDeniedRule |Object |いいえ |「HTTPトメソッド拒否」機能の設定。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|Methods |String |いいえ |無効にする1つ以上のHTTPリクエストメソッドを示します。`Switch`が`true`の場合、このパラメーターは必須です。複数のメソッドはコンマ（,）で区切られます。このパラメーターには次の値を指定できます。<br><br><br>* `get`：GETリクエストメソッドを無効にすることを示します。<br><br>* `post`：POSTリクエストメソッドを無効にすることを示します。<br><br>* `delete`：DELETEリクエストメソッドを無効にすることを示します。<br><br>* `put`：PUTリクエストメソッドを無効にすることを示します。<br><br>* `head`：HEADリクエストメソッドを無効にすることを示します。<br><br>* `patch`：PATCHリクエストメソッドを示します。<br><br>* `connect`：CONNECTリクエストメソッドを示します。<br><br>* `options`：OPTIONSリクエストメソッドを示します。 |`delete,put` |


<span id="ip制限"></span>
### IP制限


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|IpAccessRule |Object |いいえ |「IP制限」機能の設定。<br><br>この機能には2つの設定方法があります。<br><br><br>* 通常設定：現在のドメインに対して`RuleType`と`Ip`を指定して設定します。<br><br>* ユニバーサルカタログ：`SharedConfig`を指定してユニバーサルカタログを使用します。ユニバーサルカタログはアローリスト機能です。この機能を使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。<br><br><br>設定方法は1つしか選択できません。 | |
|Ip |String[] |はい |ブロックリストまたはアローリストのIPアドレスを示します。`Switch`が`true`の場合、このパラメーターは必須です。1つ以上のIPアドレスとIPアドレス範囲を指定できます。IPアドレスと範囲はIPv4またはIPv6形式にすることができます。最大1,000個のアドレスを入力できます。<br><br>`SharedConfig`を指定した場合、このパラメーターは指定できません。 |`["xx.xxx.xx.xx","x.x.x.x"]` |
|RuleType |String |はい |IPリストの種類を示します。`Switch`が`true`の場合、このパラメーターは必須です。このパラメーターには次の値を指定できます。<br><br><br>* `allow`：アローリストを示します。<br><br>* `deny`：ブロックリストを示します。<br><br><br>`SharedConfig`を指定した場合、このパラメーターは指定できません。 |`deny` |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|SharedConfig |Object |いいえ |ユニバーサルカタログを示します。<br><br>このパラメーターを指定した場合、`RuleType`と`Ip`は指定できません。 | |
|ConfigName |String |いいえ |ユニバーサルカタログの名前を示します。ユニバーサルカタログの`ConfigType`は`deny_ip_access_rule`または`allow_ip_access_rule`である必要があります。<br><br><br>* `deny_ip_access_rule`：IPブロックリストを示します。<br><br>* `allow_ip_access_rule`：IPアローリストを示します。<br><br><br>[ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_jp)を呼び出して、ユニバーサルカタログのリストを取得できます。 |`my_whitelist` |
|DenyStatusCode |Long |いいえ |拦截状态码 | |
|IpSource |Object |いいえ |IP判断来源 | |
|SourceList |String[] |いいえ |无 | |
|Type |String |いいえ |无 | |


<span id="referer制限"></span>
### Referer制限


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|RefererAccessRule |Object |いいえ |「Referer 制限」機能の設定。 | |
|AllowEmpty |Boolean |はい |ユーザーリクエストヘッダーのRefererヘッダーが空（""）の場合に、CDNがリクエストを受け入れるかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：リクエストを受け入れることを示します。<br><br>* `false`：リクエストを拒否することを示します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |
|Referers |String[] |はい |Refererのリストを示します。このパラメーターの入力要件は、`ReferersType`の`CommonType`タイプの`Referers`の入力要件と一致しています。Refererリストを指定するには、`ReferersType`を使用することをお勧めします。<br><br>`SharedConfig`を指定した場合、このパラメーターは指定できません。 |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|ReferersType |Object |はい |`ReferersType`オブジェクトを示します。これには、通常のRefererリストとReferer正規表現リストをそれぞれ表す`CommonType`オブジェクトと`RegularType`オブジェクトが含まれています。<br><br>`SharedConfig`を指定した場合、このパラメーターは指定できません。 | |
|CommonType |Object |はい |通常のRefererのリストを含む`CommonType`オブジェクトを示します。 | |
|IgnoreCase |Boolean |いいえ |`CommonType`のこの`Referers`リストが一致するときに大文字と小文字を区別するかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は`true`です。 |`true` |
|Referers |String[] |はい |通常のRefererのリストを示します。このリストでは、1つ以上のIPアドレス、CIDR範囲、ドメイン、およびワイルドカードドメインを指定できます。ドメインはセカンドレベルドメインにすることができます。IPアドレスはIPv4およびIPv6形式のアドレスにすることができます。最大1,000個のIPアドレスを入力できます。入力したドメインに`http://`または`https://`を含めることはできません。一致する場合、CDNはリクエストRefererヘッダー値のドメインをRefererリストと照合します。このパラメーター値の長さは30,000文字を超えることはできません。 |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreScheme |Boolean |いいえ |`CommonType`のこの`Referers`リストに一致するRefererヘッダー値が`HTTP`または`HTTPS`で始まる必要があるかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：`HTTP`または`HTTPS`で始まらないRefererヘッダー値が有効であることを示します。この場合、CDNはそれを`Referers`リストと照合しようとします。<br><br>* `false`：`HTTP`または`HTTPS`で始まらないRefererヘッダー値が無効であることを示します。この場合、CDNは`CommonType`のこの`Referers`リストと一致しないと判断します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`false` |
|ContMainDomain |Boolean |いいえ |泛域名匹配包含主域名 | |
|RegularType |Object |はい |リクエストのRefererヘッダー値に一致する正規表現リストを含む`RegularType`オブジェクトを示します。このパラメーターはアローリスト機能です。このパラメーターを使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。リクエストのRefererヘッダー値が`CommonType`の`Referers`リストまたは`RegularType`の`Referers`リストに一致する場合、CDNはそれを一致と見なすことに注意してください。 | |
|Referers |String[] |はい |Referer正規表現のリストを示します。このパラメーター値の長さは30,000文字を超えることはできません。 |`^http://a.com` |
|RuleType |String |はい |Refererリストの種類を示します。`Switch`が`true`の場合、このパラメーターは必須です。このパラメーターには次の値を指定できます。<br><br><br>* `allow`：アローリストを示します。<br><br>* `deny`：ブロックリストを示します。 |`deny` |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|SharedConfig |Object |いいえ |ユニバーサルカタログを示します。<br><br>このパラメーターを指定した場合、`Referers`も`ReferersType`も指定できません。 | |
|ConfigName |String |いいえ |ユニバーサルカタログの名前を示します。ユニバーサルカタログの`ConfigType`は`deny_referer_access_rule`または`allow_referer_access_rule`である必要があります。<br><br><br>* `deny_referer_access_rule`：Refererブロックリストを示します。<br><br>* `allow_referer_access_rule`：Refererアローリストを示します。<br><br><br>[ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_jp)を呼び出して、ユニバーサルカタログのリストを取得できます。 |`my_allowlist` |


<span id="ua制限"></span>
### UA制限


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|UaAccessRule |Object |いいえ |「UA 制限」機能の設定。 | |
|AllowEmpty |Boolean |はい |UAが空（""）であるか、UAフィールドが含まれていないリクエストがアクセラレーションドメインにアクセスできるかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：許可することを示します。<br><br>* `false`：許可しないことを示します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |
|IgnoreCase |Boolean |はい |UA文字列で大文字と小文字を区別するかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：UA文字列で大文字と小文字を区別しないことを示します。<br><br>* `false`：UA文字列で大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |
|RuleType |String |はい |ブロックリストとアローリストのどちらを指定するかを示します。`Switch`が`true`の場合、このパラメーターは必須です。このパラメーターには次の値を指定できます。<br><br><br>* `deny`：ブロックリストを指定することを示します。<br><br>* `allow`：アローリストを指定することを示します。 |`deny` |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|UserAgent |String[] |はい |UAのリストを示します。`Switch`が`true`の場合、このパラメーターは必須です。このリストには最大1,000個のUAを含めることができます。このパラメーターの説明は次のとおりです。<br><br><br>* このパラメーター値の長さは30,000文字を超えることはできません。<br><br>* `RuleType`が`allow`の場合、リストに含まれるUAを含むリクエストのみがアクセラレーションドメインにアクセスできることを示します。<br><br>* `RuleType`が`deny`の場合、アクセスリクエストにリストに含まれるUAが含まれている場合、アクセラレーションドメインへのアクセスは許可されないことを示します。<br><br><br>UAに含めることができる文字には次の制限があります。<br><br><br>* UAでは、`*`を使用して1つ以上の文字を表すことができます。`*`はUAの先頭と末尾にのみ表示できます。<br><br>* UAに`*`またはスペースのみを含めることはできません。<br><br>* UAに記号が含まれている場合、記号はHTMLエンコードされている必要があります。 |`["*curl*","*Mozilla*"]` |
|SharedConfig |Object |いいえ |全局配置 | |
|ConfigName |String |いいえ |配置名称 | |


<span id="origin制限"></span>
### Origin制限


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginAccessRule |Object |いいえ |「Origin 制限」機能の設定。 | |
|AllowEmpty |Boolean |はい |ユーザーリクエストヘッダーのOriginヘッダーが空（""）の場合にリクエストを許可するかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：許可することを示します。<br><br>* `false`：許可しないことを示します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |
|IgnoreCase |Boolean |はい |Originで大文字と小文字を区別するかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：Originで大文字と小文字を区別しないことを示します。<br><br>* `false`：Originで大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は`true`です。 |`true` |
|Origins |String[] |はい |`RuleType`に対応するアドレスリスト。`Switch`が`true`の場合、このパラメーターは必須です。1つ以上のIPアドレス、CIDR範囲、ドメイン、およびワイルドカードドメインを指定できます。ドメインはセカンドレベルドメインにすることができます。IPアドレスはIPv4およびIPv6形式のアドレスにすることができます。最大`100`個のアドレスを入力できます。ドメインを入力するときに`http://`または`https://`を含める必要はありません。このパラメーター値の長さは3000文字を超えることはできません。 |`["www.test.com"]` |
|RuleType |String |はい |オリジンリストの設定タイプ。`Switch`が`true`の場合、このパラメーターは必須です。このパラメーターには次の値を指定できます。<br><br><br>* `allow`：アローリストを示します。<br><br>* `deny`：ブロックリストを示します。 |`deny` |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |


<span id="カスタムブロックルール"></span>
### カスタムブロックルール


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|


<span id="署名付きurl認証"></span>
### 署名付きURL認証


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|SignedUrlAuth |Object |いいえ |「署名付きURL認証」機能の設定を表します。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|SignedUrlAuthRules |Object[] |いいえ |認証ルールの設定ルールを示します。現在、1つのルールのみ設定可能です。`Switch`が`true`の場合、このパラメーターは必須です。 | |
|Condition |Object |はい |`SignedUrlAuthAction`に対応し、認証設定ルールがどのファイルに適用されるかを示します。このパラメーターを指定しない場合、すべてのファイルに適用されます。 | |
|ConditionRule |Object[] |はい |このパラメーターはリストであり、次のように説明されます。<br><br><br>* 各リスト要素は、有効なオブジェクト設定です。<br><br>* `URLAuthType`が`typea`、`typed`、`typee`の場合、最大10個の設定を作成できます。`URLAuthType`が`typeb`、`typec`の場合、1つの設定しか作成できません。<br><br>* リスト内の要素の順序は、対応する設定の優先順位を示します。リストの最初の要素に対応する設定が最も優先されます。複数の設定を作成する場合、設定間に包含関係があるかどうかに注意する必要があります。包含関係がある場合、範囲の広い設定を範囲の狭い設定の後に配置する必要があります。 | |
|Object |String |はい |CDNがどのオブジェクトタイプに対してルールマッチングを実行するかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `filetype`：特定の拡張子を持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。<br><br><br>`URLAuthType`が`typeb`、`typec`の場合、このパラメーターの値は`filetype`または`directory`しか指定できないことに注意してください。 |`directory` |
|Operator |String |はい |マッチング方法を示します。このパラメーターには次の値を指定できます。<br><br><br>* `match`：`object`が`Value`と一致することを示します。<br><br>* `not_match`：`object`が`Value`と一致しないことをを示します。<br><br><br>このパラメーターのデフォルト値は`match`です。<br><br>`URLAuthType`が`typeb`、`typec`の場合、このパラメーターの値は`match`しか指定できないことに注意してください。 |`match` |
|Type |String |はい |マッチングオブジェクト。変更時に指定する必要があります。現在、URLリクエストリンクを示す`url`のみがサポートされています。 |`url` |
|Value |String |はい |マッチング条件の一致値を表示します。複数の一致値はセミコロン（;）で区切り、総文字数は1,024文字を超えることはできません。また、以下の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>さらに、<br><br><br>* `Object`が`filetype`の場合、各一致値はファイル拡張子を表し、ピリオド（.）で始めることはできません。例：`png;txt`。<br><br>* `Object`が`directory`の場合、各一致値はディレクトリパスを表し、スラッシュ（/）で始まり、スラッシュで終わる必要があります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object`が`path`の場合、各一致値はURLパスを表し、スラッシュ（/）で始まる必要があります。一致値にはアスタリスク（\*）を含めることができ、1つまたは複数の任意の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* `Object`が`regex`の場合、各一致値はURLパスに一致する正規表現です。例：`^/a{1,2}.*g$`。 |`png;jpg` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |
|Connective |String |はい |複数の`ConditionRule`間の論理関係を示します。このパラメーターには次の値を指定できます。<br><br><br>* `AND`: 論理関係が「AND」であることを示します。<br><br>* `OR`：論理関係が「OR」であることを示します。<br><br><br>このパラメーターのデフォルト値は`OR`です。 |`OR` |
|SignedUrlAuthAction |Object |はい |署名計算の設定を示します。 | |
|Duration |Long |はい |署名の有効期間（秒単位）。このパラメーターは、リクエストに含まれるタイムスタンプと組み合わせて使用され、署名の有効期限を計算します。このパラメーターの有効範囲は`0〜315,360,000`です。署名の有効期限=タイムスタンプ+`Duration`。CDNがリクエストを受信したときに、署名の有効期限が現在時刻より前の場合、CDNは署名が期限切れであると判断します。 |`1000` |
|MasterSecretKey |String |はい |プライマリキーを表します。長さは 120 文字以内で指定してください。 |`abcdefg` |
|URLAuthType |String |はい |署名タイプ。このパラメーターには、`typea`、`typeb`、`typec`、`typed`、`typee`の値を指定できます。各タイプの認証手順については、[URL認証の設定](https://docs.byteplus.com/en/docs/byteplus-cdn/signed-url-authentication-jp)を参照してください。 |`typea` |
|BackupSecretKey |String |いいえ |バックアップキーを表します。長さは 120 文字以内で指定してください。 |`abcdefg` |
|CustomVariableRules |Object |いいえ |カスタム署名変数を指定します。 | |
|CustomVariableInstances |Object[] |はい |変数リストを示します。 | |
|Operator |String |はい |変数の一致方法を示します。このパラメーターの値は`match`のみです。 |`match` |
|Type |String |はい |変数のタイプを示します。このパラメーターには次の値を指定できます。<br><br><br>* `queryString`：変数がリクエストのクエリパラメーターであることを示します。<br><br>* `requestHeader`：変数がリクエストのヘッダーフィールドであることを示します。 |`queryString` |
|Value |String |はい |変数の名前を示します。長さは100文字以内です。変数の名前の要件は次のとおりです。<br><br><br>* `Type`が`queryString`の場合、変数名には文字、数字、ハイフン（\-）、コンマ（,）、ピリオド（.）、感嘆符（!）を含めることができます。<br><br>* `Type`が`requestHeader`の場合、変数名には次の文字を含めることができません：<br><br>   * アンダースコア（_）、スペース、二重引用符（"）、コロン（:） |`myparam1` |
|RewriteM3u8 |Boolean |いいえ |HLS マニフェスト (.m3u8) リクエストの場合、このパラメータは、CDN がマニフェストを変更して各ビデオセグメントの署名を生成し、その署名を URI に追加するかどうかを示します。<br><br>このパラメータの値は次のとおりです。<br><br><br>* `true`: マニフェストを変更することを示します。<br><br>* `false`: マニフェストを変更しないことを示します。<br><br><br>このパラメータのデフォルト値は `false` です。<br><br>`URLAuthType` が `typee` の場合、このパラメータは無効です。<br><br>说明<br><br>現在、CDN は圧縮ファイルを変更しません。したがって、以下の状況では CDN はマニフェストを変更しません。<br><br><br>* オリジンサーバーのレスポンスに `Content-Encoding` ヘッダーが含まれている。このヘッダーは、マニフェストが圧縮されていることを示します。<br><br>* ユーザーリクエストが「ファイル圧縮」機能のルールに一致する場合。 |`true` |
|SignName |String |いいえ |署名パラメーターの名前を示します。このパラメーターの説明は次のとおりです。<br><br><br>* 英字、数字、アンダースコア（_）、ハイフン（\-）、ピリオド（.）、コンマ（,）、感嘆符（!）を含めることができます。<br><br>* 長さは100文字を超えることはできません。<br><br>* 少なくとも1つの文字または数字を含める必要があります。<br><br>* `TimeName`と同じにすることはできません。<br><br><br>`URLAuthType`が`typea`、`typed`、`typee`の場合、このパラメーターは必須です。他のタイプの場合、このパラメーターは有効になりません。 |`sign` |
|SignatureRule |String[] |いいえ |`URLAuthType`が`typee`の場合、このパラメーターは必須であり、署名計算に含める必要があるフィールドを示します。署名計算に含める必要があるフィールドは次のとおりです。<br><br><br>* `key`：キー。つまり、`MasterSecretKey`または`BackupSecretKey`のパラメーターの内容。<br><br>* `uri`：ユーザーがリクエストしたリソースのURIを示します。URIに中国語の文字が含まれている場合は、URIをエンコードする必要があります。<br><br>* `TimeName`：タイムスタンプパラメーターのパラメーターの内容を示します。<br><br><br>署名計算に含めることができるオプションのフィールドは次のとおりです。<br><br><br>* `domain`：ドメイン名を示します。<br><br>* `referer`：ユーザーリクエストで伝送されるreferer値を示します。<br><br>* `ua`：ユーザーリクエストで伝送されるUser\-Agent値を示します。<br><br>* `ip`：ユーザーリクエストのクライアントIPを示します。<br><br>* `origin`：ユーザーリクエストで伝送されるOrigin値を示します。<br><br>* カスタム変数：`CustomVariableInstances`で定義した変数名を示します。<br><br><br>リストの入力順序は、署名計算時の`MD5()`の各値の順序です。 |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |いいえ |`TimeName` で使用される基数を示します。<br><br><br>* `decimal`：10進数。<br><br>* `heximal`：16進数。<br><br><br>`URLAuthType`が`typed`、`typee`の場合、このパラメーターは必須です。`URLAuthType`が`typec`の場合、このパラメーターを設定したかどうかに関係なく、このパラメーターの値は強制的に`heximal`に設定されます。`URLAuthType`の他の値の場合、このパラメーターは有効になりません。 |`heximal` |
|TimeName |String |いいえ |タイムスタンプパラメーターの名前を示します。`TimeName`の値には、英字、数字、アンダースコア（_）、ハイフン（\-）、ピリオド（.）、コンマ（,）、感嘆符（!）を含めることができ、長さは`1〜100`文字です。`TimenName`は`SignName`と同じにすることはできません。<br><br>`URLAuthType`が`typed`、`typee`の場合、このパラメーターは必須です。他のタイプの場合、このパラメーターは有効になりません。 |`TimeParam` |
|DeleteAuthCacheAndOrigin |Boolean |いいえ |去除鉴权参数缓存和回源，仅类型e | |
|AuthRulesF |Object[] |いいえ |タイプF設定を示します。この設定にはルールリストが含まれます。リストには最大5つのルールを含めることができます。リストの最初のルールが最も高い優先度を持ちます。<br><br>ユーザーからのリクエストを受信すると、CDNは優先度の降順でルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。 | |
|ArgumentRule |Object |いいえ |オリジンフェッチパラメータ関連の設定を表します。 | |
|KeepOriginArg |Boolean |いいえ |`AuthTokenCalRule` に基づいて計算されたトークンをオリジンフェッチリクエストに含めるかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：オリジンフェッチリクエストにトークンを含めることを示します。オリジンフェッチリクエストにおけるトークンの位置は `SignCapRule` の設定と同じです。<br><br>* `false`：オリジンフェッチリクエストにトークンを含めないことを示します。 |`true` |
|GeneralParamRule |Object |いいえ |CDN がビデオセグメント URI のクエリパラメータを設定する方法を表します。 | |
|ParentLinkParamInherit |String |いいえ |書き換え後のビデオセグメント URI に、ユーザリクエスト URL 内のトークンとタイムスタンプを表すパラメータ以外のすべてのクエリパラメータを含めるかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `not_inherit`：書き換え後のセグメント URI にこれらのクエリパラメータが含まれないことを示します。<br><br>* `inherit`：書き換え後のセグメント URI にこれらのクエリパラメータが含まれることを示します。 |`not_inherit` |
|SubLinkParamRule |Object |いいえ |この構造体には、追加のクエリパラメータ設定が含まれています。この構造体には、追加のクエリパラメータ設定が含まれています。 | |
|InheritMode |String |いいえ |ビデオセグメント URI とユーザリクエスト URL に同じクエリパラメータが存在する場合、CDN がビデオセグメント URI のそのパラメータの値をどのように設定するかを表します。`ParentLinkParamInherit` が `inherit` の場合、このパラメータを設定できます。<br><br>このパラメータには以下の値があります：<br><br><br>* `sub_link_first`：ビデオセグメント URI のそのパラメータの値を使用することを示します。<br><br>* `inherit_first`：ユーザリクエスト URL のそのパラメータの値を使用することを示します。 |`inherit_first` |
|KeepSubLinkArg |String |いいえ |書き換え後のビデオセグメント URI が URI 内の元のクエリパラメータを保持するかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `delete`：書き換え後のセグメント URI がこれらのクエリパラメータを保持しないことを示します。<br><br>* `keep`：書き換え後のセグメント URI がこれらのクエリパラメータを保持することを示します。 |`delete` |
|AuthTokenCalRule |Object |いいえ |トークン計算の設定を示します。クライアント側でトークン計算ロジックをデプロイし、生成されたトークンをユーザーリクエストに含めるには、サンプルコードを参照してください。<br><br>CDN は `SignJoinSymbol` を使用して `SignParam` 内の各オブジェクトを連結し、連結されたオブジェクトに `ParamCalRules` で指定されたアルゴリズムを適用してトークンを計算し、ユーザーリクエストに含まれるトークンと比較します。 | |
|ParamCalRules |String[] |いいえ |トークンの計算に使用されるアルゴリズムのリストを示します。リストには最大5つのアルゴリズムを含めることができます。CDN は、リスト内のアルゴリズムの出現順にトークンの計算式を生成します。<br><br>このパラメーターには、`md5_bin`、`base64url`、`sha256`、`md5`、`base64_encode`、`sha1`、`sha224`、`sha384`、`sha512`、`sha3_224`、`sha3_256`、`sha3_384`、`sha3_512`、`upper_case`、`lower_case` の値があります。<br><br>说明<br><br>`md5_bin` を指定した場合は、次のアルゴリズムとして `base64url` を指定する必要があります。<br><br><br>* 正しい設定：`sha1`、`md5_bin`、`base64url`<br><br>* 誤った設定：`sha1`、`md5_bin`、`base64url`、`base64url`、`md5_bin` |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |いいえ |`SignParam` の各オブジェクトを連結するために使用される区切り文字を示します。このパラメーターのデフォルト値は空（""）です。 |`00` |
|SignParam |Object[] |いいえ |CDN がトークンを計算するときに使用するオブジェクトのリストを示します。各オブジェクトは `ParamType` と関連する設定で構成されます。たとえば、次の例は、オブジェクトが文字列であり、文字列の値が `str-for-token-calc` であることを示しています。<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|CookieToken |String |いいえ |`ParamType` が `Cookie` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定するクッキーのキーを示します。CDN はそのクッキーの値を取得します。 |`mycookiekey` |
|ParamSource |String |いいえ |このパラメータは、`RewriteMPD` または `RewriteM3U8` が有効で、オブジェクトの `ParamType` が `URI`、`URLParam`、または `FullURI` の場合に指定できます。<br><br>マニフェストに追加されたトークンの場合、このパラメータは、CDN がトークンを計算する際に使用するオブジェクトのソースを示します。<br><br>&nbsp;<br><br>このパラメータには以下の値を指定できます。<br><br><br>* `ParentLink`: オブジェクトがユーザーリクエスト内の URL から取得されることを示します。<br><br>* `ChildLink`: オブジェクトがマニフェスト内のビデオフラグメントの URI から取得されることを示します。<br><br><br>このパラメータのデフォルト値は `ChildLink` です。 |`ParentLink` |
|ParamType |String |いいえ |オブジェクトのタイプを示します。このパラメーターには次の値があります。<br><br><br>* `SecretKey`：`SecretKey` 構造体内の `MasterSecretKey` または `BackupSecretKey` を示します。認証が失敗した場合、CDN は `BackupSecretKey` を使用してトークンを計算し、ユーザーリクエストを再認証します。<br><br>* `SupString`：文字列を示します。関連する設定は `SupContent` で指定されます。<br><br>* `URI`：リクエストパス内の連続したセグメントを示します。パスにはクエリ文字列は含まれません。関連する設定は `UriParamSup` と `ParamSource` で指定されます。<br><br>* `URLParam`：リクエストURL内の特定のタイプのオブジェクトを示します。オブジェクトは、クエリパラメーターまたはディレクトリです。関連する設定は `UriParam` と `ParamSource` で指定されます。<br><br>* `ClientDomain`：リクエストドメイン名を示します。<br><br>* `Referer`：ユーザーリクエストのRefererヘッダーの値を示します。<br><br>* `Origin`：ユーザーリクエストのOriginヘッダーの値を示します。<br><br>* `ClientIP`：ユーザーリクエストを送信したクライアントIPアドレスを示します。<br><br>* `UA`：ユーザーリクエストのUser\-Agentヘッダーの値を示します。<br><br>* `ReqHeader`：ユーザーリクエストの特定のヘッダーの値を示します。関連する設定は `RequestHeader` で指定されます。<br><br>* `Cookie`：リクエスト内のクッキーを示します。関連する設定は `CookieToken` で指定されます。<br><br>* `FullURI`：クエリ文字列を含まない完全なリクエストパスを示します。関連する設定は `ParamSource` で指定されます。 |`URI` |
|RequestHeader |String |いいえ |`ParamType` が `ReqHeader` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定するリクエストヘッダーを示します。 |`myheader2` |
|SupContent |String |いいえ |`ParamType` が `SupString` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定する文字列を示します。 |`123abc` |
|UriParamSup |Object |いいえ |リクエストパスから連続したセグメントを取得する方法を示します。`ParamType` が `URI` の場合、このパラメーターを指定する必要があります。<br><br>このパラメーターは、次の設定を含む構造体です。<br><br><br>* リクエストパスの分割に使用する区切り文字。<br><br>* 必要な連続パスセグメントの開始レベルと終了レベル。<br><br>* これらのパスセグメントの連結に使用する区切り文字。連結されたパスセグメントは、トークンの計算に使用されます。 | |
|JoinSymbol |String |いいえ |これらのパスセグメントを連結するために使用される区切り文字を示します。要件は次のとおりです。<br><br><br>* 長さは1文字で、文字、数字、アンダースコア（_）、ハイフン（\-）、バックスラッシュ（/）、感嘆符（!）を使用できます。<br><br><br>このパラメーターのデフォルト値は空（""）です。 |`00` |
|SplitSymbol |String |いいえ |リクエストパスの分割に使用する区切り文字を示します。要件は次のとおりです。<br><br><br>* 長さは1文字で、文字、数字、アンダースコア（_）、ハイフン（\-）、バックスラッシュ（/）、感嘆符（!）を使用できます。 |`-` |
|StartLevel |Long |いいえ |開始セグメントのレベルを示します。要件は次のとおりです。<br><br><br>* 正の整数である必要があります。<br><br>* 合計レベル数を超えることはできません。<br><br>* `StartLevel` で示されるパスセグメントは、`TermLevel` で示されるパスセグメントの右側にあってはなりません。 |`2` |
|TermLevel |Long |いいえ |終了セグメントのレベルを示します。要件は次のとおりです。<br><br><br>* ゼロ以外の整数のみです。<br><br>* 絶対値は合計レベル数を超えることはできません。<br><br><br>`TermLevel` が負の整数の場合、右端のセグメントから左にカウントすることを示します。 |`3` |
|UrlParam |Object |いいえ |URLから目的のオブジェクトを取得する方法を示します。`ParamType` が `URLParam` の場合、このパラメーターを指定する必要があります。<br><br>このパラメーターは、オブジェクトのソースと関連する設定を含む構造体です。 | |
|ArgSegment |Object |いいえ |`ParamName` または `UriLevel` に基づいて取得されたコンテンツを、特定のレベルのフラグメントを抽出するために分割する必要があるかどうかを示します。このフラグメントが取得する必要があるオブジェクトです。 | |
|Level |Long |いいえ |取得したコンテンツが複数レベルのフラグメントに分割された後、必要なオブジェクトが配置されているレベルを示します。このパラメータの要件は次のとおりです。<br><br><br>* Level はゼロ以外の整数である必要があります。<br><br>* Level の絶対値は、レベルの合計数を超えてはなりません。<br><br><br>Level が負の整数の場合、番号は右端のレベルのフラグメントから逆順にカウントされます。<br><br>このパラメータは、`Switch` が `true` の場合に必須です。 |`2` |
|SplitSymbol |String |いいえ |コンテンツを分割するために使用する区切り文字を示します。<br><br>&nbsp;<br><br>`Switch` が `true` の場合、このパラメータを指定する必要があります。 |`-` |
|Switch |Boolean |いいえ |取得したコンテンツを分割するかどうかを示します。このパラメータの値は以下のとおりです。<br><br><br>* `true`: コンテンツを分割する必要があることを示します。<br><br>* `false`: コンテンツを分割する必要がないことを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|CapMode |String |いいえ |オブジェクトのソースを示します。このパラメータには以下の値があります。<br><br><br>* `name`: クエリパラメータを示します。関連する設定は `ParamName` と `ArgSegment` で指定します。<br><br>* `uri`: リクエストパスで指定されたディレクトリを示します。関連する設定は `UriLevel` と `ArgSegment` で指定します。 |`uri` |
|ParamName |String |いいえ |`ParamType` が `name` の場合、このパラメータを指定する必要があります。このパラメータは、指定するクエリパラメータを表します。 |`myparam3` |
|UriLevel |Long |いいえ |このパラメータは、`ParamType` が `uri` の場合に必須です。指定するディレクトリレベルを示します。<br><br>このパラメータの要件は次のとおりです。<br><br><br>* Level は 0 以外の整数である必要があります。<br><br>* 絶対値は、レベルの合計数を超えてはなりません。<br><br><br>Level が負の整数の場合、右端のディレクトリから左方向へカウントされます。 |`2` |
|CustomRewrite |Object |いいえ |ビデオマニフェストの拡張書き換え設定を示します。この設定を有効にすると、CDNは[特別な書き換えロジック](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を使用して[デフォルトの書き換えロジック](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を上書きします。 | |
|RewriteParam |Object[] |いいえ |オブジェクトのリストを表します。CDNはこれらのオブジェクトを連結してトークンを生成し、それを動画セグメントのURLに追加します。 | |
|ParamType |String |いいえ |オブジェクトの種類を示します。このパラメータには以下の値があります。<br><br><br>* `ParentLinkUrlParam`: ユーザーリクエストURL内の何らかのオブジェクトを表します。オブジェクトは、クエリパラメータまたは特定のレベルのディレクトリパスになります。関連する設定は`ParentLinkUrlParam`構造体で指定します。<br><br>* `SupString`: 文字列を表します。関連する設定は`SupContent`構造体で指定します。<br><br>* `ParentLinkURI`: ユーザーリクエストパスの連続したセグメントを表します。パスにはクエリ文字列は含まれません。関連する設定は`ParentLinkUriParamSup`構造体で指定します。<br><br>* `ParentLinkExpire`: ユーザーリクエスト内のトークンのタイムスタンプを表します。`ExpireTimeRule`の`Duration`パラメータの説明を参照してください。<br><br>* `AuthToken`: `AuthTokenCalRule`に基づいて計算されたトークンを表します。<br><br>* `ParentFullURI`: クエリ文字列を除いたユーザー要求の完全なパスを表します。 |`ParentLinkURI` |
|SupContent |String |いいえ |`ParamType` が `SupString` の場合、このパラメータを指定する必要があります。このパラメータは、指定する文字列を表します。 |`abc-13343` |
|ParentLinkUriParamSup |Object |いいえ |ユーザーのリクエストパスからオブジェクトを取得する方法を示します。`ParamType` が `ParentLinkURI` の場合、このパラメータは必須です。<br><br>このパラメータは、以下の設定を含む構造体です。<br><br><br>* リクエストパスを分割するために使用される区切り文字。<br><br>* 連続するパスセグメントの開始レベルと終了レベル。<br><br>* これらのパスセグメントを結合するために使用される連結文字。連結されたパスセグメントは、トークンを生成するために使用されます。 | |
|JoinSymbol |String |いいえ |これらのパスフラグメントを連結するために使用する連結記号を表し、要件は以下の通りです：<br><br><br>* 長さは 1 文字で、アルファベット、数字、アンダースコア（_）、ハイフン（\-）、バックスラッシュ（/）、感嘆符（!）が使用できます。 |`00` |
|SplitSymbol |String |いいえ |リクエストパスの分割に使用する区切り文字を表し、`JoinSymbol` と同じであることが要求されます。 |`-` |
|StartLevel |Long |いいえ |開始フラグメントが位置する階層を表し、要件は以下の通りです：<br><br><br>* 正の整数でなければなりません。<br><br>* 総階層数を超えることはできません。<br><br>* `StartLevel` が示すパスフラグメントは、`TermLevel` が示すパスフラグメントの右側にあってはなりません。 |`1` |
|TermLevel |Long |いいえ |終了フラグメントが位置する階層を表し、要件は以下の通りです：<br><br><br>* 0 以外の整数でなければなりません。<br><br>* 絶対値が総階層数を超えることはできません。<br><br><br>`TermLevel` が負の整数の場合、右端のフラグメントから左に数えることを示します。 |`3` |
|ParentLinkUrlParam |Object |いいえ |URL からオブジェクトを取得する方法を表します。`ParamType` が `ParentLinkUrlParam` の場合、このパラメータを指定する必要があります。<br><br>このパラメータは、オブジェクトのソースと関連設定を含む構造体です。 | |
|ArgSegment |Object |いいえ |`ParamName` または `UriLevel` に基づいて取得したコンテンツを分割して、特定の階層のフラグメントを抽出する必要があるかどうかを表します。このフラグメントが必要なオブジェクトです。 | |
|Level |Long |いいえ |取得したコンテンツを複数の階層のフラグメントに分割した後、必要なフラグメントが位置する階層を表します。このパラメータの要件は以下の通りです：<br><br><br>* 階層は 0 以外の整数です。<br><br>* 絶対値が総階層数を超えることはできません。<br><br><br>階層が負の整数の場合、右端のフラグメントから左に数えることを示します。<br><br>`Switch` が `true` の場合、このパラメータを指定する必要があります。 |`2` |
|SplitSymbol |String |いいえ |コンテンツの分割に使用する区切り文字を表します。<br><br>`Switch` が `true` の場合、このパラメータを指定する必要があります。 |`-` |
|Switch |Boolean |いいえ |取得したコンテンツを分割する必要があるかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|CapMode |String |いいえ |オブジェクトのソースを表します。このパラメータには以下の値があります：<br><br><br>* `name`：クエリパラメータを表します。関連設定は `ParamName` と `ArgSegment` で指定します。<br><br>* `uri`：リクエストパスで指定されたディレクトリを表します。関連設定は `UriLevel` と `ArgSegment` で指定します。 |`name` |
|ParamName |String |いいえ |`CapMode` が `name` の場合、このパラメータを指定する必要があります。このパラメータは、指定するクエリパラメータを表します。 |`myparam5` |
|UriLevel |Long |いいえ |`CapMode` が `uri` の場合、このパラメータを指定する必要があります。このパラメータは、指定するディレクトリ階層を表します。<br><br>このパラメータの要件は以下の通りです：<br><br><br>* 階層は 0 以外の整数です。<br><br>* 絶対値が総階層数を超えることはできません。<br><br><br>階層が負の整数の場合、右端のディレクトリから左に数えることを示します。 |`4` |
|RewriteRule |Object |いいえ |CDN がビデオセグメント URI にトークンを追加する方法を表します。 | |
|CapMode |String |いいえ |CDN が生成されたトークンをビデオセグメント URI にどのように追加するかを表します。このパラメータには以下の値があります：<br><br><br>* `name`：URI で指定されたクエリパラメータをトークンとして設定することを示します。関連設定は `ParamName` で指定します。<br><br>* `uri`：URI で指定されたディレクトリ階層にディレクトリを挿入し、そのディレクトリをトークンとして設定することを示します。関連設定は `UriLevel` で指定します。 |`name` |
|ParamName |String |いいえ |`CapMode` が `name` の場合、このパラメータを指定する必要があります。このパラメータは、指定するクエリパラメータを表します。 |`myparam4` |
|UriLevel |Long |いいえ |`CapMode` が `uri` の場合、このパラメータを指定する必要があります。このパラメータは、指定するディレクトリ階層を表します。<br><br>このパラメータの要件は以下の通りです：<br><br><br>* 階層は 0 以外の整数です。<br><br>* 絶対値が総階層数を超えることはできません。<br><br><br>階層が負の整数の場合、右端の階層のディレクトリから左に数えることを示します。 |`2` |
|SignJoinSymbol |String |いいえ |`RewriteParam` の各オブジェクトを連結するために使用する連結記号を表します。 |`00` |
|Switch |Boolean |いいえ |拡張リライト設定が有効かどうかを示します。このパラメータの値は次のとおりです。<br><br><br>* `true`: 拡張リライト設定を有効にします。<br><br>* `false`: 拡張リライト設定を無効にします。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|ExpireTimeRule |Object |いいえ |トークンの有効期限に関連する設定を示します。 | |
|Duration |Long |いいえ |トークンの有効期間（TTL）を秒単位で示します。値の範囲は 0～315,360,000 で、デフォルト値は `0` です。<br><br><br>* トークンの有効期限 = `ExpTimeCapRule` に基づいて取得されたタイムスタンプ + `Duration` |`20` |
|ExpTimeCapRule |Object |いいえ |トークンタイムスタンプの取得方法を示します。タイムスタンプはUnixタイムスタンプです。 | |
|ArgSegment |Object |いいえ |`ParamName` または `UriLevel` に基づいて取得したコンテンツを分割して、特定のレベルのセグメントを抽出する必要があるかどうかを示します。このセグメントが、取得する必要のあるトークンタイムスタンプです。 | |
|Level |Long |いいえ |コンテンツを複数のレベルのセグメントに分割した後、トークンタイムスタンプが存在するレベルを示します。要件は次のとおりです。<br><br><br>* レベルはゼロ以外の整数です。<br><br>* レベルの絶対値は、合計レベル数を超えることはできません。<br><br><br>レベルが負の整数の場合、右端のセグメントから左にカウントすることを示します。<br><br>`Switch` が `true` の場合、このパラメーターを指定する必要があります。 |`2` |
|SplitSymbol |String |いいえ |コンテンツの分割に使用する区切り文字を示します。<br><br>`Switch` が `true` の場合、このパラメーターを指定する必要があります。 |`-` |
|Switch |Boolean |いいえ |取得したコンテンツを分割する必要があるかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。<br><br><br>このパラメーターのデフォルト値は `false` です。 |`true` |
|CapMode |String |いいえ |トークンタイムスタンプのソースを示します。このパラメーターには次の値があります。<br><br><br>* `name`：クエリパラメーターを示します。関連する設定は `ParamName` と `ArgSegment` で指定されます。<br><br>* `uri`：リクエストパス内のディレクトリを示します。関連する設定は `UriLevel` と `ArgSegment` で指定されます。<br><br>* `header`：リクエスト内のヘッダーを示します。関連する設定は `CustomValue` で指定されます。<br><br>* `cookie`：リクエスト内のクッキーを示します。関連する設定は `CustomValue` で指定されます。 |`header` |
|CustomValue |String |いいえ |このパラメーターの意味は次のとおりです。<br><br><br>* `CapMode` が `header` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定するリクエストヘッダーを示します。<br><br>* `CapMode` が `cookie` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定するクッキーのキーを示します。CDN は対応する値を取得します。 |`myheader1` |
|ParamName |String |いいえ |`ParamType` が `ReqHeader` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定するクエリパラメーターを示します。 |`myparm1` |
|UriLevel |Long |いいえ |`ParamType` が `uri` の場合、このパラメーターを指定する必要があります。このパラメーターは、指定するディレクトリレベルを示します。<br><br>このパラメーターの要件は次のとおりです。<br><br><br>* レベルはゼロ以外の整数です。<br><br>* レベルの絶対値は、合計レベル数を超えることはできません。<br><br><br>レベルが負の整数の場合、パスの右端のディレクトリから左にカウントすることを示します。 |`2` |
|TimeFormat |String |いいえ |トークンタイムスタンプの形式を示します。<br><br><br>* `octal`：8進数を示します。例：`14751410031`。<br><br>* `heximal`：10進数を示します。例：`1738936345`。<br><br>* `decimal`：16進数を示します。例：`67a61019`。 |`heximal` |
|RewriteM3U8 |Object |いいえ |HLS マニフェスト書き換えの設定、つまりマニフェスト内のビデオ セグメント URI にトークンを追加する方法を示します。<br><br>&nbsp;<br><br>`SignCapRule` の `CapMode` が `header` または `cookie` の場合、このパラメータは設定できません。 | |
|RewriteM3U8Tag |Object |いいえ |追加のタグを示します。`Tags` に含まれるタグについては、CDN はそれらのタグの下にある URL にトークンを追加します。[この設定の例](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp) をご覧ください。 | |
|Switch |Boolean |いいえ |追加のタグを設定するかどうかを示します。このパラメータの値は次のとおりです。<br><br><br>* `true`: 追加のタグを設定する必要があることを示します。<br><br>* `false`: 追加のタグが不要であることを示します。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |
|Tags |String[] |いいえ |追加のタグを表すリスト。 |`["tag1","tag2","tag3"]` |
|Switch |Boolean |いいえ |HLSマニフェストの書き換えが必要かどうかを示します。このパラメータには以下の値を指定できます。<br><br><br>* `true`: マニフェストの書き換えが必要であることを示します。<br><br>* `false`: マニフェストの書き換えが必要ないことを示します。<br><br><br>デフォルトでは、CDNはマニフェスト内の`EXTINF`タグ内のビデオセグメントURIにのみトークンを追加します。 |`true` |
|RewriteMPD |Object |いいえ |DASH マニフェストを書き換えるための設定、つまりマニフェスト内のビデオ セグメント URI にトークンを追加する方法を示します。<br><br>&nbsp;<br><br>`SignCapRule` の `CapMode` が `header` または `cookie` の場合、このパラメータは設定できません。 | |
|MpdVarExpand |Boolean |いいえ |`SegmentTemplate`下のURI内の変数を実際の値に置き換えるかどうかを表示します。このパラメータには以下の値があります：<br><br><br>* `true`：この設定を有効にすることを示します。この設定が有効になると、CDNはまずビデオセグメントURIの変数を実際の値に置き換え、次に実際の値を含むURIに基づいてトークンを生成し、最後にトークンをURIに追加します。<br><br>* `false`：この設定を有効にしないことを示します。変数名自体が固定文字列としてトークン生成に使用されます。<br><br><br>このパラメータのデフォルト値は`false`です。<br><br>この設定が有効になると、現在は以下のすべての条件を満たす変数のみが実際の値に置き換えられます：<br><br><br>* 変数が`$RepresentationID$`である。<br><br>* `SegmentTemplate`の下に、以下の条件を満たすURIが少なくとも1つ存在する：<br><br>   * そのURI内で、少なくとも1つの`$RepresentationID$`の出現位置がURIパスの最後のセグメントではない。<br><br>* `<SegmentTemplate ... />`と`<Representation .../>`の間に他のコンテンツが存在しない。<br><br><br>また、書き換えられたDASH Manifest内では、元の`SegmentTemplate`が保持されます。<br><br>[例](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)を参照してください。 |`true` |
|Switch |Boolean |いいえ |DASH マニフェストの書き換えが必要かどうかを示します。このパラメータの値は次のとおりです。<br><br><br>* `true`: マニフェストの書き換えが必要であることを示します。<br><br>* `false`: マニフェストの書き換えが必要ないことを示します。 |`true` |
|SecretKey |Object |いいえ |トークンの計算に使用されるキーを示します。プライマリキーとセカンダリキーが含まれます。 | |
|BackupSecretKey |String |いいえ |セカンダリキーを示し、長さは6～40文字です。 |`secondary-key-456` |
|MasterSecretKey |String |いいえ |プライマリキーを示し、長さは6～40文字です。 |`primary-key-123` |
|SignCapRule |Object |いいえ |ユーザーリクエストからトークンを取得する方法を示します。 | |
|ArgSegment |Object |いいえ |`ParamName`または`UriLevel`に基づいて取得したコンテンツを分割して、特定のレベルのフラグメントを抽出する必要があるかどうかを示します。このレベルのフラグメントが、取得する必要のあるトークンです。 | |
|Level |Long |いいえ |コンテンツを複数のレベルのフラグメントに分割した後、トークンが存在するレベルを示します。要件は次のとおりです：<br><br><br>* レベルは0以外の整数です。<br><br>* レベルの絶対値は合計レベル数を超えることはできません。<br><br><br>レベルが負の整数の場合、右端のフラグメントから左にカウントすることを示します。<br><br>`Switch`が`true`の場合、このパラメータを指定する必要があります。 |`2` |
|SplitSymbol |String |いいえ |コンテンツの分割に使用される区切り文字を示します。<br><br>`Switch`が`true`の場合、このパラメータを指定する必要があります。 |`//` |
|Switch |Boolean |いいえ |取得したコンテンツを分割する必要があるかどうかを示します。このパラメータには次の値があります：<br><br><br>* `true`：コンテンツを分割する必要があることを示します。<br><br>* `false`：コンテンツを分割する必要がないことを示します。<br><br><br>このパラメータのデフォルト値は`false`です。 |`true` |
|CapMode |String |いいえ |トークンのソースを示します。このパラメータには次の値があります：<br><br><br>* `name`：クエリパラメータを示します。関連する設定は`ParamName`で指定されます。<br><br>* `uri`：リクエストパス内のディレクトリを示します。関連する設定は`UriLevel`で指定されます。<br><br>* `header`：リクエスト内のヘッダーを示します。関連する設定は`CustomValue`で指定されます。<br><br>* `cookie`：リクエスト内のCookieを示します。関連する設定は`CustomValue`で指定されます。 |`name` |
|CustomValue |String |いいえ |このパラメータの意味は次のとおりです：<br><br><br>* `CapMode`が`header`の場合、このパラメータを指定する必要があります。このパラメータは、指定するリクエストヘッダーを示します。<br><br>* `CapMode`が`cookie`の場合、このパラメータを指定する必要があります。このパラメータは、指定するCookieのキーを示し、CDNは対応する値を取得します。 |`myheader` |
|ParamName |String |いいえ |`CapMode`が`name`の場合、このパラメータを指定する必要があります。このパラメータは、指定するクエリパラメータを示します。 |`myparam` |
|UriLevel |Long |いいえ |`CapMode`が`uri`の場合、このパラメータを指定する必要があります。このパラメータは、指定するディレクトリレベルを示します。<br><br>このパラメータの要件は次のとおりです：<br><br><br>* レベルは0以外の整数です。<br><br>* 絶対値は合計レベル数を超えることはできません。<br><br><br>レベルが負の整数の場合、パスの右端のディレクトリから左にカウントすることを示します。 |`3` |
|Condition |Object |いいえ |一致条件の設定を示します。リクエストが一致条件を満たす場合、CDNはそのリクエストに対してURL認証を実行します。 | |
|ConditionRule |Object[] |はい |一致条件のリストを示します。リストには最大10個の一致条件を含めることができます。 | |
|Object |String |はい |一致オブジェクトを示します。このパラメータには次の値があります：<br><br><br>* `filetype`：リクエストファイルの拡張子を示します。<br><br>* `directory`：リクエストパス内のディレクトリを示します。<br><br>* `path`：クエリ文字列を含まない完全なリクエストパスを示します。<br><br>* `regex`：完全なパスを照合するために使用される正規表現を示します。 |`directory` |
|Operator |String |はい |一致演算子を示します。このパラメータには次の値があります：<br><br><br>* `match`：`Value`がリクエスト内の`Object`と一致する場合、リクエストはこの一致条件を満たします。<br><br>* `not_match`：`Value`がリクエスト内の`Object`と一致しない場合、リクエストはこの一致条件を満たします。 |`match` |
|Type |String |はい |一致オブジェクトのソースを示します。現在、このパラメータ値は`url`のみで、リクエストURLを示します。 |`url` |
|Value |String |はい |1つ以上の一致値を示し、合計の長さは1,024文字を超えることはできません。複数の一致値はセミコロン（;）で区切られます。一致値には次の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>さらに、<br><br><br>* `Object`が`filetype`の場合、各一致値はファイル拡張子を示し、ピリオド（.）で始まる必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object`が`directory`の場合、各一致値はパスディレクトリを示し、スラッシュ（/）で始まり、スラッシュ（/）で終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object`が`path`の場合、各一致値はクエリ文字列を含まない完全なパスを示します。完全なパスはスラッシュ（/）で始まります。さらに、各一致値にはワイルドカード（\*）を含めることができ、1つ以上の任意の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* `Object`が`regex`の場合、各一致値は正規表現を示します。例：`/a{1,2}(.*)g`。 |`/chs/foods/;/us/birds/` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |
|Connective |String |はい |一致条件間の関係を示します。このパラメータには次の値があります：<br><br><br>* `OR`：「または」の関係を示します。<br><br>* `AND`：「かつ」の関係を示します。<br><br><br>このパラメータのデフォルト値は`OR`です。 |`OR` |
|RuleName |String |いいえ |ルールリスト内のルールの名前を示します。長さは120文字を超えることはできません。ルール名には、漢字、文字、数字、ハイフン（\-）、アンダースコア（_）、およびスペースを含めることができます。漢字1文字は3文字としてカウントされます。 |`Authentication rule A` |
|RewriteFormat |String |いいえ |書き換え後のビデオセグメント URI のフォーマットを表します。このパラメータには以下の値があります：<br><br><br>* `default`：このパラメータ値の意味は `absolute` と同じです。<br><br>* `relative`：URI の現在のフォーマットを維持します。`ExpireTimeRule` の `CapMode` または `SignCapRule` の `CapMode` が `uri` の場合、`RewriteFormat` を `relative` に設定することはできません。<br><br>* `absolute`：URI のフォーマットが相対パスの場合、CDN はフォーマットを絶対パスに変換します。URI が絶対パスまたは完全な URL の場合、現在のフォーマットを維持します。<br><br>* `full`：URI のフォーマットが絶対パスまたは相対パスの場合、CDN はフォーマットを完全な URL に変換します。<br><br><br>このパラメータのデフォルト値は `default` です。 |`default` |


<span id="リモートurl認証"></span>
### リモートURL認証


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|RemoteAuth |Object |いいえ |「リモート認証」機能の設定。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|RemoteAuthRules |Object[] |いいえ |リモート認証の設定ルールリストを示します。`Switch`が`true`の場合、このパラメーターは必須です。設定ルールは1つしか追加できません。 | |
|Condition |Object |はい |認証設定の有効なオブジェクトを示します。有効なオブジェクトは、CDNがどのユーザーのリクエストに対してリモート認証を実行する必要があるかを定義します。 | |
|ConditionRule |Object[] |はい |このパラメーターはリストであり、次のように説明されます。<br><br><br>* 各リスト要素は、有効なオブジェクト設定です。<br><br>* 最大50個の設定を作成できます。<br><br>* リスト内の要素の順序は、対応する設定の優先順位を示します。リストの最初の要素に対応する設定が最も優先されます。複数の設定を作成する場合、設定間に包含関係があるかどうかに注意する必要があります。包含関係がある場合、範囲の広い設定を範囲の狭い設定の後に配置する必要があります。 | |
|Object |String |はい |CDNがどのオブジェクトタイプに対してルールマッチングを実行するかを示します。このパラメーターには次の値を指定できます。<br><br><br>* `filetype`：特定の拡張子を持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。 |`filetype` |
|Operator |String |はい |マッチング方法を示します。このパラメーターには次の値を指定できます。<br><br><br>* `match`：`object`が`Value`と一致することを示します。<br><br>* `not_match`：`object`が`Value`と一致しないことをを示します。<br><br><br>このパラメーターのデフォルト値は`match`です。複数の有効なオブジェクト設定を作成する場合、各設定のこのパラメーターの値は同じでなければならないことに注意してください。 |`match` |
|Type |String |はい |リクエストのターゲットアドレスのタイプを示します。現在、このパラメーターの値は`url`のみです。urlはURLタイプのリンクを示します。 |`url` |
|Value |String |はい |1つまたは複数の一致値を表示し、総文字数は1,024文字を超えることはできません。複数の一致値はセミコロン（;）で区切ります。一致値には以下の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>同時に、<br><br><br>* `Object`が`filetype`の場合、各一致値はリクエストURLの拡張子を表し、ピリオド（.）で始める必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object`が`directory`の場合、各一致値はディレクトリパスを表し、スラッシュ（/）で始まり、スラッシュで終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object`が`path`の場合、各一致値はURLパスを表し、スラッシュ（/）で始まります。各一致値にはワイルドカード（\*）を含めることができ、1つまたは複数の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。 |`png;jpg` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |
|RemoteAuthRuleAction |Object |はい |具体的な認証設定を示します。 | |
|AuthModeConfig |Object |はい |認証サーバーの設定を示します。 | |
|MasterRemoteAddr |String |はい |認証サーバーのプライマリアドレスを示します。プライマリアドレスの形式は `<scheme>://<domain>` または `<scheme>://<ip>` です。`<scheme>` の値は `http` または `https` です。`<domain>` の値は `localhost` にはできません。`<ip>` の値は `127.0.0.1` にはできません。このパラメーター値の長さは 100 文字を超えることはできません。 |`https://primary.example.com` |
|PathType |String |はい |認証リクエストのパスを示します。認証アドレスとリクエストパスが完全な認証 URL を構成します。CDN はユーザーのリクエストをこの認証 URL に転送します。このパラメーターには次の値があります：<br><br><br>* `constant`：認証リクエストのパスがユーザーリクエストのパスと同じであることを示します。<br><br>* `variable`：`pathValue` パラメーターで認証リクエストのパスを指定する必要があることを示します。 |`constant` |
|RequestMethod |String |はい |認証リクエストを送信する際に CDN が使用するリクエストメソッドを示します。このパラメーターには次の値があります：<br><br><br>* `default`：認証リクエストが使用するメソッドがユーザーのリクエストと同じであることを示します。<br><br>* `get`：認証リクエストが GET メソッドを使用することを示します。<br><br>* `post`：認証リクエストが POST メソッドを使用することを示します。<br><br>* `head`：認証リクエストが HEAD メソッドを使用することを示します。 |`get` |
|BackupRemoteAddr |String |いいえ |認証サーバーのバックアップアドレスを示します。アドレスの形式と要件はプライマリアドレスと同じです。 |`https://secondary.example.com` |
|PathValue |String |いいえ |認証リクエストのパスを示します。長さは 100 文字を超えることはできません。パスはスラッシュ（/）で始まる必要があり、次の文字を含めることができません：<br><br><br>* ダブルスラッシュ（//）、パーセント記号（%）、ドル記号（$）、スペース、疑問符（?） |`/auth` |
|AuthResponseConfig |Object |はい |CDN は認証サーバーから返された認証ステータスコードを処理する必要があります。このパラメーターは関連する設定を示します。 | |
|CacheAction |Object |いいえ |CDN は認証ステータスコードをキャッシュできます。このパラメーターは関連する設定を示します。 | |
|Action |String |はい |CDN が認証ステータスコードをキャッシュするかどうかを示します。このパラメーターには次の値があります：<br><br><br>* `nocache`：CDN が認証ステータスコードをキャッシュしないことを示します。<br><br>* `cache`：CDN が認証ステータスコードをキャッシュすることを示します。 |`nocache` |
|Ttl |Long |はい |ブラウザがリクエストされたファイルをキャッシュする時間（秒単位）を示します。CDNは、この値をヘッダー値として、レスポンスに「Cache\-Control: max\-age」ヘッダーを含めます。 |`5` |
|CacheKey |String[] |いいえ |キャッシュキーは、異なるリクエスト URI を区別するために使用されるクエリパラメーターを指定します。各パラメーターは `$` で始まる必要があります。[変数フィールドの説明](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication-jp)でパラメーターを指定することもできます。 |`[$URI,$host]` |
|ResponseAction |Object |いいえ |認証が失敗した場合に CDN がユーザーにどのように応答するかを示します。 | |
|StatusCode |String |いいえ |認証が失敗した場合に CDN がユーザーに応答するステータスコードを示します。400～499 の範囲の任意のステータスコードを指定できます。このパラメーターのデフォルト値は `403` です。 |`403` |
|StatusCodeAction |Object |いいえ |CDN が認証ステータスコードを処理する方法を示します。 | |
|DefaultAction |String |はい |認証ステータスコードが `FailCode` でも `SuccessCode` でもない場合に CDN が認証リクエストを処理する方法を示します。このパラメーターには次の値があります：<br><br><br>* `reject`：CDN が認証の失敗を考慮することを示します。<br><br>* `pass`：CDN が認証の成功を考慮することを示します。 |`pass` |
|FailCode |String |はい |認証が失敗した場合の認証ステータスコードを示します。400～499 の範囲の 1 つ以上のステータスコードを指定できます。複数のステータスコードはセミコロン（;）で区切ります。4xx を指定して 400～499 の範囲の任意のステータスコードを示すこともできます。このパラメーターのデフォルト値は `401` です。 |`403` |
|SuccessCode |String |はい |認証が成功した場合の認証ステータスコードを示します。200～299 の範囲の 1 つ以上のステータスコードを指定できます。複数のステータスコードはセミコロン（;）で区切ります。2xx を指定して 200～299 の範囲の任意のステータスコードを示すこともできます。このパラメーターのデフォルト値は `200` です。 |`200` |
|TimeOutAction |Object |いいえ |認証がタイムアウトした後に CDN が認証リクエストをどのように処理するかを示します。 | |
|Action |String |はい |認証がタイムアウトした後に CDN が認証リクエストを処理するポリシーを示します。このパラメーターには次の値があります：<br><br><br>* `reject`：CDN が認証の失敗を考慮することを示します。<br><br>* `pass`：CDN が認証の成功を考慮することを示します。 |`reject` |
|Time |Long |はい |認証のタイムアウト時間を示します。単位はミリ秒です。このパラメーターのデフォルト値は `200` で、値の範囲は 200～3600 です。 |`200` |
|QueryStringRules |Object |はい |認証リクエストのパラメーター設定を示します。 | |
|QueryStringComponents |Object |いいえ |認証リクエストパラメーターの設定ポリシーを示します。 | |
|Action |String |いいえ |認証リクエストにユーザーリクエスト URL のクエリパラメーターが含まれているかどうかを示します。このパラメーターには次の値があります：<br><br><br>* `exclude`：認証リクエストにクエリパラメーターが含まれていないことを示します。<br><br>* `include`：認証リクエストにすべてのクエリパラメーターが含まれていることを示します。<br><br>* `includePart`：認証リクエストに指定されたクエリパラメーターが含まれていることを示します。 |`exclude` |
|Value |String |いいえ |`Action` パラメーターに対応するパラメーター値を示します。長さは 1,024 文字を超えることはできません。このパラメーターには次の値があります：<br><br><br>* `Action` が `exclude` または `include` の場合、`Value` は `*` である必要があります。<br><br>* `Action` が `includePart` の場合、`Value` パラメーターでユーザーリクエスト URL の 1 つ以上のクエリパラメーターを指定する必要があります。複数のクエリパラメーターはセミコロン（;）で区切ります。`*` は指定できません。クエリパラメーターでは大文字と小文字が区別され、次の文字を含めることができません：<br><br>   * 二重引用符（"）、スペース<br><br><br>このパラメーターのデフォルト値は `*` です。 |`*` |
|QueryStringInstances |Object[] |いいえ |認証リクエストの追加パラメーター設定を示します。最大 50 個のパラメーターを設定できます。 | |
|Action |String |いいえ |認証リクエストパラメーターの設定方法を示します。現在、`Action` を `set` にのみ設定できます。`set` はパラメーターの設定を示します。`Key` で設定する必要がある認証リクエストパラメーターを指定する必要があります。指定した認証リクエストパラメーターが存在しない場合、CDN は認証リクエストにパラメーターを追加します。指定した認証リクエストパラメーターが既に存在する場合、CDN は `Value` の値をその認証リクエストパラメーターの値として使用します。 |`set` |
|Key |String |いいえ |設定する必要がある認証リクエストパラメーターを示します。長さは 1,024 文字を超えることはできません。認証リクエストパラメーターには、次の文字を含めることができません：<br><br><br>* 二重引用符（"）、スペース |`sign` |
|Value |String |いいえ |認証リクエストパラメーターの値を示します。長さは 1,024 文字を超えることはできず、大文字と小文字が区別されます。`Value` には次の値があります：<br><br><br>* `ValueType` が `constant` の場合、認証リクエストパラメーターの値は定数であることを示します。その定数値を指定する必要があります。定数値はドル記号（$）で始めることはできず、次の文字を含めることができません：<br><br>   * 二重引用符（"）<br><br>* `ValueType` が `variable` の場合、認証リクエストパラメーターの値は変数から取得されることを示します。この[変数リスト](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication-jp)で変数を指定できます。 |`1235565` |
|ValueType |String |いいえ |`Key` で設定した認証リクエストパラメーターのタイプを示します。`ValueType` には次の値があります：<br><br><br>* `constant`：認証リクエストパラメーターが定数であることを示します。この場合、`Value` でその定数の値を指定する必要があります。<br><br>* `variable`：認証リクエストパラメーターの値が変数から取得されることを示します。`Value` の説明を参照してください。 |`variable` |
|RequestHeaderRules |Object |はい |認証リクエストヘッダーの設定を示します。最大 50 個のヘッダーを設定できます。 | |
|RequestHeaderComponents |Object |いいえ |認証リクエストヘッダーの設定ポリシーを示します。 | |
|Action |String |はい |認証リクエストヘッダーにユーザーリクエストヘッダーが含まれているかどうかを示します。このパラメーターには次の値があります：<br><br><br>* `exclude`：認証リクエストヘッダーにユーザーリクエストヘッダーが含まれていないことを示します。<br><br>* `include`：認証リクエストヘッダーにすべてのユーザーリクエストヘッダーが含まれていることを示します。<br><br>* `includePart`：認証リクエストヘッダーに指定されたユーザーリクエストヘッダーが含まれていることを示します。 |`exclude` |
|Value |String |いいえ |`Action` パラメーターに対応するパラメーター値を示します。長さは 1,024 文字を超えることはできません。このパラメーターには次の説明があります：<br><br><br>* `Action` が `exclude` または `include` の場合、`Value` は `*` である必要があります。<br><br>* `Action` が `includePart` の場合、`Value` パラメーターの値はユーザーリクエストの 1 つ以上のヘッダーです。複数のヘッダーはセミコロン（;）で区切ります。その値は `*` だけでなく、次の文字を含めることができません：<br><br>   * アンダースコア（_）、スペース、二重引用符（"）<br><br><br>このパラメーターのデフォルト値は `*` です。 |`*` |
|RequestHeaderInstances |Object[] |いいえ |認証リクエストヘッダーの設定セットを示します。<br><br>CDN が認証リクエストを開始すると、リクエストに次のヘッダーが既に含まれている可能性があることに注意してください：<br><br><br>* `X-Forwarded-Protocol`、`X-Forwarded-Proto`、`X-Client-Scheme`：これら 3 つのヘッダーはすべてユーザーリクエストが使用するプロトコルを示し、違いはありません。<br><br>* `X-Real-IP`：ユーザーの実際の IP アドレスを示します。このヘッダーの値はプロキシサーバーの影響を受けません。<br><br>* `X-Forwarded-For`：ユーザーの IP アドレスを示します。ユーザーのリクエストがプロキシサーバーを通過した場合、このヘッダーの値はプロキシサーバーの IP アドレスになります。<br><br><br>このパラメーターでこれらのヘッダーを設定することはお勧めしません。これらのヘッダーを設定すると、元の値が上書きされます。 | |
|Action |String |はい |認証リクエストヘッダーの設定方法を示します。現在、このパラメーター値を `set` にのみ設定できます。`set` はリクエストヘッダーの設定を示します。この場合、`Key` で設定する必要があるリクエストヘッダーを指定する必要があります。設定したリクエストヘッダーが存在しない場合、CDN は認証リクエストにリクエストヘッダーを追加します。設定したリクエストヘッダーが既に存在する場合、CDN は `Value` の値をそのリクエストヘッダーの値として使用します。 |`set` |
|Key |String |はい |設定する必要があるリクエストヘッダーを示します。リクエストヘッダーは `host` にすることはできず、長さは 1,024 文字を超えることはできず、大文字と小文字は区別されません。リクエストヘッダーには、次の文字を含めることができません：<br><br><br>* アンダースコア（_）、二重引用符（"）、スペース |`x-test-header` |
|ValueType |String |はい |リクエストヘッダーのタイプを示します。このパラメーターには次の値があります：<br><br><br>* `constant`：リクエストヘッダーの値が定数であることを示します。`Value` パラメーターでその定数の値を指定する必要があります。<br><br>* `variable`：リクエストヘッダーの値が変数から取得されることを示します。`Value` の説明を参照してください。 |`variable` |
|Value |String |いいえ |リクエストヘッダーの値を示します。このパラメーターには次の値があります：<br><br><br>* `ValueType` が `constant` の場合、定数値を指定する必要があります。この定数値の長さは 1,024 文字を超えることはできず、大文字と小文字が区別されます。また、この定数値はドル記号（$）で始めることはできず、次の文字を含めることができません：<br><br>   * 二重引用符（"）<br><br>* `ValueType` が `variable` の場合、リクエストヘッダーの値は変数から取得されることを示します。この[変数リスト](https://docs.byteplus.com/en/docs/byteplus-cdn/remote-authentication-jp)で変数を指定できます。 |`1234fdf` |
|RequestHost |String |いいえ |認証リクエストの HOST ヘッダーの値を示します。このパラメーターのデフォルト値は `default` で、HOST ヘッダーの値がドメイン名と同じであることを示します。 |`www.example.com` |


<span id="データレートスロットリング"></span>
### データレートスロットリング


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|DownloadSpeedLimit |Object |いいえ |「データレートスロットリング」機能の設定を示します。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値があります：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|DownloadSpeedLimitRules |Object[] |いいえ |データレートスロットリングルールのリストを表します。`Switch` が `true` の場合、このパラメータは必須です。このパラメータに関する追加情報は次のとおりです。<br><br><br>* 各ルールには、一致基準とレート制限設定が含まれます。<br><br>* リストには最大 50 個のルールを含めることができます。<br><br>* リスト内でのルールの表示順序は、その優先度を示します。リストの先頭のルールが最も高い優先度を持ちます。<br><br><br>ユーザーからのリクエストを受信すると、CDNは優先度の降順でルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。 | |
|DownloadSpeedLimitAction |Object |はい |スロットリング設定。 | |
|SpeedLimitRate |Long |はい |単一リクエストのダウンロード速度の上限を示します。単位は`B/S`です。このパラメーターの有効範囲は 1～1,073,741,824,000,000 で、使用される進数変換は`1,024`です。 |`500000` |
|SpeedLimitRateAfter |Long |いいえ |データ量を示します。単一リクエストでダウンロードされたデータ量がこの値に達した場合にのみ、そのリクエストに対してデータレートスロットリングが有効になります。単位は`Byte`です。このパラメーターの有効範囲は 0～1,073,741,824,000,000 で、使用される進数変換は`1,024`です。 |`1000` |
|SpeedLimitTime |Object |いいえ |スロットリングが発生する日付と時間帯を示します。 | |
|DayWeek |String |はい |スロットリングが発生する日付を示します。このパラメーターには、`monday`、`tuesday`、`wednesday`、`thursday`、`friday`、`saturday`、`sunday`、`unlimited` の値があります。`unlimited` は毎日を示します。1 つまたは複数の値を指定できます。複数の値はセミコロン（;）で区切ります。 |`monday;friday` |
|BeginTime |String |いいえ |スロットリングが発生する開始時刻を示します。時刻の形式は mm:ss です。`DayWeek` のパラメーター値が `unlimited` の場合、`BeginTime` と `EndTime` パラメーターのデフォルト値はそれぞれ `00:00` と `23:59` に設定されます。 |`05:08` |
|EndTime |String |いいえ |スロットリングが発生する終了時刻を示します。時刻の形式は mm:ss です。`DayWeek` のパラメーター値が `unlimited` の場合、`BeginTime` と `EndTime` パラメーターのデフォルト値はそれぞれ `00:00` と `23:59` に設定されます。 |`16:48` |
|DynamicLimitUnit |String |いいえ |动态限速类型时必填，表示动态限速单位，可选B/S、KB/S、MB/S | |
|LimitQueryName |String |いいえ |动态限速类型时必填，表示限速参数名称 | |
|LimitType |String |いいえ |限速类型。非必填，不传为 normal ，表示固定限速值，dynamic_limit:表示动态限速 | |
|Condition |Object |いいえ |データレートスロットリングのルールを示します。このパラメーターを指定しない場合、スロットリングはすべてのファイルに適用されます。 | |
|ConditionRule |Object[] |はい |データレートスロットリングのルールを示します。 | |
|Object |String |はい |スロットリングルールのタイプを示します。このパラメーターには、次の値があります：<br><br><br>* `filetype`：ファイルのサフィックスを示します。<br><br>* `directory`：特定のディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。<br><br>* `unlimited`：ドメイン名の下のすべてのファイルを示します。<br><br>* `regex`：正規表現に一致するすべてのファイルを示します。このパラメーター値は、デフォルトですべてのユーザーに公開されているわけではありません。この値を使用するには、[チケットを作成](https://console.byteplus.com/workorder/create)してください。 |`filetype` |
|Operator |String |はい |このパラメーターの値は `match` です。 |`match` |
|Type |String |はい |パラメータ値には、「リクエスト URL」を意味する `url` のみを指定できます。 |`url` |
|Value |String |はい |`Object` に対応する具体的なオブジェクトを示します。パラメーター値の長さは 1,024 文字を超えることはできず、大文字と小文字が区別されます。複数のオブジェクトはセミコロン（;）で区切ります。このパラメーターの説明は次のとおりです：<br><br><br>* `Object` が `filetype` の場合、1 つまたは複数のファイルのサフィックスを示します。ファイルのサフィックスには、英字と数字を含めることができます。複数のファイルのサフィックスはセミコロン（;）で区切ります。例：`xlsx` または `png;txt`。<br><br>* `Object` が `directory` の場合、1 つまたは複数のディレクトリパスを示します。複数のパスはセミコロン（;）で区切ります。パスはスラッシュ（/）で始まり、スラッシュ（/）で終わる必要があります。例：`/chs/foods/;/us/birds/`。`/` は、ドメイン名の下のすべてのディレクトリ内のファイルを示します。同時に、パスには次の文字を含めることができません：<br><br>   * ダブルスラッシュ（//）、パーセント記号（%）、ドル記号（$）、スペース、疑問符（?）<br><br>* `Object` が `path` の場合、1 つまたは複数のファイルパスを示します。パスはワイルドカード（\*）を使用して 1 つまたは複数の文字を表すことができます。複数のパスはセミコロン（;）で区切ります。例：`/chs/foods/local\*sets;/us/birds/chickadee`。パスは `/` で始まる必要があります。同時に、パスには次の文字を含めることができません：<br><br>   * ダブルスラッシュ（//）、パーセント記号（%）、ドル記号（$）、スペース、疑問符（?）<br><br>* `Object` のパラメーター値が `unlimited` の場合、`Value` は空の値として扱われます。空の値は、すべてのファイルに適用されることを示します。<br><br>* `Object` が `regex` の場合、1 つまたは複数の正規表現を示します。複数の正規表現はセミコロン（;）で区切ります。例：`/a/*.jpg`。 |`/www/img/f1/;/www/doc/` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |


<span id="キャッシュ設定"></span>
## キャッシュ設定

<span id="キャッシュルール"></span>
### キャッシュルール


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Cache |Object[] |いいえ |「キャッシュルール」機能の設定を示します。<br><br><br>* リストには最大 50 個のルールを含めることができます。<br><br>* リスト内のルールの順序は、ルールの優先順位を定義します。リストの最初のルールの優先順位が最も高くなります。<br><br>* ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。<br><br><br>CDNには、他のルールに一致しないユーザーリクエストに一致する[デフォルトのキャッシュルール](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules-jp#%E3%83%87%E3%83%95%E3%82%A9%E3%83%AB%E3%83%88%E3%81%AE%E3%82%AD%E3%83%A3%E3%83%83%E3%82%B7%E3%83%A5%E3%83%AB%E3%83%BC%E3%83%AB)が含まれています。このデフォルトルールは常に有効で、優先度は最も低くなります。この機能を設定する際に、このデフォルトルールを指定する必要はありません。 | |
|CacheAction |Object |はい |キャッシュ動作に関連する設定を示します。 | |
|Action |String |はい |キャッシュ動作を示します。現在、`cache` のみを指定できます。`cache` は、動作がキャッシュであることを示します。 |`cache` |
|IgnoreCase |Boolean |はい |リクエストされたファイルが `ConditionRule` に一致する場合、CDNが大文字と小文字を区別するかどうかを示します。このパラメーターは、`DefaultPolicy` が `default` の場合にのみ有効です。このパラメーターには次の値があります。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は `false` です。 |`true` |
|Ttl |Long |はい |ブラウザがリクエストされたファイルをキャッシュする時間（秒単位）を示します。CDNは、この値をヘッダー値として、レスポンスに「Cache\-Control: max\-age」ヘッダーを含めます。 |`100` |
|DefaultPolicy |String |いいえ |キャッシュポリシー。このパラメーターには次の値があります。<br><br><br>* `force_cache`：コンソールの **CDNキャッシュ**  + **強制キャッシュ（オン）**  の設定の組み合わせに対応します。<br><br>* `default`：コンソールの **CDNキャッシュ**  + **強制キャッシュ（オフ）**  の設定の組み合わせに対応します。<br><br>* `origin_first`：コンソールの  **オリジンサーバーに従う**  + **追加キャッシュ（オン）**  の設定の組み合わせに対応します。<br><br>* `origin_first_Replenish`：コンソールの  **オリジンサーバーに従う**  + **追加キャッシュ（オフ）**  の設定の組み合わせに対応します。<br><br><br>このパラメーターのデフォルト値は `default` です。これらのキャッシュポリシーの詳細については、[キャッシュルールの設定](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/cdn-cache-rules-jp) を参照してください。 |`force_cache` |
|SetCookieNoCache |Boolean |いいえ |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |はい |条件。リクエストがこの条件のルールを満たす場合、`CacheAction` で定義されたアクションが実行されます。 | |
|ConditionRule |Object[] |はい |コンテンツ一致ルールのリスト。各 `CacheControlRule` には、コンテンツ一致ルールを1つだけ指定できます。 | |
|Object |String |はい |CDNがルールを照合するオブジェクトの種類。このパラメーターには次の値があります。<br><br><br>* `filetype`：特定の拡張子を持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。 |`directory` |
|Operator |String |はい |一致方法。このパラメーターの値は `match` のみです。リクエストされたオブジェクトに対してルールを照合することを示します。 |`match` |
|Type |String |はい |このパラメーターの値は `url` のみです。`url` はURLタイプのリンクを示します。 |`url` |
|Value |String |はい |1つ以上のマッチ値を指定します。合計の長さは1,024文字を超えることはできません。複数のマッチ値はセミコロン（;）で区切られます。マッチ値には次の文字を含めることはできません。<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>さらに、<br><br><br>* `Object` が `filetype` の場合、各マッチ値はリクエストURLの拡張子を示し、ピリオド（.）で始まる必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object` が `directory` の場合、各マッチ値はディレクトリパスを示し、スラッシュ（/）で始まり、スラッシュ（/）で終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object` が `path` の場合、各マッチ値はURLパスを示し、スラッシュ（/）で始まります。各マッチ値にはワイルドカード（\*）を含めることができ、1つ以上の任意の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |


<span id="キャッシュキー"></span>
### キャッシュキー


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|CacheKey |Object[] |いいえ |「キャッシュキー」機能の設定を示します。このパラメーター値は、カスタムキャッシュキールールのリストです。説明は次のとおりです：<br><br><br>* 各リスト要素は、カスタムキャッシュキールールの設定です。<br><br>* 最大 50 個のルールを作成できます。<br><br>* リスト内の要素の順序は、対応するルールの優先順位を示します。リストの最初のルールの優先順位が最も高くなります。<br><br>* ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。<br><br><br>ルールリストの最後に、以下のデフォルトルールを追加する必要があります。このデフォルトルールは、他のルールに一致しないすべてのユーザーリクエストに一致します。デフォルトルールでは、`CacheKeyAction` の設定を調整できますが、`Condition` の設定は調整できません。<br><br>```json```<br>```{```<br>```            "CacheKeyAction": {```<br>```                "CacheKeyComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "IgnoreCase": true,```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Name": "",```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|CacheKeyAction |Object |はい |`Condition` の状況で CDN が実行する操作を示します。 | |
|CacheKeyComponents |Object[] |はい |操作設定のリストを示します。現在、1 つの操作設定のみ設定できます。 | |
|Action |String |はい |実行するアクション。変更時に指定する必要があります。このパラメーターには、次の値があります：<br><br><br>* `exclude`：キャッシュキーにクエリパラメーターが含まれていない、つまりパラメーターを削除してキャッシュします。<br><br>* `include`：キャッシュキーにすべてのクエリパラメーターが含まれている、つまりパラメーターを保持してキャッシュします。<br><br>* `includePart`：キャッシュキーに `Subobject` のクエリパラメーターが含まれている、つまり一部のパラメーターを保持してキャッシュします。<br><br>* `excludePart`：キャッシュキーに `Subobject` のクエリパラメーターが含まれていない、つまり一部のパラメーターを削除してキャッシュします。 |`excludePart` |
|IgnoreCase |Boolean |はい |CDN が `Value` を照合する際に大文字と小文字を区別するかどうかを示します。このパラメーターには、次の値があります：<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は `false` です。 |`true` |
|Object |String |はい |設定する必要があるオブジェクトを示します。現在、`queryString` のみを指定できます。`queryString` は、リクエスト URL のクエリパラメーターを示します。 |`queryString` |
|Subobject |String |はい |1 つまたは複数の `Object` タイプのオブジェクトを指定します。このパラメーターの説明は次のとおりです：<br><br><br>* `Action` が `include` または `exclude` の場合、`Subobject` の値は `*` である必要があります。`*` はすべてのクエリパラメーターを示します。<br><br>* `Action` が `includePart` または `excludePart` の場合、1 つまたは複数のクエリパラメーターを指定できます。指定するクエリパラメーターは `*` にすることはできず、ダブルスラッシュ（//）、パーセント記号（%）、スペースを含めることもできません。複数のクエリパラメーター名はセミコロン（;）で区切ります。<br><br><br>`Subobject` のデフォルト値は `*` です。 |`sign;testParams` |
|Condition |Object |はい |条件を指定します。リクエストがこの条件のルールを満たす場合、`CacheKeyAction` で定義された操作が実行されます。 | |
|ConditionRule |Object[] |はい |コンテンツ一致ルールのリストを示します。各 `CacheKeyGenerationRule` で、1 つのコンテンツ一致ルールのみ指定できます。 | |
|Object |String |はい |CDN がどのオブジェクトタイプに対してルールを照合するかを示します。このパラメーターには、次の値があります：<br><br><br>* `filetype`：特定のサフィックスを持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。 |`directory` |
|Operator |String |はい |一致方法を示します。このパラメーターの値は `match` のみです。リクエストされたオブジェクトに対してルールを照合することを示します。 |`match` |
|Type |String |はい |このパラメーターの値は `url` のみです。`url` は URL タイプのリンクを示します。 |`url` |
|Value |String |はい |1つ以上のマッチ値を指定します。合計の長さは1,024文字を超えることはできません。複数のマッチ値はセミコロン（;）で区切られます。マッチ値には次の文字を含めることはできません。<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>さらに、<br><br><br>* `Object` が `filetype` の場合、各マッチ値はリクエストURLの拡張子を示し、ピリオド（.）で始まる必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object` が `directory` の場合、各マッチ値はディレクトリパスを示し、スラッシュ（/）で始まり、スラッシュ（/）で終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object` が `path` の場合、各マッチ値はURLパスを示し、スラッシュ（/）で始まります。各マッチ値にはワイルドカード（\*）を含めることができ、1つ以上の任意の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |


<span id="urlリダイレクト"></span>
### URLリダイレクト


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|RedirectionRewrite |Object |いいえ |「URLリダイレクト」機能の設定を表します。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメータは次の値を取ります：<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|RedirectionRule |Object[] |いいえ |URLリダイレクトルールのリストを表します。`Switch`が`true`の場合、このパラメータは必須です。リストには最大50個のルールを含めることができます。ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。 | |
|RedirectionAction |Object |はい |URLリダイレクトルールを表します。 | |
|RedirectCode |String |はい |URLリダイレクトの応答ステータスコードを表します。このパラメータは次の値を取ります：<br><br><br>* `301`：ファイルが恒久的に移動されたことを示します。<br><br>* `302`：ファイルが一時的に移動されたことを示します。 |`301` |
|SourcePath |String |はい |ファイルの元のパスを表します。つまり、リクエストに含まれるパスです。パスはスラッシュ（/）で始まり、ダブルスラッシュ（//）、パーセント記号（%）、スペースを含んではいけません。このパラメータ値の長さは1,024文字を超えることはできません。 |`/img/image.png` |
|TargetHost |String |はい |ターゲットパスが属するサイトのドメイン名またはIPアドレスを表します。IPアドレスはIPv4タイプのアドレスである必要があります。このパラメータ値の長さは1,024文字を超えることはできません。このパラメータのデフォルト値はドメインです。 |`www.test.com` |
|TargetPath |String |はい |リダイレクト後のターゲットパスを表します。パスはスラッシュ（/）で始まり、ダブルスラッシュ（//）、パーセント記号（%）、スペースを含んではいけません。このパラメータ値の長さは1,024文字を超えることはできません。 |`/png/image.png` |
|TargetProtocol |String |はい |URLリダイレクト後の新しいリクエストが使用するプロトコルを表します。このパラメータは次の値を取ります：<br><br><br>* `followclient`：元のリクエストのプロトコルを使用することを示します。<br><br>* `http`：新しいリクエストがHTTPプロトコルを強制的に使用することを示します。<br><br>* `https`：新しいリクエストがHTTPSプロトコルを強制的に使用することを示します。 |`followclient` |
|TargetQueryComponents |Object |はい |元のリクエストURLのクエリパラメータの処理方法を表します。 | |
|Action |String |はい |元のリクエストURLのクエリパラメータの処理方法を表します。このパラメータは次の値を取ります：<br><br><br>* `include`：リダイレクト後のURLに元のリクエストURLのすべてのクエリパラメータを含めることを示します。<br><br>* `exclude`：リダイレクト後のURLに元のリクエストURLのクエリパラメータを一切含めないことを示します。<br><br>* `includePart`：リダイレクト後のURLに元のリクエストURLの特定のクエリパラメータを含めることを示します。<br><br>* `excludePart`：リダイレクト後のURLに元のリクエストURLの特定のクエリパラメータを含めないことを示します。 |`include` |
|Value |String |はい |保持または削除するクエリパラメータを表します。複数のクエリパラメータは英語のセミコロン（;）で区切られます。指定されたクエリパラメータには、ダブルスラッシュ（//）、パーセント記号（"）、スペースを含めることはできません。`Value`のデフォルト値は`*`で、すべてのクエリパラメータを表します。<br><br><br>* `Action`が`include`または`exclude`の場合、`Value`は`*`でなければなりません。<br><br>* `Action`が`includePart`または`excludePart`の場合、1つ以上のクエリパラメータを指定できます。この場合、指定するクエリパラメータは`*`にすることはできません。 |`seq` |


<span id="ネガティヴキャッシュ"></span>
### ネガティヴキャッシュ


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|NegativeCache |Object[] |いいえ |「ネガティブキャッシュ」機能の設定。このパラメーター値はリストであり、以下の点にご注意ください。<br><br><br>* 各リスト要素はキャッシュルールの設定です。<br><br>* 最大50個のルールを作成できます。<br><br>* リスト内の要素の順序は、対応するルールの優先順位を表します。リストの最初のルールが最も高い優先順位を持ちます。<br><br>* ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。いずれかのルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。 | |
|NegativeCacheRule |Object |はい |リスト。このリストの各要素はネガティブキャッシュルールです。 | |
|Action |String |はい |キャッシュの動作。現在指定できるのは `cache` のみです。`cache` はキャッシュ動作であることを示します。 |`cache` |
|StatusCode |String |はい |キャッシュするステータスコードを指定します。ステータスコードの範囲は `400`～`599` です。`4xx` または `5xx` を指定することもできます。`4xx` は 400 から 499 までのすべてのステータスコードを表します。`5xx` は 500 から 599 までのすべてのステータスコードを表します。 |`404` |
|Ttl |Long |はい |ブラウザがリクエストされたファイルをキャッシュする時間（秒単位）を示します。CDNは、この値をヘッダー値として、レスポンスに「Cache\-Control: max\-age」ヘッダーを含めます。 |`100` |
|IgnoreCase |Boolean |いいえ |リクエストされたファイルが `ConditionRule` に一致する場合、CDNが大文字と小文字を区別するかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は `false` です。 |`true` |
|Condition |Object |いいえ |ネガティブキャッシュ設定では、条件付き設定はサポートされていません。このパラメーターを指定する必要はありません。このパラメーターを `null` に設定することもできます。 | |
|ConditionRule |Object[] |はい |コンテンツ一致ルールのリスト。各 `NegativeCache` には、コンテンツ一致ルールを1つだけ指定できます。 | |
|Object |String |はい |CDNがルールを照合するオブジェクトの種類。このパラメーターには次の値があります。<br><br><br>* `filetype`：特定の拡張子を持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。 |`directory` |
|Operator |String |はい |一致方法。このパラメーターの値は `match` のみです。リクエストされたオブジェクトに対してルールを照合することを示します。 |`match` |
|Type |String |はい |このパラメーターの値は `url` のみです。`url` はURLタイプのリンクを示します。 |`url` |
|Value |String |はい |1つ以上のマッチング値を示します。合計の長さは1,024文字を超えることはできません。複数のマッチング値はセミコロン（;）で区切られます。マッチング値には、次の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>また、<br><br><br>* `Object` が `filetype` の場合、各マッチング値はリクエストURLのサフィックスを表し、ピリオド（.）で始める必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object` が `directory` の場合、各マッチング値はディレクトリパスを表し、スラッシュ（/）で始まり、スラッシュ（/）で終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object` が `path` の場合、各マッチング値はURLパスを表し、スラッシュ（/）で始まります。各マッチング値には、1つ以上の文字を表すワイルドカード（\*）を含めることができます。例：`/chs/foods/local*sets;/us/birds/chickadee`。 |`png` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |


<span id="ブラウザキャッシュ"></span>
### ブラウザキャッシュ


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|BrowserCache |Object[] |いいえ |「ブラウザキャッシュ」機能の設定。この設定では、次のようにルールのリストを作成できます。<br><br><br>* リストの各要素はルールを表します。各ルールは、一致条件の設定とアクションの設定で構成されます。<br><br>* リストには最大50個のルールを含めることができます。<br><br>* リスト内でのルールの表示順序によって、ルールの優先順位が決まります。リストの最初のルールの優先順位が最も高くなります。<br><br><br>ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。いずれかのルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。 | |
|CacheAction |Object |はい |キャッシュ動作に関連する設定を示します。 | |
|Action |String |はい |キャッシュの動作。現在指定できるのは `cache` のみです。`cache` はキャッシュ動作であることを示します。 |`cache` |
|IgnoreCase |Boolean |はい |リクエストされたファイルが `ConditionRule` に一致する場合、CDNが大文字と小文字を区別するかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：大文字と小文字を区別しないことを示します。<br><br>* `false`：大文字と小文字を区別することを示します。<br><br><br>このパラメーターのデフォルト値は `false` です。 |`true` |
|Ttl |Long |はい |キャッシュ時間（秒単位）。範囲は `0`～`31,536,000` です。`31,536,000` は1年を表します。指定したコンテンツをCDNでキャッシュしたくない場合は、このパラメーターを `0` に設定できます。 |`100` |
|DefaultPolicy |String |いいえ |キャッシュポリシー。このパラメーターには次の値があります。<br><br><br>* `cache`：ポリシーが「キャッシュ」であることを示します。<br><br>* `origin_first`：ポリシーが「オリジンサーバーに従う」であることを示します。<br><br>* `no_cache`：ポリシーが「キャッシュしない」であることを示します。<br><br><br>ブラウザのキャッシュポリシーの詳細については、[ブラウザのキャッシュポリシー](https://docs.byteplus.com/en/docs/byteplus-cdn/browser-cache-jp) を参照してください。 |`cache` |
|SetCookieNoCache |Boolean |いいえ |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |はい |条件。リクエストがこの条件のルールを満たす場合、`CacheAction` で定義されたアクションが実行されます。 | |
|ConditionRule |Object[] |はい |コンテンツ一致ルールのリスト。各 `BrowserCacheRule` には、コンテンツ一致ルールを1つだけ指定できます。 | |
|Object |String |はい |CDNがルールを照合するオブジェクトの種類。このパラメーターには次の値があります。<br><br><br>* `filetype`：特定の拡張子を持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。 |`directory` |
|Operator |String |はい |一致方法。このパラメーターの値は `match` のみです。リクエストされたオブジェクトに対してルールを照合することを示します。 |`match` |
|Type |String |はい |このパラメーターの値は `url` のみです。`url` はURLタイプのリンクを示します。 |`url` |
|Value |String |はい |1つ以上のマッチング値を示します。合計の長さは1,024文字を超えることはできません。複数のマッチング値はセミコロン（;）で区切られます。マッチング値には、次の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>また、<br><br><br>* `Object` が `filetype` の場合、各マッチング値はリクエストURLのサフィックスを表し、ピリオド（.）で始める必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object` が `directory` の場合、各マッチング値はディレクトリパスを表し、スラッシュ（/）で始まり、スラッシュ（/）で終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object` が `path` の場合、各マッチング値はURLパスを表し、スラッシュ（/）で始まります。各マッチング値には、1つ以上の文字を表すワイルドカード（\*）を含めることができます。例：`/chs/foods/local*sets;/us/birds/chickadee`。" |`png` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |


<span id="httpレスポンスへダー"></span>
### HTTPレスポンスへダー


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|ResponseHeader |Object[] |いいえ |「HTTPレスポンスヘッダー」機能の設定。 | |
|ResponseHeaderAction |Object |はい |ユーザーリクエストに応答する際のレスポンスヘッダーに対するCDNの操作を示します。 | |
|ResponseHeaderInstances |Object[] |はい |レスポンスヘッダーの設定ルールリスト。各ルールには、ヘッダー関連の操作設定が含まれています。最大50個のルールを追加できます。 | |
|Action |String |はい |レスポンスヘッダーに対する操作を指定します。このパラメーターには次の値があります。<br><br><br>* `set`：ヘッダーを設定することを示します。設定操作には、追加と変更が含まれます。オリジンサーバーの応答にヘッダーがすでに含まれている場合、ヘッダーの値は上書きされます。オリジンサーバーの応答にヘッダーが含まれていない場合、ヘッダーが追加されます。<br><br>* `delete`：ヘッダーを削除することを示します。 |`set` |
|Key |String |はい |ヘッダーの名前を指定します。名前は1,024文字を超えることはできず、大文字と小文字は区別されません。また、名前には次の文字を含めることができません：<br><br><br>* アンダースコア（_）、スペース、二重引用符（"）<br><br><br>また、ヘッダー名にはこれらの [特定の名前](https://docs.byteplus.com/en/docs/byteplus-cdn/response-header-setting#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85) を使用できません。 |`Content-Disposition` |
|ValueType |String |はい |`Key` の値のタイプを指定します。このパラメーターは、`Action` が `set` の場合にのみ有効です。`Action` が `set` でない場合、このパラメーターは無効です。このパラメーターには次の値があります。<br><br><br>* `constant`：`Key` の値が固定文字列であることを示します。<br><br>* `variable`：`Key` の値が変数から取得されることを示します。<br><br>* `customize`：`Key` の値が変数と固定文字列を連結した文字列であることを示します。 |`constant` |
|AccessOriginControl |Boolean |いいえ |CDNがユーザーリクエストに応答する際に、リクエストヘッダーのOriginフィールドを検証するかどうかを示します。<br><br>このパラメーターには次の値があります。<br><br><br>* `true`：CDNがOriginフィールドを検証することを示します。検証が成功した場合、CDNはレスポンスヘッダーにAccess\-Control\-Allow\-Originフィールドを含めます。フィールド値はOriginフィールド値と同じです。検証が失敗した場合、レスポンスヘッダーにAccess\-Control\-Allow\-Originフィールドは含まれません。<br><br>* `false`：CDNがOriginフィールドを検証しないことを示します。レスポンスヘッダーでは、CDNはAccess\-Control\-Allow\-Originフィールドを含めます。フィールド値は、設定したAccess\-Control\-Allow\-Originのコンテンツです。<br><br><br>このパラメーターのデフォルト値は `false` です。<br><br>このパラメーターは、次のすべての条件が満たされている場合にのみ有効です。<br><br><br>* `Action` が `set` です。<br><br>* `Key` が `Access-Control-Allow-Origin` です。<br><br>* `ValueType` が `constant` です。 | |
|Value |String |いいえ |`Key` の値を示します。このパラメーターは、`Action` が `set` の場合にのみ有効です。`Action` が `set` でない場合、このパラメーターは無効です。`ValueType` が `constant` の場合、ヘッダーの値として固定文字列を指定する必要があります。ヘッダー値の長さは1,024文字を超えることはできず、次の文字を含めることができません。<br><br><br>* ドル記号（$）<br><br><br>`ValueType` が `variable` の場合、`Key` の値は [このリストの変数](https://docs.byteplus.com/en/docs/byteplus-cdn/response-header-setting#%E5%A4%89%E6%95%B0%E3%83%AA%E3%82%B9%E3%83%88) のいずれかになります。名前にアンダースコアが含まれる変数を除き、リスト内のどの変数も `Key` として使用でき、既存の値を置き換えるために固定文字列を割り当てることができます。つまり、名前にアンダースコアが含まれていないこれらの変数を `Key` として使用する場合、その値は上書きできます。<br><br>`ValueType` が `customize` の場合、`Key` の値はリスト内の変数と固定文字列を連結した文字列であることを示します。連結された文字列では、変数は `${変数名}` で表されます。値の例：`${remote_addr}aaa${host}ccc` |`attachment;filename=FileName.xls` |


<span id="カスタムエラーページ"></span>
### カスタムエラーページ


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|CustomErrorPage |Object |いいえ |「カスタムエラーページ」機能の設定。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|ErrorPageRule |Object[] |いいえ |設定ルールのコレクション。最大50個のルールを追加できます。 | |
|ErrorPageAction |Object |はい |ルールの関連設定を示します。 | |
|Action |String |いいえ |実際の操作を示します。現在、指定できるのはredirectパラメータ値のみです。このパラメータはクライアントリクエストをリダイレクトします。 |`redirect` |
|RedirectCode |String |はい |リダイレクトの応答ステータスコードを示します。必要に応じて適切なステータスコードを選択できます。このパラメーターの値は次のとおりです。<br><br><br>* `301`：コンテンツが恒久的に移動したことを示します。<br><br>* `302`：コンテンツが一時的に移動したことを示します。 |`302` |
|RedirectUrl |String |はい |リダイレクトのターゲットアドレスを示します。長さは1,024文字を超えることはできません。アドレスには、プロトコル、ドメイン名、パスを含め、URLの仕様に準拠している必要があります。 |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |はい |400～599の範囲のステータスコードを示します。4xxまたは5xxと入力できます。4xxは400～499のすべてのステータスコードを表します。5xxは500～599のすべてのステータスコードを表します。 |`4xx` |


<span id="マルチレンジ"></span>
### マルチレンジ


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|MultiRange |Object |いいえ |「マルチレンジ」機能の設定を表します。 | |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。この機能が有効になると、CDNは複数の範囲を指定したRangeリクエストを許可します。<br><br>* `false`：この機能を無効にすることを示します。複数の範囲を指定したRangeリクエストを受信した場合、CDNはそのリクエストを拒否し、416応答ステータスコードを返します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |


<span id="古いコンテンツを配信"></span>
### 古いコンテンツを配信


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OfflineCache |Object |いいえ |「Rangeオリジン取得」機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメーターのデフォルト値は`false`です。 | |
|Object |String |いいえ |无 |`request_error,error_code` |
|StatusCode |String |いいえ |无 |`504;505` |
|Switch |Boolean |いいえ |无 |`true` |


<span id="オリジンフェッチ設定"></span>
## オリジンフェッチ設定

<span id="rangeリクエスト"></span>
### Rangeリクエスト


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginRange |Boolean |いいえ |「Rangeリクエスト」機能の設定を示します。このパラメータには以下の値があります。<br><br><br>* `true`: 機能を有効にします。<br><br>* `false`: 機能を無効にします。<br><br><br>このパラメータのデフォルト値は `false` です。 |`true` |


<span id="オリジンリクエストのタイムアウト"></span>
### オリジンリクエストのタイムアウト


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Timeout |Object |いいえ |「オリジンリクエストのタイムアウト」機能の設定を示します。 | |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。この場合、TCPリクエストとHTTPリクエストのタイムアウト時間はデフォルト値のそれぞれ2秒と60秒が使用されます。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |
|TimeoutRules |Object[] |いいえ |タイムアウト時間の構成セットを示します。現在、構成は1つしか指定できません。`Switch`が`true`の場合、このパラメーターは必須です。 | |
|TimeoutAction |Object |いいえ |HTTPリクエストのタイムアウト時間を示します。このパラメーターの有効範囲は5～60です。 | |
|HttpTimeout |Long |いいえ |TCPリクエストのタイムアウト時間を示します。このパラメーターの有効範囲は2～60です。 |`60` |
|TcpTimeout |Long |いいえ |「オリジン取得再試行設定」機能の構成モジュールを示します。この機能を使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。 |`2` |


<span id="リダイレクトフォロー"></span>
### リダイレクトフォロー


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|FollowRedirect |Boolean |いいえ |「リダイレクトフォロー」機能の設定を示します。 |`true` |


<span id="オリジンリクエストのへダー"></span>
### オリジンリクエストのへダー


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|RequestHeader |Object[] |いいえ |リクエストヘッダーの構成ルールのリストを示します。各ルールには、ヘッダー関連の操作設定が含まれています。最大50個のルールを追加できます。 | |
|RequestHeaderAction |Object |はい |リクエストヘッダーの構成ルールのリストを示します。各ルールには、ヘッダー関連の操作設定が含まれています。最大50個のルールを追加できます。 | |
|RequestHeaderInstances |Object[] |はい |リクエストヘッダーの構成ルールのリストを示します。各ルールには、ヘッダー関連の操作設定が含まれています。最大50個のルールを追加できます。 | |
|Action |String |はい |リクエストヘッダーに対する操作を指定します。このパラメーターには次の値があります。<br><br><br>* `set`：ヘッダーを設定することを示します。設定操作には、追加と変更が含まれます。リクエストにヘッダーがすでに含まれている場合、ヘッダーの値は上書きされます。リクエストにヘッダーが含まれていない場合、ヘッダーが追加されます。<br><br>* `delete`：ヘッダーを削除することを示します。 |`set` |
|Key |String |はい |ヘッダーの名前を指定します。名前は1,024文字を超えることはできず、大文字と小文字は区別されません。また、名前には次の文字を含めることができません：<br><br><br>* アンダースコア（_）、スペース、二重引用符（"）<br><br><br>また、ヘッダー名にはこれらの[特定の名前](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header-jp#%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A0%85)を使用できません。 |`Cdn-provider` |
|ValueType |String |はい |`Key`の値のタイプを指定します。このパラメーターは、`Action`が`set`の場合にのみ有効です。`Action`が`set`でない場合、このパラメーターは無効です。このパラメーターには次の値があります。<br><br><br>* `constant`：`Key`の値が固定文字列であることを示します。<br><br>* `variable`：`Key`の値が変数から取得されることを示します。<br><br>* `customize`：`Key`の値が変数と固定文字列を連結した文字列であることを示します。 |`constant` |
|Value |String |いいえ |`Key`の値を示します。このパラメーターは、`Action`が`set`の場合にのみ有効です。`Action`が`set`でない場合、このパラメーターは無効です。`ValueType`が`constant`の場合、ヘッダーの値として固定文字列を指定する必要があります。ヘッダーの値の長さは1,024文字を超えることはできず、次の文字を含めることができません：<br><br><br>* ドル記号（$）<br><br><br>`ValueType`が`variable`の場合、`Key`の値は[このリストの変数](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-header-jp#%E5%A4%89%E6%95%B0%E3%83%AA%E3%82%B9%E3%83%88)のいずれかになります。名前にアンダースコアが含まれる変数を除き、リスト内のどの変数も`Key`として使用でき、既存の値を置き換えるために固定文字列を割り当てることができます。つまり、名前にアンダースコアが含まれていないこれらの変数を使用する場合、その値を上書きできます。<br><br>`ValueType`が`customize`の場合、`Key`の値はリスト内の変数と固定文字列を連結した文字列であることを示します。連結された文字列では、変数は`${変数名}`で表されます。値の例：`aaa${http_host}bbb${msec}ccc` |`bp-cdn` |


<span id="オリジンリクエストのパラメータ"></span>
### オリジンリクエストのパラメータ


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginArg |Object[] |いいえ |「オリジンリクエストパラメータ」設定のルールリストを表示します。<br><br><br>* リストには最大50個のルールを含めることができます。<br><br>* 各ルールには、一致条件（`Condition`）とCDNが実行するアクション（`OriginArgAction`）が含まれています。<br><br>* リスト内のルールの順序がルールの優先順位を定義します。リストの最初のルールが最も高い優先順位を持ちます。<br><br>* ユーザーからのリクエストを受信すると、CDNは優先度の高い順にルールとリクエストを照合します。ルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。いずれかのルールがリクエストに一致すると、CDNは残りのルールの処理を停止します。<br><br><br>ルールリストの最後に、以下のデフォルトルールを**必ず** 追加してください。このデフォルトルールは、他のルールに一致しなかったユーザーリクエストを一致させるために使用されます。このルール内の`Condition`を変更することはできませんが、`OriginArgAction`内の設定は変更できます。<br><br>```JSON```<br>```{```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "OriginArgAction": {```<br>```                "OriginArgComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|Condition |Object |はい |一致条件の設定を表します。リクエストが一致条件を満たす場合、CDNは`OriginArgAction`で指定されたアクションを実行します。現在、指定できる条件は1つだけです。 | |
|ConditionRule |Object[] |はい |一致するルールのリストを表します。現在、リストに含めることができる一致するルールは 1 つだけです。 | |
|Object |String |はい |フィルタータイプを示します。このパラメーターには次の値があります。<br><br><br>* `filetype`：リクエストURL内の拡張子を示します。<br><br>* `directory`：リクエストURL内の特定のディレクトリを示します。<br><br>* `path`：リクエストURL内の完全なパスを示します。<br><br>* `regex`：正規表現を介して、リクエストURL内の完全なパスを示します。このフィルタータイプを使用するには、[チケットを送信](https://console.byteplus.com/workorder/create)してください。 |`directory` |
|Operator |String |はい |比較タイプを示します。このパラメーターの値は`match`のみです。これは、`Value`がリクエスト内の`Object`に一致する場合、リクエストがこのフィルター条件を満たすことを示します。 |`match` |
|Type |String |はい |`Object`がどのオブジェクトのプロパティであるかを示します。現在、このパラメーターの値は`url`のみです。これはリクエストURLを示します。 |`url` |
|Value |String |はい |1つまたは複数の一致値を表示し、総文字数は1,024文字を超えることはできません。複数の一致値はセミコロン（;）で区切ります。一致値には以下の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>同時に、<br><br><br>* `Object`が`filetype`の場合、各一致値はリクエストURLの拡張子を表し、ピリオド（.）で始める必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object`が`directory`の場合、各一致値はディレクトリパスを表し、スラッシュ（/）で始まり、スラッシュで終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object`が`path`の場合、各一致値はURLパスを表し、スラッシュ（/）で始まります。各一致値にはワイルドカード（\*）を含めることができ、1つまたは複数の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。<br><br>* `Object`が`regex`の場合、各一致値は正規表現を表します。正規表現の例については、[設定例](https://docs.byteplus.com/en/docs/byteplus-cdn/query-parameter-jp)を参照してください。 |`/` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |
|OriginArgAction |Object |はい |リクエストが条件を満たしたときに CDN が実行するアクションを示します。 | |
|OriginArgComponents |Object[] |はい |アクションのリストを示します。これらのアクションは、CDNがオリジン取得リクエストでクエリパラメーターをどのように設定するかを定義します。<br><br>現在、リストには1つのアクションしか含めることができません。 | |
|Action |String |はい |* `include`: オリジンGETリクエストURLに、ユーザーリクエストURLのすべてのクエリパラメーターが含まれることを示します。<br><br>* `exclude`：オリジンGETリクエストURLに、ユーザーリクエストURLのクエリパラメーターが含まれないことを示します。<br><br>* `addPart`：オリジンGETリクエストURLに、ユーザーリクエストURLのすべてのクエリパラメーターと、`Subobject`で指定された追加のクエリパラメーターが含まれることを示します。<br><br>* `includePart`：ユーザーリクエストURLに`Subobject`で指定されたクエリパラメーターが含まれている場合、オリジンGETリクエストURLにこれらの指定されたクエリパラメーターが含まれることを示します。<br><br>* `excludePart`：オリジンGETリクエストURLに、`Subobject`で指定されたクエリパラメーターを除く、ユーザーリクエストURLのすべてのクエリパラメーターが含まれることを示します。<br><br>* `set`：オリジンGETリクエストURLに、ユーザーリクエストURLのすべてのクエリパラメーターが含まれることを示します。さらに、`Subobject`で指定したクエリパラメーターとパラメーター値について、CDNは次のアクションを実行します。<br><br>   * これらのクエリパラメーターがユーザーリクエストURLにある場合、CDNはオリジンGETリクエストURLでこれらのパラメーターの値を指定した値に設定します。<br><br>   * ユーザーリクエストURLにこれらのクエリパラメーターが含まれていない場合、CDNはオリジンGETリクエストURLにこれらのクエリパラメーターを追加します。 |`exclude` |
|Object |String |はい |CDNが`Action`を実行するオブジェクトを示します。現在、このパラメーターの値は`queryString`のみです。これはリクエストURLのクエリ文字列を示します。 |`queryString` |
|Subobject |String |はい |1つ以上のクエリパラメーターを示します。複数のクエリパラメーターはセミコロン（;）で区切られ、合計の長さは1,024文字を超えることはできません。`Subobject`には、文字、数字、アンダースコア（_）、コンマ（,）、ハイフン（\-）、ピリオド（.）、感嘆符（!）のみを含めることができます。<br><br>リクエストURLのクエリパラメーターを照合する場合、`Subobject`のパラメーターでは大文字と小文字が区別されます。<br><br>`Subobject`に関する追加の注意事項は次のとおりです。<br><br><br>* `Action`が`include`または`exclude`の場合、`Subobject`は`*`である必要があります。これは、リクエストURLのすべてのクエリパラメーターを示します。<br><br>* `Action`が`includePart`または`excludePart`の場合、`Subobject`は1つ以上のクエリパラメーターを示します。例：`param1;param2`。<br><br>* `Action`が`addPart`または`set`の場合、`Subobject`は1つ以上のクエリパラメーターとパラメーター値を示し、形式は`key=value`です。例：`param1=val1;param2=val2;param3=val3`。 |`*` |


<span id="オリジンリクエストのsni"></span>
### オリジンリクエストのSNI


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|OriginSni |Object |いいえ |「オリジンリクエストのSNI」機能の設定を示します。 | |
|SniDomain |String |いいえ |オリジン取得SNIのドメイン名を指定します。`Switch`が`true`の場合、このパラメーターは必須です。パラメーター値の長さは1,024文字を超えることはできません。 |`img.example.com` |
|Switch |Boolean |いいえ |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。<br><br><br>このパラメーターのデフォルト値は`false`です。 |`true` |


<span id="オリジンリクエストのurlを書き換え"></span>
### オリジンリクエストのURLを書き換え


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|


<span id="コンテンの最適化"></span>
## コンテンの最適化

<span id="ファイル圧縮"></span>
### ファイル圧縮


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|Compression |Object |いいえ |「ファイル圧縮」機能の設定を表します。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |
|CompressionRules |Object[] |いいえ |ファイル圧縮の構成ルールのセットを示します。`Switch`が`true`の場合、このパラメーターは必須です。 | |
|CompressionAction |Object |はい |圧縮操作の設定を示します。 | |
|CompressionType |String[] |はい |CDN が使用する圧縮アルゴリズムを示します。このパラメータには以下の値を指定できます。<br><br><br>* `br`: Brotli 圧縮アルゴリズムを示します。<br><br>* `gzip`: Gzip 圧縮アルゴリズムを示します。<br><br><br>両方のアルゴリズムを同時に指定することもできます。<br><br>CDN は、ユーザーリクエストの `Accept-Encoding` ヘッダーに基づいて、要求されたファイルを圧縮するかどうか、および使用する圧縮アルゴリズムを決定します。 |`["gzip","br"]` |
|CompressionFormat |String |いいえ |CDN がリクエスト内の `Content-Type` ヘッダーに基づいてリクエストを照合することを示します。このパラメータには以下の値があります。<br><br><br>* `default`: `Content-Type` ヘッダーの値が以下のデフォルトリストに含まれている場合、CDN はリクエストされたファイルに対して `CompressionAction` で設定されたアクションを実行します。<br><br>* `customize`: `Content-Type` ヘッダーの値が `CompressionFormat` で指定されたヘッダー値に含まれている場合、CDN はリクエストされたファイルに対して `CompressionAction` で設定されたアクションを実行します。<br><br><br>CDN が `Condition`` の一致条件に基づいてリクエストを照合するようにしたい場合は、`CompressionFormat`を指定したり、`CompressionFormat`を`all` に設定したりする必要はありません。<br><br>\|\|  **デフォルトリスト** <br><br>&nbsp;<br><br>text/html、text/xml、text/plain、text/css、application/javascript、application/x\-javascript、application/rss+xml、text/javascript、image/tiff、image/svg+xml、application/json、application/xml、text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |いいえ |`Content-Type` のフィルター値を示します。<br><br><br>* `CompressionFormat` が `default` または `all` の場合、このパラメータは `*` にする必要があります。<br><br>* `CompressionFormat` が `customize` の場合、1 つ以上のファイルタイプを指定する必要があります。複数のファイルタイプを指定する場合は、カンマ (,) で区切ってください。 |`application/xml,hello/world` |
|MinFileSizeKB |Long |いいえ |最小ファイルサイズの範囲。CDNは、`MinFileSizeKB`と`MaxFileSizeKB`で指定された範囲内のファイルのみを圧縮します。このパラメータの値の範囲は0～2,147,483,647KB（1,024を基数とする）です。デフォルト値は`0`です。 |`10` |
|MaxFileSizeKB |Long |いいえ |ファイルサイズの最大範囲は、1,024を基数として0～2,147,483,647KBです。このパラメータを指定しない場合、ファイルサイズの制限は無制限となります。 |`1000` |
|Condition |Object |いいえ |ルールのセットの有効化条件を示します。現在、ルールには1つの条件しか含めることができません。 | |
|ConditionRule |Object[] |はい |ルールがどのタイプのファイルに適用されるかを示します。このパラメーターには次の値があります。<br><br><br>* `filetype`：特定のサフィックスを持つファイルを示します。<br><br>* `directory`：特定のファイルディレクトリ内のすべてのファイルを示します。<br><br>* `path`：特定のファイルを示します。 | |
|Object |String |はい |照合方式を示します。このパラメーターの値は `match` です。これは `object` が `Value` と一致することを示します。 |`directory` |
|Operator |String |はい |リクエストのターゲットアドレスのタイプを示します。現在、このパラメーターの値は `url` のみです。url は URL タイプのリンクを示します。 |`match` |
|Type |String |はい |`Object` に対応する具体的なオブジェクトを示します。このパラメーター値は照合時に大文字と小文字が区別され、長さは 1,024 文字を超えることはできません。1 つまたは複数のオブジェクトを指定できます。複数のオブジェクトはセミコロン（;）で区切ります。このパラメーターの説明は次のとおりです。<br><br><br>* `Object` が `filetype` の場合、1 つまたは複数のファイルサフィックスを指定する必要があります。ファイルサフィックスには英字と数字を含めることができます。複数のファイルサフィックスはセミコロン（;）で区切ります。例：`xlsx` または `png;txt`。<br><br>* `Object` が `directory` の場合、1 つまたは複数のディレクトリパスを指定する必要があります。複数のディレクトリパスはセミコロン（;）で区切ります。各ディレクトリパスはスラッシュ（/）で始まり、スラッシュで終わる必要があります。例：`/www/img/;/www/doc/`。`/` を使用してドメイン下のすべてのディレクトリを表すことができます。同時に、ディレクトリパスには次の文字を含めることができません：<br><br>   * ダブルスラッシュ（//）、パーセント記号（%）、ドル記号（$）、スペース、疑問符（?）<br><br>* `Object` が `path` の場合、1 つまたは複数のファイルパスを指定する必要があります。ファイルパスでワイルドカード（\*）を使用して 1 つまたは複数の文字を表すことができます。例：`/www/img/image.png;/a*/ab*.png`。複数のファイルパスはセミコロン（;）で区切ります。例：`/www/img/image.png;/doc/study.docx`。ファイルパスは `/` で始まる必要があります。同時に、ファイルパスには次の文字を次の文字を含めることができません：<br><br>   * ダブルスラッシュ（//）、パーセント記号（%）、ドル記号（$）、スペース、疑問符（?） |`url` |
|Value |String |はい |1つまたは複数の一致値を表示し、総文字数は1,024文字を超えることはできません。複数の一致値はセミコロン（;）で区切ります。一致値には以下の文字を含めることはできません：<br><br><br>* ダブルスラッシュ（//）、スペース、ドル記号（$）、疑問符（?）。<br><br><br>同時に、<br><br><br>* `Object`が`filetype`の場合、各一致値はリクエストURLの拡張子を表し、ピリオド（.）で始める必要はなく、文字と数字のみを含めることができます。例：`png;txt`。<br><br>* `Object`が`directory`の場合、各一致値はディレクトリパスを表し、スラッシュ（/）で始まり、スラッシュで終わります。例：`/chs/foods/;/us/birds/`。<br><br>* `Object`が`path`の場合、各一致値はURLパスを表し、スラッシュ（/）で始まります。各一致値にはワイルドカード（\*）を含めることができ、1つまたは複数の文字を表します。例：`/chs/foods/local*sets;/us/birds/chickadee`。 |`/img/` |
|IgnoreCase |Boolean |いいえ |是否忽略大小写，仅支持cache_key | |


<span id="ファイル最小化"></span>
### ファイル最小化


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|PageOptimization |Object |いいえ |「ファイル最小化」機能の設定を示します。 | |
|OptimizationType |String[] |はい |最適化の対象を示します。このパラメーターには次の値があります。<br><br><br>* `html`: HTML ページを示します。<br><br>* `js`: JavaScript コードを示します。<br><br>* `css`: CSS コードを示します。<br><br><br>このパラメーターのデフォルト値は `html` です。`js` または `css` を指定した場合、`html` も指定する必要があります。 |`["html","js"]` |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |


<span id="ビデオシーク"></span>
### ビデオシーク


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|VideoDrag |Object |いいえ |「ビデオシーク」機能の設定を示します。 | |
|Switch |Boolean |はい |この機能を有効にするかどうかを示します。このパラメーターには次の値があります。<br><br><br>* `true`：この機能を有効にすることを示します。<br><br>* `false`：この機能を無効にすることを示します。 |`true` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="作成したポリシー情報"></span>
## 作成したポリシー情報

<span id="ポリシーid"></span>
### ポリシーID


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|TemplateId |String |作成された配信ポリシーのIDを示します。 | |


<span id="リクエスト例"></span>
## リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=CreateServiceTemplate&Version=2021-03-01
{
    "Title": "TestPolicy",
    "Message": "This is a test.",
    "Project": "default",
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
                        "Value": "jpg;png",
                        "IgnoreCase": true
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
                    "MaxFileSizeKB": 102400,
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
                    "MaxFileSizeKB": 100000,
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
        "StatusCode": "500",
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
                        "Address": "bpcntest.tos-cn-shanghai.bytepluses.com.cn",
                        "InstanceType": "tos",
                        "OriginHost": "bpcntest.tos-cn-shanghai.bytepluses.com.cn",
                        "OriginType": "primary",
                        "PrivateBucketAccess": true,
                        "PrivateBucketAuth": {
                            "AuthType": "tos",
                            "Switch": true
                        },
                        "Region": "cn-shanghai",
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
    "OriginRetry": {
        "StatusCode": "504",
        "Switch": true
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
```


<span id="レスポンス例"></span>
## レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "20250825062009F02F48A66E223DAF57B1",
        "Action": "CreateServiceTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-sezpk72"
    }
}
```


&nbsp;
