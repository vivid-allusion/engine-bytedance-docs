---
title: "UpdateRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_jp"
---

ルールエンジンテンプレート内の設定を更新します。

`Title`および`Message`以外のパラメータを更新する場合は、`UpdateRuleEngineTemplate`を呼び出す際に`TemplateVersion`を`draft`として指定する必要があります。つまり、更新対象のポリシーがDraftバージョンを既に持っている必要があります。更新対象のポリシーがDraftバージョンを持っていることを確認するには、以下の手順を実行します：


1. 対象ポリシーに対して[DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp)APIを呼び出します。

2. APIから返されるバージョンリストで、Draftバージョン（`"Version": "draft"`）が存在するかを確認します。

   * Draftバージョンが存在する場合、そのポリシーに対して`UpdateRuleEngineTemplate`を呼び出すことができます。

   * それ以外の場合は、まず対象ポリシーに対して[CreateTemplateVersion](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_jp)を呼び出してDraftバージョンを作成し、その後で`UpdateRuleEngineTemplate`を呼び出す必要があります。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このAPIは、BytePlus SDK for Python v1.0.40以降のバージョンに統合されています。<a href="https://github.com/byteplus-sdk/byteplus-sdk-python">最新版のBytePlus SDK for Python</a>を入手してください。</div>


