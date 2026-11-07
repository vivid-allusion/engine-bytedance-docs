---
title: "DescribeRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_zh-tw"
---

獲取一個規則引擎策略的配置詳情。


* 如果該策略已發布，API 默認返回的是該策略下已發布，也就是狀態為 `running` 的版本配置詳情。

* 如果該策略未發布，API 默認返回的是該策略下狀態為 `draft` 的版本配置詳情。


您也可以指定該策略下的某個版本，獲取該版本的配置詳情。

<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `DescribeRuleEngineTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要查詢的規則引擎策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 獲取您想要查詢的規則引擎策略的 ID。 | |
|TemplateVersion |String |否 |表示該策略下的一個版本，API 返回該版本的配置詳情。<br><br>該參數的默認值如下：<br><br><br>* 如果該策略已發布，該參數的默認值是策略下已發布，也就是狀態為 `running` 的版本。<br><br>* 如果該策略未發布，該參數的默認值為 `draft`。<br><br><br>您可以調用 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw) 獲取該策略下的所有版本。 | |


<span id="回應"></span>
## 回應


|參數 |類型 |說明 |範例 |
|---|---|---|---|
|BoundDomains |Object[] |對於 `TemplateId` 所指定的規則引擎策略，該參數表示與該策略綁定的域名列表。<br><br>如果該規則引擎策略未與任何域名綁定，該參數值為 `null`。 | |
|BoundTime |Long |表示該規則引擎策略與 `Domain` 所指定的域名綁定的時間，格式是 Unix 時間戳。 |`1709174039` |
|Domain |String |表示一個與該規則引擎策略綁定的域名。 |`www.example.com` |
|CreateTime |Long |表示該規則引擎策略的創建時間，格式是 Unix 時間戳。 |`1709173909` |
|Exception |Boolean |表示該規則引擎策略中是否存在特殊配置。如果特殊配置存在，您無法將該策略與域名綁定，請 [提交工單](https://console.byteplus.com/workorder/create)。<br><br>該參數有以下取值：<br><br><br>* `true`：表示存在特殊配置。<br><br>* `false`：表示不存在特殊配置。 |`false` |
|Message |String |表示該規則引擎策略的描述。 |`This is a test` |
|ProdVersion |String |表示該規則引擎策略下已發布，也就是狀態為 `running` 的版本。如果不存在狀態為 `running` 的版本，該參數值為空（""）。 |`P-250414.89520` |
|Project |String |表示該規則引擎策略所屬的項目。 |`default` |
|Rule |String |表示規則的內容。您需要反序列化規則內容以提取規則配置。關於規則配置的描述，參見 [UpdateRuleEngineTemplate](https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-tw) 中 `Rule` 參數的描述。 | |
|Status |String |表示該規則引擎策略的狀態。該參數有以下取值：<br><br><br>* `locked`：表示狀態是 "已發布"。對於已發布的規則引擎策略，您無法修改其配置。<br><br>* `editing`：表示狀態是 "草稿"。 |`locked` |
|TemplateId |String |表示該規則引擎策略的 ID。 |`tpl-sZRpwq` |
|Title |String |表示該規則引擎策略的名稱。 |`NetTVWeb001` |
|Type |String |表示該規則引擎策略的類型。該參數值始終是 `rule`。 |`rule` |
|UpdateTime |Long |表示該規則引擎策略的最近修改時間，格式是 Unix 時間戳。<br><br>如果該規則引擎策略自創建後未被修改，該參數值與 `CreateTime` 的值相同。 |`1709173909` |


<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

```json
POST https://cdn.byteplusapi.com/?Action=DescribeRuleEngineTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft"
}
```


<span id="範例回應"></span>
### 範例回應

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
