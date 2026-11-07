---
title: "DescribeRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_jp"
---

ルールエンジンポリシーの設定詳細を取得します。


* ポリシーが公開されている場合、APIはデフォルトでそのポリシー配下の公開済み（`running`状態）のバージョン設定詳細を返します。

* ポリシーが未公開の場合、APIはデフォルトでそのポリシー配下の`draft`状態のバージョン設定詳細を返します。


ポリシー配下の特定のバージョンを指定して、そのバージョンの設定詳細を取得することもできます。

<span id="使用制限"></span>
## 使用制限

スロットリング制限：1秒あたり最大20個のAPIリクエストを送信できます。

<span id="リクエストの説明"></span>
## リクエストの説明


* リクエストメソッド: POST

* リクエストURL: https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021\-03\-01


<span id="リクエストパラメータ"></span>
## リクエストパラメータ

<span id="クエリパラメータ"></span>
### クエリパラメータ


|パラメータ |データタイプ |必須 |説明 |
|---|---|---|---|
|Action |String |はい |API名。現在のAPI名はDescribeRuleEngineTemplateです。 |
|Version |String |はい |APIバージョン。現在のAPIバージョンは2021\-03\-01です。 |


<span id="要求本文のパラメーター"></span>
### 要求本文のパラメーター


|パラメータ |データタイプ |必須 |説明 |例 |
|---|---|---|---|---|
|TemplateId |String |はい |照会するルールエンジンポリシーのIDを指定します。<br><br>[DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplates_jp)を使用して、照会したいルールエンジンポリシーのIDを取得できます。 |`tpl-sZRpwq` |
|TemplateVersion |String |いいえ |ポリシー配下のバージョンを指定します。APIはこのバージョンの設定詳細を返します。<br><br>このパラメータのデフォルト値は以下の通りです：<br><br><br>* ポリシーが公開されている場合、このパラメータのデフォルト値はポリシー配下の公開済み（`running`状態）のバージョンです。<br><br>* ポリシーが未公開の場合、このパラメータのデフォルト値は`draft`です。<br><br><br>[DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_jp)を呼び出すことで、このポリシー配下のすべてのバージョンを取得できます。 |`P-250414.89520` |


<span id="レスポンスパラメータ"></span>
## レスポンスパラメータ