<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplateDoc&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はUpdateRuleEngineTemplateDocです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |設定を変更するルールエンジンポリシーのIDを表します。<br><br>変更したいルールエンジンポリシーのIDは、[DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/DescribeTemplates_jp)を使用して取得できます。 |`tpl-rev6j89` |
|Message |String |いいえ |新しいポリシー説明を表し、長さは120文字を超えることはできません。 |`new-desc` |
|Rule |Object |いいえ |ルールの設定を表します。このパラメータの実際のデータ型はStringです。APIリクエストを送信する際は、`Rule`構造体をシリアライズして、JSON形式を文字列形式に変換する必要があります。操作手順は以下の通りです：<br><br><br>1. 改行とスペースを削除します。<br><br>2. `"`を`\"`に置き換えます。<br><br>3. 処理後のコンテンツを文字列として`Rule`の値に設定します。<br><br><br>**設定例**<br><br>`"Rule": "{\"IfBlock\":{\"SubRules\":[],\"Actions\":[{\"Action\":\"origin_tcp_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"30\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}],\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Condition\":{\"Object\":\"always\"}}]}]}}}"` | |
|IfBlock |Object |はい |ルール内のIF式を表し、`Condition`、`Actions`、`SubRules`の構造体を含みます。これらの構造体は、以下のリクエスト処理ロジックを示します：<br><br><br>* ユーザーリクエストが`Condition`のマッチング条件を満たす場合、CDNは最初に`IfBlock`内の`Actions`の操作を実行し、その後`IfBlock`内の`SubRules`のサブルールを処理します。<br><br>* それ以外の場合、CDNは最初に`ElseBlock`内の`Actions`の操作を実行し、その後`ElseBlock`内の`SubRules`のサブルールを処理します。 | |
|SubRules |Object[] |いいえ |IF式の下のサブルールリストを表します。リストには最大10個のサブルールを含めることができます。 | |
|Desc |String |いいえ |サブルールの説明を表します。 |`Sub-rule1` |
|IfBlock |Object |はい |サブルールの下のIF式を表し、親ルールの`IfBlock`と同じ意味およびパラメータを含みます。注意点として、サブルール内ではサブルールをネストできません。そのため、サブルール内の`IfBlock`の`SubRules`構造体の値は空（`[]`）である必要があります。 | |
|SubRules |String[] |いいえ | | |
|Actions |Object[] |はい | | |
|Action |String |はい | |`response_header` |
|Stage |String |いいえ | |`client_response` |
|Phase |Integer |いいえ | |`6` |
|Module |Integer |いいえ | |`1` |
|Groups |Object[] |いいえ | | |
|Dimension |String |いいえ | |`response_header` |
|GroupParameters |Object[] |いいえ | | |
|Parameters |Object[] |いいえ | | |
|Name |String |はい | |`action` |
|Values |String[] |はい | | |
|Condition |Object |はい | | |
|IsGroup |Boolean |はい | |`true` |
|Connective |String |はい | |`and` |
|ConditionGroups |Object[] |はい | | |
|IsGroup |Boolean |いいえ | |`true` |
|Connective |String |いいえ | |`and` |
|ConditionGroups |Object[] |いいえ | | |
|IsGroup |Boolean |はい | |`false` |
|Condition |Object |はい | | |
|Object |String |はい | |`always` |
|Operator |String |はい | |`suffix_match` |
|IgnoreCase |Boolean |はい | |`true` |
|Value |String[] |はい | | |
|ElseBlock |Object |いいえ |サブルールの下のELSE式を表し、親ルールの`ElseBlock`と同じ意味およびパラメータを含みます。 | |
|SubRules |String[] |いいえ | | |
|Actions |Object[] |はい | | |
|Action |String |いいえ | |`response_header` |
|Stage |String |いいえ | |`client_response` |
|Phase |Integer |いいえ | |`6` |
|Module |Integer |いいえ | |`1` |
|Groups |Object[] |いいえ | | |
|Dimension |String |いいえ | |`response_header` |
|GroupParameters |Object[] |いいえ | | |
|Parameters |Object[] |いいえ | | |
|Name |String |はい | |`action` |
|Values |String[] |はい | | |
|Actions |Object[] |はい |CDNが実行するアクションリストを表します。各アクションは1つのCDN機能設定です。<br><br>現在、一部のCDN機能はルールエンジンで設定できませんが、将来的に順次サポートされる予定です。ルールエンジンでサポートされるCDN機能については、`Action`パラメータの説明を参照してください。 | |
|Action |String |いいえ |CDN機能の名前を表します。このパラメータには以下の値があります：<br><br><br>* `redirect_request`："URLリダイレクト書き換え"を表します。<br><br>* `redirect_protocol`："プロトコル強制ジャンプ"を表します。<br><br>* `allow_access`：受信したすべてのユーザーリクエストを許可することを表します。<br><br>* `download_speed_limit`："ダウンロード速度制限"を表します。<br><br>* `request_header`："クライアントリクエストヘッダー設定"を表します。<br><br>* `deny_access`：受信したすべてのユーザーリクエストを拒否することを表します。<br><br>* `cache_key`："キャッシュキー"を表します。<br><br>* `compression`："ファイル圧縮"を表します。<br><br>* `video_drag`："ビデオシーク"を表します。<br><br>* `cache_time`："エッジノードキャッシュルール"を表します。<br><br>* `origin_range`："レンジGET"を表します。<br><br>* `origin_follow`："リダイレクト追従"を表します。<br><br>* `origin_tcp_timeout`："オリジンTCPタイムアウト"を表します。<br><br>* `origin_http_timeout`："オリジンHTTPタイムアウト"を表します。<br><br>* `response_header`："HTTPレスポンスヘッダー設定"を表します。<br><br><br>注意<br><br>マッチング条件リスト内の条件の`Object`が`response_header`または`http_code`の場合、アクションリストには`Action`が`respond_header`のアクションを1つだけ含めることができます。 |`response_header` |
|Stage |String |いいえ |このパラメータは`Action`の実行ステージを表します。設定する必要はありません。APIリクエストを送信する際、CDNは自動的にこのパラメータ値を設定します。このパラメータには以下の値があります：<br><br><br>* `client_request`：CDNがユーザーリクエストを受信するステージを表します。<br><br>* `cache`：CDNがオリジンサーバーからのレスポンスをキャッシュするステージを表します。<br><br>* `origin_request`：CDNがファイルをオリジンサーバーからリクエストするステージを表します。<br><br>* `client_response`：CDNがユーザーリクエストにレスポンスするステージを表します。<br><br><br>**設定説明**<br><br><br>* `Action`が`redirect_request`、`redirect_protocol`、`allow_access`、`download_speed_limit`、`request_header`、または`deny_access`の場合、CDNはこのパラメータ値を`client_request`に設定します。<br><br>* `Action`が`cache_key`、`compression`、`video_drag`、または`cache_time`の場合、CDNはこのパラメータ値を`cache`に設定します。<br><br>* `Action`が`origin_range`、`origin_follow`、`origin_tcp_timeout`、または`origin_http_timeout`の場合、CDNはこのパラメータ値を`origin_request`に設定します。<br><br>* `Action`が`response_header`の場合、CDNはこのパラメータ値を`client_response`に設定します。 |`client_response` |
|Phase |Integer |いいえ |このパラメータは`Stage`に対応し、設定する必要はありません。APIリクエストを送信する際、CDNは自動的にこのパラメータ値を設定します。<br><br><br>* `Stage`が`client_request`の場合、CDNはこのパラメータ値を`1`に設定します。<br><br>* `Stage`が`cache`の場合、CDNはこのパラメータ値を`5`に設定します。<br><br>* `Stage`が`origin_request`の場合、CDNはこのパラメータ値を`2`に設定します。<br><br>* `Stage`が`client_response`の場合、CDNはこのパラメータ値を`6`に設定します。 |`6` |
|Module |Integer |いいえ |このパラメータは`Stage`に対応し、設定する必要はありません。APIリクエストを送信する際、CDNは自動的にこのパラメータ値を設定します。<br><br><br>* `Stage`が`client_request`の場合、CDNはこのパラメータ値を`1`に設定します。<br><br>* `Stage`が`cache`の場合、CDNはこのパラメータ値を`2`に設定します。<br><br>* `Stage`が`origin_request`の場合、CDNはこのパラメータ値を`2`に設定します。<br><br>* `Stage`が`client_response`の場合、CDNはこのパラメータ値を`1`に設定します。 |`1` |
|Groups |Object[] |いいえ |`Action`に対応するCDN機能設定を表し、`Dimension`パラメータと`GroupParameters`構造体を含みます。<br><br><br>* `Dimension`パラメータは設定対象を表します。一部のCDN機能には複数の設定対象が含まれます。<br><br>* `GroupParameters`構造体は`Dimension`に対応する設定を含みます。一部の設定では異なる値が異なる設定組み合わせを生成するため、`GroupParameters`は設定グループを表します。例えば、"クライアントリクエストヘッダー設定"では、リクエストヘッダーの設定と削除を実行できます。これらの操作は異なる設定組み合わせを生成し、それぞれの設定グループで定義されます。また、`GroupParameters`について、各設定グループは1つの`Parameters`構造体を含みます。`Parameters`構造体はパラメータリストであり、各パラメータは1つの具体的な設定を表します。<br><br><br>[CDN機能のパラメータ設定](https://docs.byteplus.com/en/docs/18/63603#cdn-%E6%A9%9F%E8%83%BD%E3%81%AE%E3%83%91%E3%83%A9%E3%83%A1%E3%83%BC%E3%82%BF%E8%A8%AD%E5%AE%9A)を参照してください。 | |
|Dimension |String |いいえ |設定対象を表します。 |`response_header` |
|GroupParameters |Object[] |いいえ |`Dimension` に対応する設定を示します。 | |
|Parameters |Object[] |はい |パラメータリストを示します。 | |
|Name |String |はい |リスト内の1つのパラメータ名を示します。 |`action` |
|Values |String[] |はい |そのパラメータの値を示します。 | |
|Condition |Object |はい |IF式でのマッチング条件定義を示します。 | |
|IsGroup |Boolean |はい |このパラメータ値は `true` でなければなりません。 |`true` |
|Connective |String |はい |このパラメータ値は `and` でなければなりません。 |`and` |
|ConditionGroups |Object[] |はい |条件グループリストを示します。 | |
|IsGroup |Boolean |はい |各リスト項目が条件グループであるかどうかを示します。このパラメータ値は `true` でなければならず、各リスト項目が条件グループであることを示します。 |`true` |
|Connective |String |はい |条件グループ間の論理関係を示します。このパラメータには以下の値があります：<br><br><br>* `and`：関係が `AND` であることを示します。<br><br>* `or`：関係が `OR` であることを示します。<br><br><br>このパラメータのデフォルト値は `and` です。 |`and` |
|ConditionGroups |Object[] |はい |条件グループ内のマッチング条件リストを示します。 | |
|IsGroup |Boolean |はい |そのマッチング条件が条件グループであるかどうかを示します。このパラメータ値は `false` でなければなりません。ルールエンジンは条件グループのネストをサポートしていません。 |`false` |
|Condition |Object |はい |リスト内の1つのマッチング条件の定義を示します。各マッチング条件には以下が含まれます：<br><br><br>* `Object`：マッチングオブジェクトを示します。<br><br>* `Operator`：マッチング演算子を示します。<br><br>* `Value`：マッチング値リストを示します。`Operator` が `exist` または `not_exist` でない限り、各マッチング条件でマッチング値リストを指定する必要があります。<br><br>* `IgnoreCase`：マッチング値で大文字小文字を区別するかどうかを示します。マッチング値が文字列の場合にのみ適用されます。<br><br>* `TimeZone`：タイムゾーンを示し、`Object` が `request_time` の場合にのみ適用されます。<br><br>* `Name`：パラメータ名を示し、`Object` が `query_string`、`request_header`、または `response_header` の場合に適用されます。また、`Object` が `request_time` の場合、`Name` は時間範囲の種類を示します。<br><br><br>異なるObjectで使用できるOperator、およびIgnoreCaseとTimeZoneの適用可否については、[マッチング条件リスト](https://docs.byteplus.com/en/docs/18/63603#%E5%8C%B9%E9%85%8D%E6%9D%A1%E4%BB%B6%E5%88%97%E8%A1%A8)を参照してください。 | |
|Object |String |はい |マッチングオブジェクトを示します。このパラメータには以下の値があります：<br><br><br>* `always`：すべてのリクエストを示します。<br><br>* `path`：リクエストパスを示し、クエリ文字列は含まれません。<br><br>* `path_and_param`：リクエストパスとクエリ文字列を示します。<br><br>* `url`：完全なリクエストURLを示します。<br><br>* `query_string`：リクエストURL内のクエリ文字列を示します。<br><br>* `http_referer`：リクエスト内のRefererヘッダーを示します。<br><br>* `client_ip`：リクエストを送信するクライアントのIPアドレスを示します。<br><br>* `http_origin`：リクエスト内のOriginヘッダーを示します。<br><br>* `http_ua`：リクエスト内のUser\-Agentヘッダーを示します。<br><br>* `request_header`：Origin、Referer、およびUser\-Agent以外のリクエスト内の特定のヘッダーを示します。<br><br>* `client_area`：クライアントのIPアドレスが由来する国または地域を示します。<br><br>* `http_method`：リクエストで使用されるメソッドを示します。<br><br>* `request_time`：CDNがユーザーリクエストを受信した時刻を示します。<br><br>* `protocol`：リクエストで使用されるプロトコルを示します。<br><br>* `response_header`：オリジン応答内の特定のヘッダーを示します。<br><br>* `http_code`：オリジン応答内のステータスコードを示します。 |`always` |
|Operator |String |はい |マッチング演算子を示します。このパラメータには以下の値があります：<br><br><br>* `prefix_match`：指定されたプレフィックスにマッチすることを示します。<br><br>* `prefix_not_match`：指定されたプレフィックスにマッチしないことを示します。<br><br>* `suffix_match`：指定されたサフィックスにマッチすることを示します。<br><br>* `suffix_not_match`：指定されたサフィックスにマッチしないことを示します。<br><br>* `match`：指定されたオブジェクトにマッチすることを示します。<br><br>* `not_match`：指定されたオブジェクトにマッチしないことを示します。<br><br>* `regex_match`：指定された正規表現にマッチすることを示します。<br><br>* `regex_not_match`：指定された正規表現にマッチしないことを示します。<br><br>* `equal`：指定された値と同じであることを示します。<br><br>* `not_equal`：指定された値と異なることを示します。<br><br>* `exist`：指定されたオブジェクトが存在することを示します。<br><br>* `not_exist`：指定されたオブジェクトが存在しないことを示します。 |`suffix_match` |
|IgnoreCase |Boolean |はい |`Value` で大文字小文字を区別するかどうかを示します。 |`true` |
|Value |String[] |はい |マッチング値リストを示します。ここでは、`Object` がそれぞれ `request_time`、`client_area`、`http_method`、`protocol` の場合に `Value` をどのように設定するかを説明します。<br><br>`Object` が `path` であり、`Operator` が `suffix_match` または `suffix_not_match` の場合、`Value` で指定するサフィックスはピリオド（.）で始める必要はありません。例：`["png","gif"]`。<br><br>`Object` が `url` の場合、`Value` で指定するサフィックスはピリオド（.）で始める必要はありません。例：`["png","gif"]`。<br><br>`Object` が `request_time` の場合：<br><br><br>* `Name` が `weekday` の場合、`Value` には以下の1つまたは複数の値を含めることができます：<br><br>   * `mon`、`tue`、`wed`、`thur`、`fri`、`sat`、`sun`。<br><br>* `Name` が `period` の場合、`Value` には秒単位までの時間帯を指定する必要があります。時間帯の例：`["2025-05-07 14:21:21", "2025-06-13 14:21:24"]`<br><br>* `Name` が `everyday` の場合：`Value` には秒単位までの時間帯を指定する必要があります。時間帯の例：`["02:02:02","06:04:04"]`<br><br><br>`Object` が `client_area` の場合、`Value` には最大30の国または地域のAlpha\-3コードを含めることができます。例えば `["PNG","FSM","FSM"]` です。[DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp_jp)を呼び出して、指定可能な国と地域のAlpha\-3コードを取得できます。`DescribeCdnRegionAndIsp`を呼び出す際には、リクエスト本文で`Area`を`Global`に設定してください。APIのレスポンス本文では、`Regions`構造体にこれらの国と地域の名前と対応するAlpha\-3コードが含まれています。<br><br>`Object` が `http_method` の場合、`Value` には以下の1つまたは複数の値を含めることができます：`post`、`head`、`get`、`put`、`options`、`delete`、`connect`、`patch`。<br><br>`Object` が `protocol` の場合、`Value` には以下のいずれかの値を含めることができます：`http`、`https`。 | |
|Name |String |いいえ |* `Object` が `request_header`、`response_header`、または `query_string` の場合、このパラメータは指定するヘッダーまたはクエリパラメータを示します。<br><br>* `Object` が `request_time` の場合、このパラメータには以下の値があります：<br><br>   * `weekday`：毎週の固定曜日を示します。<br><br>   * `period`：固定時間帯を示します。<br><br>   * `everyday`：毎日の固定時間帯を示します。 |`myparam` |
|TimeZone |String |いいえ |`Object` が `request_time` の場合、このパラメータはリクエスト時刻に対応するタイムゾーンを示します。現在、タイムゾーンとして UTC+08:00 のみを指定でき、対応するパラメータ値は `+0800` です。 |`+0800` |
|ElseBlock |Object |はい |ルール内のELSE式を示し、`Actions` と `SubRules` の2つの構造体を含みます。<br><br>ユーザーリクエストが `IfBlock` 内の `Condition` のマッチング条件を満たさない場合、CDNは最初に `ElseBlock` 内の `Actions` の操作を実行し、その後 `ElseBlock` 内の `SubRules` のサブルールを処理します。 | |
|SubRules |Object[] |いいえ |`ElseBlock` 式内のサブルールリストを示し、意味および含まれるパラメータは親ルールの `IfBlock` 内の `SubRules` 構造体と同じです。リストには最大10のサブルールを含めることができます。 | |
|Desc |String |いいえ |サブルールの説明を示します。 |`规则名称` |
|IfBlock |Object |はい |サブルール内のIF式を示し、意味および含まれるパラメータは親ルールの `IfBlock` と同じです。ただし、サブルールではサブルールをネストできないことに注意してください。そのため、サブルール内の `IfBlock` の `SubRules` 構造体の値は空（`[]`）でなければなりません。 | |
|SubRules |String[] |いいえ | | |
|Actions |Object[] |はい | | |
|Action |String |いいえ | |`response_header` |
|Stage |String |いいえ | |`client_response` |
|Phase |Integer |いいえ | |`6` |
|Module |Integer |いいえ | |`1` |
|Groups |Object[] |いいえ | | |
|Dimension |String |いいえ | |`response_header` |
|GroupParameters |Object[] |いいえ | | |
|Parameters |Object[] |いいえ | | |
|Name |String |はい | |`action` |
|Values |String[] |はい | | |
|Condition |Object |はい | | |
|IsGroup |Boolean |はい | |`true` |
|Connective |String |はい | |`and` |
|ConditionGroups |Object[] |はい | | |
|IsGroup |Boolean |いいえ | |`true` |
|Connective |String |いいえ | |`and` |
|ConditionGroups |Object[] |いいえ | | |
|IsGroup |Boolean |いいえ | |`false` |
|Condition |Object |いいえ | | |
|Object |String |はい | |`http_referer` |
|Operator |String |はい | |`exist` |
|ElseBlock |Object |いいえ |サブルール内のELSE式を示し、意味および含まれるパラメータは親ルールの `ElseBlock` と同じです。 | |
|SubRules |String[] |いいえ | | |
|Actions |Object[] |はい | | |
|Action |String |いいえ | |`response_header` |
|Stage |String |いいえ | |`client_response` |
|Phase |Integer |いいえ | |`6` |
|Module |Integer |いいえ | |`1` |
|Groups |Object[] |いいえ | | |
|Dimension |String |いいえ | |`response_header` |
|GroupParameters |Object[] |いいえ | | |
|Parameters |Object[] |いいえ | | |
|Name |String |はい | |`action` |
|Values |String[] |はい | | |
|Actions |Object[] |いいえ |`ElseBlock` 式内の `Actions` 構造体を示し、意味および含まれるパラメータは `IfBlock` の `Actions` と同じです。 | |
|Action |String |いいえ | |`response_header` |
|Stage |String |いいえ | |`client_response` |
|Phase |Integer |いいえ | |`6` |
|Module |Integer |いいえ | |`1` |
|Groups |Object[] |いいえ | | |
|Dimension |String |いいえ | |`response_header` |
|GroupParameters |Object[] |いいえ | | |
|Parameters |Object[] |いいえ | | |
|Name |String |はい | |`action` |
|Values |String[] |はい | | |
|TemplateVersion |String |いいえ |更新するポリシーバージョンを示します。<br><br><br>* 更新するパラメータが `Title` または `Message` の場合、このパラメータを指定する必要はありません。これらの2つのパラメータはポリシーバージョンとは関係ありません。<br><br>* 更新するパラメータが `Title` と `Message` ではない場合、このパラメータを `draft` として指定する必要があります。ドキュメントの冒頭の説明を参照してください。 |`draft` |
|Title |String |いいえ |新しいポリシー名を示し、長さは100文字を超えてはなりません。 |`new-title` |


<span id="マッチング条件リスト"></span>
## マッチング条件リスト


| **オブジェクト**  | **オペレーター（利用可能）**  |**IgnoreCase** |**TimeZone** |
|---|---|---|---|
|always |該当なし |該当なし |該当なし |
|path |equal<br><br>not_equal<br><br>prefix_match<br><br>prefix_not_match<br><br>suffix_match<br><br>suffix_not_match<br><br>regex_match<br><br>regex_not_match |適用 ||
|path_and_param ||||
|url ||||
|query_string |regex_match<br><br>regex_not_match<br><br>equal<br><br>not_equal<br><br>exist<br><br>not_exist |||
|http_referer ||||
|http_origin ||||
|http_ua ||||
|request_header ||||
|response_header ||||
|client_area |match<br><br>not_match |該当なし ||
|client_ip ||||
|http_code ||||
|http_method |equal<br><br>not_equal |||
|protocol ||||
|request_time |match<br><br>not_match ||適用 |
|||||


<span id="cdn-機能のパラメータ設定"></span>
## CDN 機能のパラメータ設定


| **アクション**  | **ディメンション**  |**GroupParameters \> Parameters \> Name** | **パラメータ説明** |
|---|---|---|---|
|redirect_request |redirect_request |source_path |オリジンサーバー上のファイルの元のパスを表します。 |
| | |status_code |リダイレクトステータスコードを表します。このパラメータには以下の値があります：<br><br><br>* `301`：恒久的リダイレクトを表します。<br><br>* `302`：一時的リダイレクトを表します。 |
| | |protocol |リダイレクトリクエストで使用されるプロトコルを表します。このパラメータには以下の値があります：<br><br><br>* `followclient`：元のリクエストと同じプロトコルを使用します。<br><br>* `http`<br><br>* `https` |
| | |target_host |リダイレクトパスが属するサイトのドメイン名またはIPアドレスを表します。 |
| | |target_path |リダイレクトパスを表します。 |
| | |target_query_action |元のリクエストURLのクエリパラメータの処理方法を表します。このパラメータには以下の値があります：<br><br><br>* `include_all`：リダイレクトURLに元のリクエストURLのすべてのクエリパラメータが含まれます。<br><br>* `exclude_all`：リダイレクトURLにクエリパラメータが含まれません。<br><br>* `include_part`：リダイレクトURLに指定されたクエリパラメータのみが含まれます。<br><br>* `exclude_part`：リダイレクトURLに指定されたクエリパラメータ以外のすべてのクエリパラメータが含まれます。 |
| | |target_query_values |`target_query_action`が`include_part`または`exclude_part`の場合、`target_query_values`は指定するクエリパラメータを表します。 |
|allow_access |allow_access | |CDNがユーザーリクエストを拒否する際のレスポンスステータスコードを表します。 |
|download_speed_limit |download_speed_limit |rate |単一リクエストのデータ転送速度上限を表し、1024進数を使用します。 |
| | |rate_unit |`rate`の単位を表します。このパラメータには以下の値があります：<br><br><br>* `KB/s`<br><br>* `B/s`<br><br>* `MB/s` |
| | |after_size |データ量を表します。単一リクエストのデータ転送量がこの値に達した時点で、CDNはそのリクエストのデータ転送速度の監視を開始します。 |
| | |after_size_unit |`after_size`の単位を表します。このパラメータには以下の値があります：<br><br><br>* `KB`<br><br>* `B`<br><br>* `MB` |
|request_header |request_header |action |`header_name`に対して実行する操作を表します。このパラメータには以下の値があります：<br><br><br>* `set`：`header_name`の値を設定します。`header_name`が存在しない場合、CDNはこのヘッダーを追加します。<br><br>* `delete`：`header_name`を削除します。<br><br><br>複数のヘッダーを削除または設定する必要がある場合、各ヘッダーの操作設定を個別の`GroupParameter`で定義する必要があります。 |
| | |header_name |リクエストヘッダーの名前を表します。 |
| | |header_value |`action`が`set`の場合、`header_value`は`header_name`に設定する値を表します。 |
|deny_access |deny_access |status_code |CDNが拒否するリクエストを表します。 |
|cache_key |query_string |query_action |CDNがリクエストURLのクエリパラメータを処理する方法を表します。このパラメータには以下の値があります：<br><br><br>* `exclude_part`：指定されたクエリパラメータを除く、リクエストURLのすべてのクエリパラメータがキャッシュキーに追加されます。<br><br>* `include_part`：指定されたクエリパラメータのみがキャッシュキーに追加されます。<br><br>* `include_all`：すべてのクエリパラメータがキャッシュキーに追加されます。<br><br>* `exclude_all`：クエリパラメータはキャッシュキーに追加されません。<br><br><br>1つまたは複数の処理方法を同時に指定できます。各処理方法の設定は独立した`GroupParameter`で定義する必要があります。 |
| | |query_names |`query_action`が`exclude_part`または`include_part`の場合、このパラメータは指定するクエリパラメータのリストを表します。 |
| | |ignore_case |キャッシュキー内のクエリパラメータ値が大文字小文字を区別するかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：大文字小文字を区別しません。<br><br>* `false`：大文字小文字を区別します。 |
| |request_header |header_names |キャッシュキーに追加する必要があるヘッダーリストを表します。<br><br>&nbsp;<br><br>デフォルトでは、キャッシュキーにはユーザーリクエストのヘッダーは含まれません。 |
| | |ignore_case |キャッシュキー内のヘッダー値が大文字小文字を区別するかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：大文字小文字を区別しません。<br><br>* `false`：大文字小文字を区別します。 |
| |cookie |cookie_action |CDNがリクエスト内のcookieを処理する方法を表します。このパラメータには以下の値があります：<br><br><br>* `exclude_part`：指定されたcookieを除く、リクエスト内のすべてのcookieがキャッシュキーに追加されます。<br><br>* `include_part`：指定されたcookieのみがキャッシュキーに追加されます。<br><br>* `include_all`：すべてのcookieがキャッシュキーに追加されます。<br><br>* `exclude_all`：cookieはキャッシュキーに追加されません。<br><br><br>1つまたは複数の処理方法を同時に指定できます。各処理方法の設定は独立した`GroupParameter`で定義する必要があります。 |
| | |cookie_names |指定するcookieのリストを表します。リストにはこれらのcookieのkeyが含まれます。<br><br>&nbsp;<br><br>デフォルトでは、キャッシュキーにはユーザーリクエストのcookieは含まれません。 |
| | |ignore_case |キャッシュキーに追加されるcookie値が大文字小文字を区別するかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：大文字小文字を区別しません。<br><br>* `false`：大文字小文字を区別します。 |
| |request_path |source_path |書き換える必要がある元のパスを表します。書き換えられたパスはキャッシュキーに追加されます。 |
| | |target_path |書き換えられたパスを表します。このパスはキャッシュキーに追加されます。 |
| |path_ignore_case |ignore_case |キャッシュキー内のパスが大文字小文字を区別するかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：大文字小文字を区別しません。<br><br>* `false`：大文字小文字を区別します。 |
|compression |compression |methods |CDNが使用する圧縮アルゴリズムのリストを表します。このパラメータには以下の値があります：<br><br><br>* `br`：Brotli圧縮アルゴリズムを表します。<br><br>* `gzip`：Gzip圧縮アルゴリズムを表します。 |
| | |min_file_size |圧縮条件を満たすファイルの最小サイズを表します。リクエストファイルのサイズがこの値より小さい場合、CDNはファイルを圧縮しません。<br><br>&nbsp;<br><br>このパラメータのデフォルト値は`0`です。 |
| | |min_file_size_unit |`min_file_size`の単位を表します。このパラメータには以下の値があります：<br><br><br>* `KB`<br><br>* `MB` |
| | |format |CDNがユーザーリクエストのContent\-Typeヘッダーに基づいてリクエストファイルを圧縮する方法を表します。このパラメータには以下の値があります：<br><br><br>* `default`：CDNのデフォルト動作を使用します。<br><br>* `customize`：指定されたContent\-Type値を表します。<br><br><br>**CDNのデフォルト動作**<br><br>デフォルトでは、以下のContent\-Type値を含むユーザーリクエストに対して、CDNはリクエストファイルを圧縮します：<br><br><br>* text/html<br><br>* text/plain<br><br>* text/xml<br><br>* text/css<br><br>* application/javascript<br><br>* application/x\-javascript<br><br>* application/rss+xml<br><br>* application/json<br><br>* image/tiff<br><br>* text/javascript<br><br>* image/svg+xml<br><br>* application/xml<br><br>* text/plain; charset=utf\-8 |
| | |content_types |指定されたContent\-Type値のリストを表します。 |
|video_drag |video_drag |switch |この機能を有効にするかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にします。<br><br>* `false`：この機能を無効にします。 |
|cache_time |cache_time |ttl |キャッシュの存続期間を表します。 |
| | |ttl_unit |`ttl`の単位を表します。このパラメータには以下の値があります：<br><br><br>* `sec`：秒を表します。<br><br>* `min`：分を表します。<br><br>* `hour`：時間を表します。<br><br>* `day`：日を表します。 |
| | |cache_policy |キャッシュポリシーを表します。このパラメータには以下の値があります：<br><br><br>* `default`："ルールに従う"を表します。<br><br>* `origin_first`："オリジンサーバーに従う"を表します。<br><br><br>[キャッシュルール](https://docs.byteplus.com/en/docs/byteplus-cdn/cdn-cache-rules-jp)を参照してください。 |
| | |force_cache |"強制キャッシュ"を有効にするかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`："強制キャッシュ"を有効にします。<br><br>* `false`："強制キャッシュ"を有効にしません。 |
| | |replenish |"補充キャッシュ"を有効にするかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`："補充キャッシュ"を有効にします。<br><br>* `false`："補充キャッシュ"を有効にしません。 |
|origin_range |origin_range |switch |この機能を有効にするかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にします。<br><br>* `false`：この機能を無効にします。 |
|origin_follow |origin_follow |switch |この機能を有効にするかどうかを表します。このパラメータには以下の値があります：<br><br><br>* `true`：この機能を有効にします。<br><br>* `false`：この機能を無効にします。 |
|origin_tcp_timeout |origin_tcp_timeout |connect_timeout |オリジンリクエストに対して、このパラメータはTCP接続のタイムアウト時間を表し、値の範囲は2\-60で、デフォルト値は`2`です。 |
| | |connect_timeout_unit |`connect_timeout`の単位を表します。このパラメータの値は`sec`のみで、秒を表します。 |
|origin_http_timeout |origin_http_timeout |read_timeout |オリジンリクエストに対して、このパラメータはHTTPリクエストのタイムアウト時間を表し、値の範囲は2\-60で、デフォルト値は`60`です。 |
| | |read_timeout_unit |`read_timeout_unit`の単位を表します。このパラメータの値は`sec`のみで、秒を表します。 |
|response_header |response_header |action |`header_name`に対して実行する操作を表します。このパラメータには以下の値があります：<br><br><br>* `set`：`header_name`の値を設定します。`header_name`が存在しない場合、CDNはこのヘッダーを追加します。<br><br>* `delete`：`header_name`を削除します。<br><br><br>複数のヘッダーを削除または設定する必要がある場合、各ヘッダーの操作設定を個別の`GroupParameter`で定義する必要があります。 |
| | |header_name |レスポンスヘッダーの名前を表します。 |
| | |header_value |`action`が`set`の場合、`header_value`は`header_name`に設定する値を表します。 |
|redirect_protocol |redirect_protocol |status_code |プロトコルリダイレクトのステータスコードを表します。このパラメータには以下の値があります：<br><br><br>* `301`：恒久的リダイレクトを表します。<br><br>* `302`：一時的リダイレクトを表します。 |
| | |protocol |リダイレクト先のプロトコルを表します。このパラメータには以下の値があります：<br><br><br>* `https`<br><br>* `http` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ

<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

<span id="例-1"></span>
#### 例 1

この例では、`Condition` の設定に焦点を当てています。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">この例はそのまま使用できません。まず <code>Rule</code> 構造体のパラメータを設定する必要があります。<code>Rule</code> パラメータの説明を参照してください。</div>


```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplateDoc&Version=2021-03-01
{
    "Title": "rulesengine-conditions",
    "Message": "desc",
    "Project": "default",
    "Rule": [
        {
            "Desc": "myDesc",
            "IfBlock": {
                "SubRules": [
                    {
                        "Desc": "Sub-rule1",
                        "IfBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "set"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader2"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_value",
                                                            "Values": [
                                                                "myheadervalue"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "Condition": {
                                "IsGroup": true,
                                "Connective": "and",
                                "ConditionGroups": [
                                    {
                                        "IsGroup": true,
                                        "Connective": "and",
                                        "ConditionGroups": [
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "always"
                                                }
                                            },
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "path",
                                                    "Operator": "suffix_match",
                                                    "IgnoreCase": true,
                                                    "Value": [
                                                        "param=value"
                                                    ]
                                                }
                                            }
                                        ]
                                    }
                                ]
                            }
                        },
                        "ElseBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "delete"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader3"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "Actions": [
                    {
                        "Action": "response_header",
                        "Stage": "client_response",
                        "Phase": 6,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "response_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "set"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            },
                                            {
                                                "Name": "header_value",
                                                "Values": [
                                                    "myheadervalue"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader1"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "Condition": {
                    "IsGroup": true,
                    "Connective": "and",
                    "ConditionGroups": [
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "always"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "suffix_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "jpg",
                                            "png"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path_and_param",
                                        "Operator": "prefix_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/docs1/",
                                            "/docs2/"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "url",
                                        "Operator": "equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "https://www.example.com/abc/file"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "query_string",
                                        "Name": "myparam",
                                        "Operator": "equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "myvalue",
                                            "myvalue2"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_referer",
                                        "Operator": "not_equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "myreferer1",
                                            "myreferere2"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "match",
                                        "Value": [
                                            "1.1.1.1",
                                            "2.2.2.2"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_origin",
                                        "Operator": "exist"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_ua",
                                        "Operator": "not_exist"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_header",
                                        "Name": "myhttpheader",
                                        "Operator": "regex_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "^abc$",
                                            "^cde$"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "client_area",
                                        "Operator": "not_match",
                                        "Value": [
                                            "PNG",
                                            "FSM"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_method",
                                        "Operator": "equal",
                                        "Value": [
                                            "post",
                                            "head",
                                            "get",
                                            "put",
                                            "options",
                                            "delete",
                                            "connect",
                                            "patch"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "everyday",
                                        "Operator": "match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "02:02:02",
                                            "06:04:04"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "weekday",
                                        "Operator": "not_match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "mon",
                                            "tue",
                                            "wed",
                                            "thur",
                                            "fri",
                                            "sat",
                                            "sun"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "period",
                                        "Operator": "not_match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "2025-05-07 14:21:21",
                                            "2025-06-13 14:21:24"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "protocol",
                                        "Operator": "equal",
                                        "Value": [
                                            "http"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "response_header",
                                        "Name": "myresponseheader",
                                        "Operator": "regex_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "^resheader1$",
                                            "^resheader2$"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_code",
                                        "Operator": "match",
                                        "Value": [
                                            "400",
                                            "500"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "prefix_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/abc/"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "suffix_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/def/"
                                        ]
                                    }
                                }
                            ]
                        }
                    ]
                }
            },
            "ElseBlock": {
                "SubRules": [
                    {
                        "Desc": "规则名称",
                        "IfBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "set"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader6"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_value",
                                                            "Values": [
                                                                "1111"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "Condition": {
                                "IsGroup": true,
                                "Connective": "and",
                                "ConditionGroups": [
                                    {
                                        "IsGroup": true,
                                        "Connective": "and",
                                        "ConditionGroups": [
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "http_referer",
                                                    "Operator": "exist"
                                                }
                                            }
                                        ]
                                    }
                                ]
                            }
                        },
                        "ElseBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Stage": "client_response",
                                    "Phase": 6,
                                    "Module": 1,
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "delete"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader7"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "Actions": [
                    {
                        "Action": "response_header",
                        "Stage": "client_response",
                        "Phase": 6,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "response_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "MyHeader"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ],
    "TemplateId": "tpl-r5lx4gr",
    "Status": "editing",
    "CreateTime": 1748240796,
    "UpdateTime": 1748240816,
    "TemplateVersion": "draft"
}
```


<span id="例-2"></span>
#### 例 2

この例では、`Actions` の設定に焦点を当てています。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">この例はそのまま使用できません。まず <code>Rule</code> 構造体のパラメータを設定する必要があります。<code>Rule</code> パラメータの説明を参照してください。</div>


```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplateDoc&Version=2021-03-01
{
    "Title": "rulesengine-actions",
    "Message": "desc",
    "Project": "default",
    "Rule": [
        {
            "Desc": "myDesc",
            "IfBlock": {
                "SubRules": [],
                "Actions": [
                    {
                        "Action": "redirect_request",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "redirect_request",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "source_path",
                                                "Values": [
                                                    "^/docs/file1$"
                                                ]
                                            },
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "301"
                                                ]
                                            },
                                            {
                                                "Name": "protocol",
                                                "Values": [
                                                    "follow_client"
                                                ]
                                            },
                                            {
                                                "Name": "target_host",
                                                "Values": [
                                                    "www.example.com"
                                                ]
                                            },
                                            {
                                                "Name": "target_path",
                                                "Values": [
                                                    "^/cos1/file2$"
                                                ]
                                            },
                                            {
                                                "Name": "target_query_action",
                                                "Values": [
                                                    "include_all"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "allow_access",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "allow_access",
                                "GroupParameters": [
                                    {
                                        "Parameters": []
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "download_speed_limit",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "download_speed_limit",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "rate",
                                                "Values": [
                                                    "100"
                                                ]
                                            },
                                            {
                                                "Name": "rate_unit",
                                                "Values": [
                                                    "B/s"
                                                ]
                                            },
                                            {
                                                "Name": "after_size",
                                                "Values": [
                                                    "15"
                                                ]
                                            },
                                            {
                                                "Name": "after_size_unit",
                                                "Values": [
                                                    "MB"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "request_header",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "request_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "set"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            },
                                            {
                                                "Name": "header_value",
                                                "Values": [
                                                    "myvalue"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "deny_access",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "deny_access",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "465"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "cache_key",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "query_string",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "exclude_part"
                                                ]
                                            },
                                            {
                                                "Name": "query_names",
                                                "Values": [
                                                    "myparam1",
                                                    "myparam2"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "include_part"
                                                ]
                                            },
                                            {
                                                "Name": "query_names",
                                                "Values": [
                                                    "ff"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "include_all"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "exclude_all"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "request_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "header_names",
                                                "Values": [
                                                    "myheader",
                                                    "myheader2"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "request_path",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "source_path",
                                                "Values": [
                                                    "^/path1/$"
                                                ]
                                            },
                                            {
                                                "Name": "target_path",
                                                "Values": [
                                                    "^/path2/$"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "path_ignore_case",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "compression",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "compression",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "methods",
                                                "Values": [
                                                    "gzip",
                                                    "brotli"
                                                ]
                                            },
                                            {
                                                "Name": "min_file_size",
                                                "Values": [
                                                    "563"
                                                ]
                                            },
                                            {
                                                "Name": "min_file_size_unit",
                                                "Values": [
                                                    "KB"
                                                ]
                                            },
                                            {
                                                "Name": "format",
                                                "Values": [
                                                    "default"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "video_drag",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "video_drag",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "cache_time",
                        "Stage": "cache",
                        "Phase": 5,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "cache_time",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "ttl",
                                                "Values": [
                                                    "56"
                                                ]
                                            },
                                            {
                                                "Name": "ttl_unit",
                                                "Values": [
                                                    "day"
                                                ]
                                            },
                                            {
                                                "Name": "cache_policy",
                                                "Values": [
                                                    "origin_first"
                                                ]
                                            },
                                            {
                                                "Name": "replenish",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_range",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_range",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_follow",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_follow",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_tcp_timeout",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_tcp_timeout",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "connect_timeout",
                                                "Values": [
                                                    "56"
                                                ]
                                            },
                                            {
                                                "Name": "connect_timeout_unit",
                                                "Values": [
                                                    "sec"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_http_timeout",
                        "Stage": "origin_request",
                        "Phase": 2,
                        "Module": 2,
                        "Groups": [
                            {
                                "Dimension": "origin_http_timeout",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "read_timeout",
                                                "Values": [
                                                    "58"
                                                ]
                                            },
                                            {
                                                "Name": "read_timeout_unit",
                                                "Values": [
                                                    "sec"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "Condition": {
                    "IsGroup": true,
                    "Connective": "and",
                    "ConditionGroups": [
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "always"
                                    }
                                }
                            ]
                        }
                    ]
                }
            },
            "ElseBlock": {
                "SubRules": [],
                "Actions": [
                    {
                        "Action": "redirect_protocol",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 1,
                        "Groups": [
                            {
                                "Dimension": "redirect_protocol",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "301"
                                                ]
                                            },
                                            {
                                                "Name": "protocol",
                                                "Values": [
                                                    "https"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ],
    "TemplateId": "tpl-rejjo23",
    "Status": "editing",
    "CreateTime": 1748241181,
    "UpdateTime": 1748241181,
    "TemplateVersion": "draft"
}
```


&nbsp;
