---
title: "UpdateRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-tw"
---

更新規則引擎範本中的配置。

除了 `Title` 和 `Message`，其他參數的更新需要您在呼叫 `UpdateRuleEngineTemplate` 時指定 `TemplateVersion` 為 `draft`。也就是說，待更新的策略已存在 Draft 版本。要確保待更新的策略已存在 Draft 版本，參照以下步驟：


1. 對該策略呼叫 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-tw) API。

2. 在 API 返回的版本列表中，查看 Draft 版本（`"Version": "draft"`）是否存在。

   * 如果 Draft 版本存在，您可以對該策略呼叫 `UpdateRuleEngineTemplate`。

   * 否則，您需要先對該策略呼叫 [CreateTemplateVersion](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_zh-tw) 以建立 Draft 版本，然後再呼叫 `UpdateRuleEngineTemplate`。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">該 API 已整合到 BytePlus SDK for Python v1.0.40 以及後續版本中。獲取 <a href="https://github.com/byteplus-sdk/byteplus-sdk-python">最新版本的 BytePlus SDK for Python</a>。</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">規則引擎設定的更新方式是全量覆蓋更新。在更新規則引擎設定時，如果規則中的某個已有設定沒有被指定，則該設定會被移除。您可以調用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_zh-tw">DescribeRuleEngineTemplate</a> 獲取當前規則的設定。</div>


<span id="使用限制"></span>
## 使用限制

請求頻率限制：您每秒最多可以提交 20 個 API 請求。

<span id="請求說明"></span>
## 請求說明


* 請求方法：POST

* 請求URL：https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021\-03\-01


<span id="請求參數"></span>
## 請求參數

<span id="query"></span>
### Query


|參數 |類型 |必要 |說明 |
|---|---|---|---|
|Action |String |是 |介面名稱。當前 API 的名稱為 `UpdateRuleEngineTemplate`。 |
|Version |String |是 |介面版本。當前 API 的版本為 `2021-03-01`。 |


<span id="body"></span>
### Body