|パラメータ |データタイプ |説明 |例 |
|---|---|---|---|
|BoundDomains |Object[] |`TemplateId`で指定されたルールエンジンポリシーに対して、このパラメータはそのポリシーにバインドされているドメイン名リストを示します。<br><br>このルールエンジンポリシーがいかなるドメイン名にもバインドされていない場合、このパラメータの値は`null`です。 | |
|BoundTime |Long |ルールエンジンポリシーが`Domain`で指定されたドメイン名にバインドされた時間を示します。形式はUnixタイムスタンプです。 |`1709174039` |
|Domain |String |ルールエンジンポリシーにバインドされているドメイン名を示します。 |`www.example.com` |
|CreateTime |Long |ルールエンジンポリシーの作成時間を示します。形式はUnixタイムスタンプです。 |`1709173909` |
|Exception |Boolean |ルールエンジンポリシーに特殊設定が存在するかどうかを示します。特殊設定が存在する場合、そのポリシーをドメイン名にバインドすることはできません。[チケットを作成](https://console.byteplus.com/workorder/create)してください。<br><br>このパラメータには以下の値があります：<br><br><br>* `true`：特殊設定が存在することを示します。<br><br>* `false`：特殊設定が存在しないことを示します。 |`false` |
|Message |String |ルールエンジンポリシーの説明を示します。 |`This is a test` |
|ProdVersion |String |ルールエンジンポリシー配下の公開済み（`running`状態）のバージョンを示します。`running`状態のバージョンが存在しない場合、このパラメータの値は空（""）です。 |`P-250414.89520` |
|Project |String |ルールエンジンポリシーが所属するプロジェクトを示します。 |`default` |
|Rule |String |ルールの内容を示します。ルールの内容を逆シリアル化して、ルール設定を抽出する必要があります。ルール設定の説明については、[UpdateRuleEngineTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_jp)の`Rule`パラメータの説明を参照してください。 | |
|Status |String |ルールエンジンポリシーの状態を示します。このパラメータには以下の値があります：<br><br><br>* `locked`：状態が"公開済み"であることを示します。公開済みのルールエンジンポリシーでは、その設定を変更することはできません。<br><br>* `editing`：状態が"下書き"であることを示します。 |`locked` |
|TemplateId |String |ルールエンジンポリシーのIDを示します。 |`tpl-sZRpwq` |
|Title |String |ルールエンジンポリシーの名前を示します。 |`NetTVWeb001` |
|Type |String |ルールエンジンポリシーのタイプを示します。このパラメータの値は常に`rule`です。 |`rule` |
|UpdateTime |Long |ルールエンジンポリシーの最新修正時間を示します。形式はUnixタイムスタンプです。<br><br>ルールエンジンポリシーが作成後に修正されていない場合、このパラメータの値は`CreateTime`の値と同じです。 |`1709173909` |


<span id="例"></span>
## 例

<span id="リクエスト例"></span>
### リクエスト例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft"
}
```


<span id="レスポンス例"></span>
### レスポンス例

```json
{
    "ResponseMetadata": {
        "RequestId": "2025053003420680999F0B12D54B0FB5C8",
        "Action": "DescribeRuleEngineTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "BoundDomains": null,
        "CreateTime": 1748241181,
        "Exception": false,
        "Message": "test",
        "ProdVersion": "",
        "Project": "default",
        "Rule": "{\"IfBlock\":{\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Connective\":\"and\",\"Condition\":{\"Object\":\"always\"}}]}]},\"Actions\":[{\"Action\":\"redirect_request\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"redirect_request\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"source_path\",\"Values\":[\"^/docs/file1$\"]},{\"Name\":\"status_code\",\"Values\":[\"301\"]},{\"Name\":\"protocol\",\"Values\":[\"follow_client\"]},{\"Name\":\"target_host\",\"Values\":[\"www.example.com\"]},{\"Name\":\"target_path\",\"Values\":[\"^/cos1/file2$\"]},{\"Name\":\"target_query_action\",\"Values\":[\"include_all\"]}]}]}]},{\"Action\":\"allow_access\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"allow_access\",\"GroupParameters\":[{}]}]},{\"Action\":\"download_speed_limit\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"download_speed_limit\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"rate\",\"Values\":[\"100\"]},{\"Name\":\"rate_unit\",\"Values\":[\"B/s\"]},{\"Name\":\"after_size\",\"Values\":[\"15\"]},{\"Name\":\"after_size_unit\",\"Values\":[\"MB\"]}]}]}]},{\"Action\":\"request_header\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"request_header\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"action\",\"Values\":[\"set\"]},{\"Name\":\"header_name\",\"Values\":[\"myheader\"]},{\"Name\":\"header_value\",\"Values\":[\"myvalue\"]}]},{\"Parameters\":[{\"Name\":\"action\",\"Values\":[\"delete\"]},{\"Name\":\"header_name\",\"Values\":[\"myheader\"]}]}]}]},{\"Action\":\"deny_access\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"deny_access\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"status_code\",\"Values\":[\"465\"]}]}]}]},{\"Action\":\"cache_key\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"query_string\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"exclude_part\"]},{\"Name\":\"query_names\",\"Values\":[\"myparam1\",\"myparam2\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"include_part\"]},{\"Name\":\"query_names\",\"Values\":[\"ff\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"include_all\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]},{\"Parameters\":[{\"Name\":\"query_action\",\"Values\":[\"exclude_all\"]}]}]},{\"Dimension\":\"request_header\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"header_names\",\"Values\":[\"myheader\",\"myheader2\"]},{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]}]},{\"Dimension\":\"request_path\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"source_path\",\"Values\":[\"^/path1/$\"]},{\"Name\":\"target_path\",\"Values\":[\"^/path2/$\"]}]}]},{\"Dimension\":\"path_ignore_case\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"ignore_case\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"compression\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"compression\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"methods\",\"Values\":[\"gzip\",\"brotli\"]},{\"Name\":\"min_file_size\",\"Values\":[\"563\"]},{\"Name\":\"min_file_size_unit\",\"Values\":[\"KB\"]},{\"Name\":\"format\",\"Values\":[\"default\"]}]}]}]},{\"Action\":\"video_drag\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"video_drag\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"cache_time\",\"Stage\":\"cache\",\"Phase\":5,\"Module\":2,\"Groups\":[{\"Dimension\":\"cache_time\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"ttl\",\"Values\":[\"56\"]},{\"Name\":\"ttl_unit\",\"Values\":[\"day\"]},{\"Name\":\"cache_policy\",\"Values\":[\"origin_first\"]},{\"Name\":\"replenish\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_range\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_range\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_follow\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_follow\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"switch\",\"Values\":[\"true\"]}]}]}]},{\"Action\":\"origin_tcp_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"56\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]},{\"Action\":\"origin_http_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_http_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"read_timeout\",\"Values\":[\"58\"]},{\"Name\":\"read_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}]},\"ElseBlock\":{\"Actions\":[{\"Action\":\"redirect_protocol\",\"Stage\":\"client_request\",\"Phase\":1,\"Module\":1,\"Groups\":[{\"Dimension\":\"redirect_protocol\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"status_code\",\"Values\":[\"301\"]},{\"Name\":\"protocol\",\"Values\":[\"https\"]}]}]}]}]}}",
        "Status": "editing",
        "TemplateId": "tpl-rejjo23",
        "Title": "rules-actions",
        "Type": "rule",
        "UpdateTime": 1748241181
    }
}
```


&nbsp;