|參數 |類型 |必要 |說明 |範例 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要修改配置的規則引擎策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeTemplates_zh-tw) 獲取您想要修改的規則引擎策略的 ID。 |`tpl-rev6j89` |
|Message |String |否 |表示一個新的策略描述，長度不能超過 120 個字符。 |`new-desc` |
|Rule |Object |否 |表示規則的配置。該參數的實際數據類型是 String。在提交 API 請求時，您需要序列化 `Rule` 結構體，使 JSON 格式轉換為字符串格式。操作步驟如下：<br><br><br>1. 移除最外層的 `[]`。<br><br>2. 刪除換行和空格。<br><br>3. 將 `"` 替換成 `\"`。<br><br>4. 將處理後的內容作為字符串設置為 `Rule` 的值。 |`參見下方的請求範例 1` |
|IfBlock |Object |是 |表示規則中 IF 表達式，包含 `Condition`、`Actions` 和 `SubRules` 這幾個結構體。這些結構體展示了以下請求處理邏輯：<br><br><br>* 如果用戶請求滿足 `Condition` 下的匹配條件，則 CDN 先執行 `IfBlock` 中 `Actions` 下的操作，再處理 `IfBlock` 中 `SubRules` 下的子規則。<br><br>* 否則，CDN 先執行 `ElseBlock` 中 `Actions` 下的操作，再處理 `ElseBlock` 中 `SubRules` 下的子規則。 | |
|SubRules |Object[] |否 |表示 IF 表達式下的子規則列表。列表中最多可以包含 10 條子規則。 | |
|Desc |String |否 |表示子規則的描述。 |`Sub-rule1` |
|IfBlock |Object |是 |表示子規則下的 IF 表達式，含義以及其包含的參數與父規則的 `IfBlock` 相同。需要留意的是，子規則中無法嵌套子規則。因此，子規則中 `IfBlock` 下的 `SubRules` 結構體的值必須為空（`[]`）。 | |
|ElseBlock |Object |否 |表示子規則下的 ELSE 表達式，含義以及其包含的參數與父規則的 `ElseBlock` 相同。 | |
|Actions |Object[] |是 |表示 CDN 執行的動作列表。每個動作就是一個 CDN 特性配置。<br><br>當前，部分 CDN 特性無法在規則引擎中配置，未來會陸續支持。關於規則引擎支持的 CDN 特性，參見 `Action` 參數的描述。 | |
|Action |String |否 |表示 CDN 特性的名稱。該參數有以下取值：<br><br><br>* `redirect_request`：表示 "URL 重定向改寫"。<br><br>* `redirect_protocol`：表示 "協議強制跳轉"。<br><br>* `allow_access`：表示允許所有收到的用戶請求。<br><br>* `download_speed_limit`：表示 "下載限速"。<br><br>* `request_header`：表示 "客戶端請求頭設置"。<br><br>* `deny_access`：表示拒絕任何收到的用戶請求。<br><br>* `cache_key`：表示 "快取索引鍵"。<br><br>* `compression`：表示 "智能壓縮"。<br><br>* `video_drag`：表示 "視頻拖拽"。<br><br>* `cache_time`：表示 "節點快取規則"。<br><br>* `origin_range`：表示 "Range 源伺服器請求"。<br><br>* `origin_follow`：表示 "源伺服器請求重定向跟隨"。<br><br>* `origin_tcp_timeout`：表示 "源伺服器請求 TCP 超時"。<br><br>* `origin_http_timeout`：表示 "源伺服器請求 HTTP 超時"。<br><br>* `response_header`：表示 "HTTP 響應頭設置"。<br><br><br>注意<br><br>如果匹配條件列表中有一個條件的 `Object` 是 `response_header` 或者 `http_code`，動作列表只能包含一個 `Action` 為 `respond_header` 的動作。 |`response_header` |
|Stage |String |否 |該參數表示 `Action` 的執行階段。無需設置。當您提交 API 請求時，CDN 會自動設置該參數值。該參數有以下取值：<br><br><br>* `client_request`：表示的階段是 CDN 收到用戶請求。<br><br>* `cache`：表示的階段是 CDN 快取来源伺服器響應。<br><br>* `origin_request`：表示的階段是 CDN 源伺服器請求文件。<br><br>* `client_response`：表示的階段是 CDN 響應用戶請求。<br><br><br>關於各階段下可設定的 Action 以及相應的參數，參見下方 [各 Stage 下 Action 的參數設定](https://docs.byteplus.com/en/docs/18/47601#%E5%90%84-stage-%E4%B8%8B-action-%E7%9A%84%E5%8F%83%E6%95%B8%E8%A8%AD%E5%AE%9A) 章節中的描述。 |`client_response` |
|Phase |Integer |否 |該參數對應 `Stage`，無需設置。當您提交 API 請求時，CDN 會自動設置該參數值。<br><br><br>* 如果 `Stage` 是 `client_request`，CDN 會將該參數值設置為 `1`。<br><br>* 如果 `Stage` 是 `cache` 時，CDN 會將該參數值設置為 `5`。<br><br>* 如果 `Stage` 是 `origin_request`時，CDN 會將該參數值設置為 `2`。<br><br>* 如果 `Stage` 是 `client_response` 時，CDN 會將該參數值設置為 `6`。 |`6` |
|Module |Integer |否 |該參數對應 `Stage`，無需設置。當您提交 API 請求時，CDN 會自動設置該參數值。<br><br><br>* 如果 `Stage` 是 `client_request`，CDN 會將該參數值設置為 `1`。<br><br>* 如果 `Stage` 是 `cache`，CDN 會將該參數值設置為 `2`。<br><br>* 如果 `Stage` 是 `origin_request`，CDN 會將該參數值設置為 `2`。<br><br>* 如果 `Stage` 是 `client_response`，CDN 會將該參數值設置為 `1`。 |`1` |
|Groups |Object[] |否 |表示 `Action` 對應的 CDN 特性配置，包含 `Dimension` 參數和 `GroupParameters` 結構體。<br><br><br>* `Dimension` 參數表示配置對象。某些 CDN 特性會包含多個配置對象。<br><br>* `GroupParameters` 結構體包含與 `Dimension` 對應的配置。某些配置的不同值會產生不同的配置組合，因此 `GroupParameters` 表示一個配置組。例如，在 "客戶端請求頭設置" 中，您可以對請求頭進行設置和刪除操作。這些操作會產生不同的配置組合，定義在各自的配置組中。另外，對於 `GroupParameters` 來說，每個配置組包含一個 `Parameters` 結構體。`Parameters` 結構體是一個參數列表，每個參數表示一個具體的配置。<br><br><br>參見下方 [各 Stage 下 Action 的參數設定](https://docs.byteplus.com/en/docs/18/47601#%E5%90%84-stage-%E4%B8%8B-action-%E7%9A%84%E5%8F%83%E6%95%B8%E8%A8%AD%E5%AE%9A) 章節中的描述。 | |
|Dimension |String |否 |表示配置對象。 |`response_header` |
|GroupParameters |Object[] |否 |表示與 `Dimension` 對應的配置。 | |
|Parameters |Object[] |是 |表示一個參數列表。 | |
|Name |String |是 |表示列表中一個參數的名稱。 |`action` |
|Values |String[] |是 |表示該參數的值。 | |
|Condition |Object |是 |表示 IF 表達式下的匹配條件定義。 | |
|IsGroup |Boolean |是 |該參數值必須是 `true`。 |`true` |
|Connective |String |是 |該參數值必須是 `and`。 |`and` |
|ConditionGroups |Object[] |是 |表示一個條件組列表。 | |
|IsGroup |Boolean |是 |表示每個列表項是否是條件組。該參數值必須是 `true`，表示每個列表項是一個條件組。 |`true` |
|Connective |String |是 |表示條件組之間的邏輯關係。該參數有以下取值：<br><br><br>* `and`：表示關係是 `AND`。<br><br>* `or`：表示關係是 `OR`。<br><br><br>該參數的默認值是 `and`。 |`and` |
|ConditionGroups |Object[] |是 |表示條件組中的匹配條件列表。 | |
|IsGroup |Boolean |是 |表示該匹配條件是否是條件組。該參數值必須是 `false`。規則引擎不支持條件組嵌套。 |`false` |
|Condition |Object |是 |表示列表中一個匹配條件的定義。每個匹配條件包含：<br><br><br>* `Object`：表示匹配對象。<br><br>* `Operator`：表示匹配操作符。<br><br>* `Value`：表示匹配值列表。除非 `Operator` 是 `exist` 或 `not_exist`，否則每個匹配條件中都需要指定匹配值列表。<br><br>* `IgnoreCase`：表示匹配值是否區分大小寫。僅適用於匹配值是字符串的情況。<br><br>* `TimeZone`：表示時區，僅適用於 `Object` 是 `request_time` 的情況。<br><br>* `Name`：表示參數名稱，適用於 `Object` 是 `query_string`、`request_header` 或者 `response_header` 的情況。另外，當 `Object` 是 `request_time` 時，`Name` 表示時間範圍的類型。<br><br><br>關於各 Object 可搭配使用的 `Operator`，以及 `IgnoreCase` 等資訊，參見下方 [各匹配對象的輸入要求](https://docs.byteplus.com/en/docs/18/47601#%E5%90%84%E5%8C%B9%E9%85%8D%E5%B0%8D%E8%B1%A1%E7%9A%84%E8%BC%B8%E5%85%A5%E8%A6%81%E6%B1%82) 章節的描述。 | |
|Object |String |是 |表示匹配對象。該參數有以下取值：<br><br><br>* `always`：表示所有請求。<br><br>* `path`：表示請求路徑，不包含查詢字符串。<br><br>* `path_and_param`：表示請求路徑和查詢字符串。<br><br>* `url`：表示完整的請求 URL。<br><br>* `query_string`：表示請求 URL 中的查詢字符串。<br><br>* `http_referer`：表示請求中的 Referer 頭部。<br><br>* `client_ip`：表示發送請求的客戶端 IP 地址。<br><br>* `http_origin`：表示請求中的 Origin 頭部。<br><br>* `http_ua`：表示請求中的 User\-Agent 頭部。<br><br>* `request_header`：表示請求中除 Origin，Referer 和 User\-Agent 之外的某個頭部。<br><br>* `client_area`：表示客戶端 IP 地址來自的國家或地區。<br><br>* `http_method`：表示請求使用的方法。<br><br>* `request_time`：表示 CDN 收到用戶請求的時間。<br><br>* `protocol`：表示請求使用的協議。<br><br>* `response_header`：表示来源伺服器響應中的某個頭部。<br><br>* `http_code`：表示来源伺服器響應中的狀態碼。 |`always` |
|Operator |String |是 |表示匹配操作符。該參數有以下取值：<br><br><br>* `prefix_match`：表示匹配指定的前綴。<br><br>* `prefix_not_match`：表示不匹配指定的前綴。<br><br>* `suffix_match`：表示匹配指定的後綴。<br><br>* `suffix_not_match`：表示不匹配指定的後綴。<br><br>* `match`：表示匹配指定的對象。<br><br>* `not_match`：表示不匹配指定的對象。<br><br>* `regex_match`：表示匹配指定的正則表達式。<br><br>* `regex_not_match`：表示不匹配指定的正則表達式。<br><br>* `equal`：表示與指定的值相同。<br><br>* `not_equal`：表示與指定的值不同。<br><br>* `exist`：表示指定的對象存在。<br><br>* `not_exist`：表示指定的對象不存在。 |`suffix_match` |
|IgnoreCase |Boolean |是 |表示 `Value` 是否區分大小寫。 |`true` |
|Value |String[] |是 |表示匹配值列表。<br><br>關於匹配值的輸入要求，參見下方 [各匹配對象的輸入要求](https://docs.byteplus.com/en/docs/18/47601#%E5%90%84%E5%8C%B9%E9%85%8D%E5%B0%8D%E8%B1%A1%E7%9A%84%E8%BC%B8%E5%85%A5%E8%A6%81%E6%B1%82) 章節的描述。 |`["png","gif"]` |
|Name |String |否 |* 當 `Object` 是 `request_header`、`response_header` 或 `query_string` 時，該參數表示您要指定的頭部或查詢參數。<br><br>* 當 `Object` 是 `request_time` 時，該參數有以下取值：<br><br>   * `weekday`：表示每星期中的固定幾天。<br><br>   * `period`：表示一個固定時間段。<br><br>   * `everyday`：表示每日中的固定時間段。 |`myparam` |
|TimeZone |String |否 |當 `Object` 是 `request_time` 時，該參數請求時間對應的時區。當前，您只能指定時區為 UTC+08:00，對應的參數值是 `+0800`。 |`+0800` |
|ElseBlock |Object |是 |表示規則中 ELSE 表達式，包含 `Actions` 和 `SubRules` 這兩個結構體。<br><br>如果用戶請求不滿足 `IfBlock` 中 `Condition` 下的匹配條件，CDN 先執行 `ElseBlock` 中 `Actions` 下的操作，再處理 `ElseBlock` 中 `SubRules` 下的子規則。 | |
|SubRules |Object[] |否 |表示 `ElseBlock` 表達式下的子規則列表，含義及其包含的參數與 `IfBlock` 下的 `SubRules` 結構體相同。列表中最多可以包含 10 條子規則。 | |
|IfBlock |Object |是 |表示子規則下的 IF 表達式，含義及其包含的參數與父規則的 `IfBlock` 相同。需要留意的是，子規則中無法嵌套子規則。因此，子規則中 `IfBlock` 下的 `SubRules` 結構體的值必須為空（`[]`）。 | |
|ElseBlock |Object |否 |表示子規則下的 ELSE 表達式，含義及其包含的參數與父規則的 `ElseBlock` 相同。 | |
|Actions |Object[] |否 |表示 `ElseBlock` 表達式下的 `Actions` 結構體，含義及其包含的參數與 `IfBlock` 的 `Actions` 相同。 | |
|TemplateVersion |String |否 |表示待更新的策略版本。<br><br><br>* 如果待更新的參數是 `Title` 或 `Message`，您無需指定該參數。這兩個參數與策略版本無關。<br><br>* 如果待更新的參數是不是 `Title` 和 `Message`，您必須指定該參數為 `draft`。參見文檔開頭的描述。 |`draft` |
|Title |String |否 |表示一個新的策略名稱，長度不能超過 100 個字符。 |`new-title` |


<span id="各-stage-下-action-的參數設定"></span>
## 各 Stage 下 Action 的參數設定

<span id="stage-為-client-request"></span>
### Stage 為 client_request


|**行為（Action）**  |**設定參數** |**範例** |
|---|---|---|
|`redirect_request` |* `source_path`：原始路徑，透過正規表示式比對。<br><br>* `status_code`：重新導向狀態碼，可選值為 `301`、`302`。<br><br>* `protocol`：重新導向協定。可選值為 `follow_client`、`http`、`https`。<br><br>* `target_host`：目標網站的網域名稱或 IP 位址。連接埠為選用。<br><br>* `target_path`：目標路徑，支援指定`$n` 捕獲原始路徑的群組。<br><br>* `target_query_action`：對使用者請求 URL 中查詢參數的處理方式，可選值為 `include_part`、`include_all`、`exclude_part`、`exclude_all`。<br><br>* `target_query_values`：表示需要包含或移除的參數。適用於 `target_query_action` 是 `include_part` 或 `exclude_part` 的情況。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_848f77ffbcb91e14ee2a87e9c611ec68.json" name="redirect_request">redirect_request</Attachment><br> |
|`redirect_protocol` |* `status_code`：重新導向狀態碼，可選值為 `301`、`302`。<br><br>* `protocol`：重新導向協定。可選值為 `http`、`https`。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_43a312a13033eee7e30a28eeb6487a84.json" name="redirect_protocol">redirect_protocol</Attachment><br> |
|`allow_access` |無設定參數。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_844ddd854d38fde71e00c867d6504455.json" name="allow_access">allow_access</Attachment><br> |
|`download_speed_limit` |* `rate`：傳輸速度上限。<br><br>* `rate_unit`：速度單位。可選值為 `KB/s`、`B/s、MB/s`。<br><br>* `after_size`：限速規則生效前的不限速資料量。<br><br>* `after_size_unit`：資料量單位。可選值為 `B`、`KB`、`MB`。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_74544cbc8f00df19cce27e4d3b4f5479.json" name="download_speed_limit">download_speed_limit</Attachment><br> |
|`request_header` |* `action`: 請求標頭操作，可選值為 `set`、`delete`。<br><br>* `header_name`：標頭名稱。<br><br>* `header_value`：標頭值，適用於 `action` 是 `set` 的情況。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1256921962199dc770f0e4166ffee10b.json" name="request_header">request_header</Attachment><br> |
|`deny_access` |* `status_code`：CDN 回應狀態碼，範圍是 100\-599。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7dbd65a0c7d33573eb4573650c05b65b.json" name="deny_access">deny_access</Attachment><br> |
|`url_auth` |* `auth_type`：表示驗證類型，可選值為 `type_a`、`type_b`、`type_c`、`type_d`、`type_e`。不支援 Type\-F。<br><br><br>**Type A 設定參數**<br><br><br>* `master_secret_key`：表示主金鑰。<br><br>* `backup_secret_key`：表示備用金鑰。<br><br>* `sign_name`：表示簽章參數的名稱。<br><br>* `duration`：表示簽章的有效時長，單位是秒。<br><br>* `time_format`：表示時間標記的格式，可選值為 `dec`。<br><br>* `algorithm`：表示驗證演算法，可選值為：`md5`、`sha256`。<br><br>* `origin_keep_auth_query`：表示是否在來源伺服器請求中包含簽章參數，可選值為 `true`、`false`。<br><br>* `rewrite_m3u8`：表示是否啟用 "M3U8 改寫"，可選值為 `true`、`false`。<br><br>* `keep_slice_query`：表示是否保留影片分片 URI 中的查詢參數，可選值為 `true`、`false`。<br><br>* `m3u8_keep_query`：表示是否在影片分片 URI 中新增使用者請求 URL 中的非簽章參數，可選值為 `true`、`false`。<br><br><br>**Type B 設定參數**<br><br><br>* `master_secret_key`、`backup_secret_key`、`duration`、`algorithm`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`<br><br>* `time_format`：可選值為 `fixed`，表示的時間格式為 YYYYMMDDHHMM。<br><br><br>**Type C 設定參數**<br><br><br>* `master_secret_key`、`backup_secret_key`、`duration`、`algorithm`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`<br><br>* `time_format`：可選值為 `hex`。<br><br><br>**Type D 設定參數**<br><br><br>* `master_secret_key`、`backup_secret_key`、`sign_name`、`time_name`、`duration`、`algorithm`、`origin_keep_auth_query`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`<br><br>* `time_format`：可選值為：`dec`、`hex`。<br><br>* `time_name`：表示時間標記參數的名稱。<br><br><br>**Type E 設定參數**<br><br><br>* `master_secret_key`、`backup_secret_key`、`sign_name`、`time_name`、`duration`、`algorithm`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`<br><br>* `time_format`：可選值為：`dec`、`hex`。<br><br>* `custom_headers`：表示額外參與簽章計算的自訂請求標頭，最多 50 個。<br><br>* `custom_queries`：表示額外參與簽章計算的查詢參數，最多 50 個。<br><br>* `signature_rules`：表示參數簽章計算的物件順序。`signature_rules` 中可以包含 `referer`、`origin`、`secret_key`、`domain`、`uri`、`ip`、`ua`、`time_name` 以及您在 `custom_headers` 和 `custom_queries` 中定義的請求標頭和查詢參數。這裡，`uri` 表示請求 URL 中的路徑，不包含查詢參數。`time_name` 表示時間標記。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9e2d9f901dba645ee1d151268cef353f.json" name="Type-A.json">Type-A.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b34837ee859b2fed3a499e332984665a.json" name="Type-B.json">Type-B.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f490fc5a97470ae259de0edd0d48447f.json" name="Type-C.json">Type-C.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f657cfc6b07b0d3f5d906fa53dbf14ed.json" name="Type-D.json">Type-D.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c9e2ad6c03eb25dcc8f49d218c21bb64.json" name="Type-E.json">Type-E.json</Attachment><br> |


<span id="stage-為-cache"></span>
### Stage 為 cache


|**行為（Action）**  |**設定參數** |**範例** |
|---|---|---|
|`cache_key` |`Dimension` 為 `query_string` 時，表示對請求 URL 中查詢參數的處理方式。快取索引鍵預設包含所有查詢參數，有以下設定參數：<br><br><br>* `query_action`：包含的查詢參數，可選值為 `include_part`、`include_all`、`exclude_part`、`exclude_all`。<br><br>* `query_names`：需要包含或移除的參數。適用於 `target_query_action` 是 `include_part` 或 `exclude_part` 的情況。<br><br>* `ignore_case`：查詢參數名稱是否區分大小寫。<br><br><br>&nbsp;<br><br>`Dimension` 為 `request_header` 時，表示對請求中標頭的處理方式。快取索引鍵預設不包含任何標頭，有以下設定參數：<br><br><br>* `header_names`：包含的標頭列表。<br><br>* `ignore_case`：標頭名稱是否區分大小寫。<br><br><br>&nbsp;<br><br>`Dimension` 為 `cookie` 時，表示對請求中 Cookie 的處理方式。快取索引鍵預設不包含任何 cookie，有以下設定參數：<br><br><br>* `cookie_action`：對使用者請求中 Cookie 的處理方式，可選值為 `include_part`、`include_all`、`exclude_part`、`exclude_all`。<br><br>* `cookie_names`：需要包含的 Cookie 列表，列表中是這些 Cookie 的 Key。<br><br>* `ignore_case`：Cookie key 是否區分大小寫。<br><br><br>&nbsp;<br><br>`Dimension` 為 `request_path` 時，表示是否改寫原始路徑，預設不改寫原始路徑，有以下設定參數：<br><br><br>* `source_path`：原始路徑，透過正規表示式比對。<br><br>* `target_path`：改寫後的路徑，支援指定`$n` 捕獲原始路徑的群組。<br><br><br>&nbsp;<br><br>`Dimension` 為 `path_ignore_case` 時，表示快取索引鍵中的路徑是否區分大小寫。預設是不區分大小寫，有以下設定參數：<br><br><br>* `ignore_case`：快取索引鍵中的路徑是否區分大小寫。<br><br><br> |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e259b18ca4cee02bd7e236a75a061fb8.json" name="cache_key">cache_key</Attachment><br> |
|`compression` |* `methods`：壓縮演算法，可選值為 `br`、`gzip`。<br><br>* `min_file_size`：檔案最小尺寸。小於該尺寸的檔案不壓縮。<br><br>* `min_file_size_unit`：尺寸單位。可選值為 `KB`、`MB`。<br><br>* `format`：檔案類型的設定。CDN 僅壓縮指定的檔案類型。可選值為 `default`、`customize`。`default` 表示`content_types` 列表中的所有類型。<br><br>* `content_types`：指定的檔案類型、適用於 `format` 是 `customize` 的情況。可選值為：`text/html`、`text/plain`、`text/xml`、`text/css`、`application/javascript`、`application/x-javascript`、`application/rss+xml`、`application/json`、`image/tiff`、`text/javascript`、`image/svg+xml`、`application/xml`、`text/plain; charset=utf-8`。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c1380dbf5f009acdada053eee900ca1f.json" name="compression">compression</Attachment><br> |
|`video_drag` |* `switch`：是否啟用影片拖曳。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_62fe72779258ada9a38aa3fd494f0162.json" name="video_drag">video_drag</Attachment><br> |
|`cache_time` |* `ttl`：快取時長。<br><br>* `ttl_unit`：快取時長的單位，可選值為 `sec`、`min`、`hour`、`day`。<br><br>* `cache_policy`：快取策略，可選值為 `default`、`origin_first`。<br><br>* `force_cache`：是否開啟 "強制快取"。適用於 `cache_policy`為 `default` 的情況。<br><br>* `replenish`：是否開啟 "補充快取"。適用于 `cache_policy`為 `origin_first`的情況。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d448267d7a5a5c6bc15853e5dc1c77b1.json" name="cache_time">cache_time</Attachment><br> |


<span id="stage-為-origin-request"></span>
### Stage 為 origin_request


|**行為（Action）**  |**設定參數** |**範例** |
|---|---|---|
|`origin_range` |* `switch`：是否啟用回源 Range。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c62df748b40fd99816bcac844204f33c.json" name="origin_range">origin_range</Attachment><br> |
|`origin_follow` |* `switch`：是否啟用回源重新導向跟隨。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d3f8a388aa58b13b92b51e255a062b1.json" name="origin_follow">origin_follow</Attachment><br> |
|`origin_tcp_timeout` |* `connect_timeout`：TCP 建連的逾時時長，預設值是 2。<br><br>* `connect_timeout_unit`：逾時時長的單位，可選值只能是 `sec`。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_268d479fbe65383bcf9a614f7a68ac9e.json" name="origin_tcp_timeout">origin_tcp_timeout</Attachment><br> |
|`origin_http_timeout` |* `connect_timeout`：HTTP 請求的逾時時長，預設值是 60。<br><br>* `connect_timeout_unit`：逾時時長的單位，可選值只能是 `sec`。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4c3e1cbcfdeff38969f4d5ed86ad3e25.json" name="connect_timeout_unit">connect_timeout_unit</Attachment><br> |


<span id="stage-為-client-response"></span>
### Stage 為 client_response


|**行為（Action）**  |**設定參數** |**範例** |
|---|---|---|
|`response_header` |* `action`: 回應標頭操作，可選值為 `set`、`delete`。<br><br>* `header_name`：標頭名稱。<br><br>* `header_value`：標頭值，適用於 `action` 是 `set` 的情況。 |<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cfae7ef66114e65159142de1f61bbed5.json" name="response_header">response_header</Attachment><br> |


<span id="各匹配對象的輸入要求"></span>
## 各匹配對象的輸入要求


|**匹配對象** |**IgnoreCase** |**可指定的** **Operator** |**Name 輸入要求** |**Value 輸入要求** |**範例值** |
|---|---|---|---|---|---|
|`always` |不適用 |不適用 |不適用 |不適用 | |
|`path` |適用 |`equal` `not_equal` |不適用 |* 必須以 `/` 開頭。<br><br>* 總數不能超過 100 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。 |`["/www/img/myimage.png", "/docs/file"]` |
|||`prefix_match` `prefix_not_match` ||* 必須以 `/` 開頭。<br><br>* 總數不能超過 100 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%） |`["/www", "/docs/f"]` |
|||`suffix_match` `suffix_not_match` ||* 總數不能超過 100 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。<br><br>* 不能以句點（.）開頭。 |`["png","docx"]` |
|||`regex_match` `regex_not_match` ||* 總數不能超過 50 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。 |`["^/a{1,2}(.*)g$"]` |
|`path_and_param` |適用 |與 `path` 相同 |不適用 |與 `path` 相同。 | |
|`url` |適用 |`equal` `not_equal` |不適用 |* 必須以 `http://` 或者 `https://` 開頭。<br><br>* 總數不能超過 100 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。 |`["https://www.example.com/www/img/myimage.png","https://www.example.com/docs/file"]` |
|||`prefix_match` `prefix_not_match` ||* 必須以 `http://` 或者 `https://` 開頭。<br><br>* 總數不能超過 100 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。 |`["https://www.example.com/www", "https://www.example.com/docs/f"]` |
|||`suffix_match` `suffix_not_match` ||* 總數不能超過 100 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。 |`["png","docx"]` |
|||`regex_match` `regex_not_match` ||* 總數不能超過 50 個，總長度不能超過 300 個字元。<br><br>* 不能包含空格、百分比符號（%）。 |`["^/a{1,2}(.*)g$"]` |
|`http_referer` |適用 |`equal` `not_equal` |不適用 |* 總數不能超過 100 個。<br><br>* 單一條目的長度不能超過 200 個字元。 |`["https://www.example.com/image.png", "a.example.com","*.exampe.net","203.0.113.8"]` |
|||`exist` `not_exist` ||不適用 | |
|||`regex_match` `regex_not_match` ||* 總數不能超過 50 個。<br><br>* 單一條目的長度不能超過 200 個字元。 |`["^/a{1,2}(.*)g$"]` |
|`client_ip` |不適用 |`match` `not_match` |不適用 |* 支援 IP 位址和 CIDR 網段。<br><br>* 支援 IPv4 位址和 IPv6 位址。<br><br>* 總數不能超過 100 個， |`["203.0.113.8","203.0.113.9"]` |
|`http_origin` |適用 |與 `http_referer` 相同。 |不適用 |與 `http_referer` 相同。 | |
|`http_ua` |適用 |與 `http_referer` 相同。 |不適用 |與 `http_referer` 相同。 | |
|`request_header` |適用 |與 `http_referer` 相同。 |* 不能包含漢字、底線（_）、空格、雙引號（"）、冒號（:）。<br><br>* 長度不能超過 100 個字元。 |與 `http_referer` 相同。 |**Name**<br><br>`myheader`<br><br>**Value**<br><br>`["value1","value2"]` |
|`client_area` |不適用 |`match` `not_match` |不適用 |* 包含最多 30 個國家或地區的 Alpha\-3 代碼。Alpha\-3 代碼可以呼叫 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-DescribeCdnRegionAndIsp_zh-tw) 獲取。 |`["PNG","FSM","FSM"]` |
|`http_method` |不適用 |`equal` `not_equal` |不適用 |* 包含以下一個或多個值：`post`、`head`、`get`、`put`、`options`、`delete`、`connect`、`patch`。 |`["post","options"]` |
|`request_time` |不適用 |`match` `not_match` |`weekday` |* 包含以下一個或多個值：`mon`、`tue`、`wed`、`thur`、`fri`、`sat`、`sun`。 |`["mon","fri"]` |
||||`period` |指定一個任意時間段的開始和結束時間，精確到秒。 |`["2025-05-07 14:21:21", "2025-06-13 14:21:24"]` |
||||`everyday` |指定每天的一個時間段的開始和結束時間，精確到秒。 |`["02:02:02","06:04:04"]` |
|`protocol` |不適用 |`equal` `not_equal` |不適用 |指定 `http` 或者 `https`。 |`["http"]` |
|`response_header` |適用 |與 `http_referer` 相同。 |* 不能包含漢字、底線（_）、空格、雙引號（"）、冒號（:）。<br><br>* 長度不能超過 100 個字元。 |與 `http_referer` 相同。 |**Name**<br><br>`myheader`<br><br>**Value**<br><br>`["value1","value2"]` |
|`http_code` |不適用 |`match` `not_match` |不適用 |* 包含最多 30 個狀態碼。<br><br>* 狀態碼的範圍是 100\-599。<br><br>* 支援指定 `2xx`、`3xx` 等。 |`["405","5xx"]` |


<span id="回應"></span>
## 回應

<span id="範例"></span>
## 範例

<span id="範例請求"></span>
### 範例請求

<span id="範例一"></span>
#### 範例一

```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
    "Rule": "{\"IfBlock\":{\"SubRules\":[],\"Actions\":[{\"Action\":\"origin_tcp_timeout\",\"Stage\":\"origin_request\",\"Phase\":2,\"Module\":2,\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"30\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}],\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Condition\":{\"Object\":\"always\"}}]}]}}}"
}
```


<span id="範例二"></span>
#### 範例二

本範例重點展示 `Condition` 的配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本範例不能直接使用。您需要先處理 <code>Rule</code> 結構體中的參數配置。參見 <code>Rule</code> 參數的說明。</div>


```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine-actions",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
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
    ]
}
```


<span id="範例三"></span>
#### 範例三

本範例重點展示 `Condition` 的配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本範例不能直接使用。您需要先處理 <code>Rule</code> 結構體中的參數配置。參見 <code>Rule</code> 參數的說明。</div>


```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine-actions",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
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
                    },
                    {
                        "Action": "url_auth",
                        "Stage": "client_request",
                        "Phase": 1,
                        "Module": 3,
                        "Groups": [
                            {
                                "Dimension": "url_auth",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "auth_type",
                                                "Values": [
                                                    "type_e"
                                                ]
                                            },
                                            {
                                                "Name": "master_secret_key",
                                                "Values": [
                                                    "pk123"
                                                ]
                                            },
                                            {
                                                "Name": "backup_secret_key",
                                                "Values": [
                                                    "bk456"
                                                ]
                                            },
                                            {
                                                "Name": "sign_name",
                                                "Values": [
                                                    "sign"
                                                ]
                                            },
                                            {
                                                "Name": "time_name",
                                                "Values": [
                                                    "ts"
                                                ]
                                            },
                                            {
                                                "Name": "duration",
                                                "Values": [
                                                    "600"
                                                ]
                                            },
                                            {
                                                "Name": "time_format",
                                                "Values": [
                                                    "hex"
                                                ]
                                            },
                                            {
                                                "Name": "algorithm",
                                                "Values": [
                                                    "md5"
                                                ]
                                            },
                                            {
                                                "Name": "rewrite_m3u8",
                                                "Values": [
                                                    "true"
                                                ]
                                            },
                                            {
                                                "Name": "keep_slice_query",
                                                "Values": [
                                                    "true"
                                                ]
                                            },
                                            {
                                                "Name": "m3u8_keep_query",
                                                "Values": [
                                                    "true"
                                                ]
                                            },
                                            {
                                                "Name": "custom_headers",
                                                "Values": [
                                                    "header1",
                                                    "header2"
                                                ]
                                            },
                                            {
                                                "Name": "custom_queries",
                                                "Values": [
                                                    "param1",
                                                    "param2"
                                                ]
                                            },
                                            {
                                                "Name": "signature_rules",
                                                "Values": [
                                                    "secret_key",
                                                    "domain",
                                                    "uri",
                                                    "ip",
                                                    "ua",
                                                    "referer",
                                                    "origin",
                                                    "time_name",
                                                    "header1",
                                                    "header2",
                                                    "param1",
                                                    "param2"
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
    ]
}
```


<span id="範例回應"></span>
### 範例回應

&nbsp;
