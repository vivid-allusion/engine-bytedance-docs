---
title: "UpdateRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_zh-cn"
---

更新规则引擎模板中的配置。

除了 `Title` 和 `Message`，其他参数的更新需要您在调用 `UpdateRuleEngineTemplate` 时指定 `TemplateVersion` 为 `draft`。也就是说，待更新的策略已存在 Draft 版本。要确保待更新的策略已存在 Draft 版本，参照以下步骤：


1. 对该策略调用 [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_zh-cn) API。

2. 在 API 返回的版本列表中，查看 Draft 版本（`"Version": "draft"`）是否存在。

   * 如果 Draft 版本存在，您可以对该策略调用 `UpdateRuleEngineTemplate`。

   * 否则，您需要先对该策略调用 [CreateTemplateVersion](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_zh-cn) 以创建 Draft 版本，然后再调用 `UpdateRuleEngineTemplate`。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">该 API 已集成到 BytePlus SDK for Python v1.0.40 以及后续版本中。获取 <a href="https://github.com/byteplus-sdk/byteplus-sdk-python">最新版本的 BytePlus SDK for Python</a>。</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">规则引擎配置的更新方式是全量覆盖更新。在更新规则引擎配置时，如果规则中的某个已有配置没有被指定，则该配置会被移除。您可以调用 <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_zh-cn">DescribeRuleEngineTemplate</a> 获取当前规则的配置。</div>


<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `UpdateRuleEngineTemplate`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|TemplateId |String |是 |表示您要修改配置的规则引擎策略的 ID。<br><br>您可以使用 [DescribeTemplates](https://docs.byteplus.com/byteplus-cdn/reference/describetemplates) 获取您想要修改的规则引擎策略的 ID。 |`tpl-rev6j89` |
|Message |String |否 |表示一个新的策略描述，长度不能超过 120 个字符。 |`new-desc` |
|Rule |Object |否 |表示规则的配置。该参数的实际数据类型是 String。在提交 API 请求时，您需要序列化 `Rule` 结构体，使 JSON 格式转换为字符串格式。操作步骤如下：<br><br><br>1. 移除最外层的 `[]`。<br><br>2. 删除换行和空格。<br><br>3. 将 `"` 替换成 `\"`。<br><br>4. 将处理后的内容作为字符串设置为 `Rule` 的值。 |`参见 请求示例一。` |
|IfBlock |Object |是 |表示规则中 IF 表达式，包含 `Condition`、`Actions` 和 `SubRules` 这几个结构体。这些结构体展示了以下请求处理逻辑：<br><br><br>* 如果用户请求满足 `Condition` 下的匹配条件，则 CDN 先执行 `IfBlock` 中 `Actions` 下的操作，再处理 `IfBlock` 中 `SubRules` 下的子规则。<br><br>* 否则，CDN 先执行 `ElseBlock` 中 `Actions` 下的操作，再处理 `ElseBlock` 中 `SubRules` 下的子规则。 | |
|SubRules |Object[] |否 |表示 IF 表达式下的子规则列表。列表中最多可以包含 10 条子规则。 | |
|Desc |String |否 |表示子规则的描述。 |`Sub-rule1` |
|IfBlock |Object |是 |表示子规则下的 IF 表达式，含义以及其包含的参数与父规则的 `IfBlock` 相同。需要留意的是，子规则中无法嵌套子规则。因此，子规则中 `IfBlock` 下的 `SubRules` 结构体的值必须为空（`[]`）。 | |
|ElseBlock |Object |否 |表示子规则下的 ELSE 表达式，含义以及其包含的参数与父规则的 `ElseBlock` 相同。 | |
|Actions |Object[] |是 |表示 CDN 执行的动作列表。每个动作就是一个 CDN 特性配置。<br><br>当前，部分 CDN 特性无法在规则引擎中配置，未来会陆续支持。关于规则引擎支持的 CDN 特性，参见 `Action` 参数的描述。 | |
|Action |String |否 |表示 CDN 特性的名称。该参数有以下取值：<br><br><br>* `redirect_request`：表示 "URL 重定向改写"。<br><br>* `allow_access`：表示 "允许访问"。<br><br>* `redirect_protocol`：表示 "协议强制跳转"。<br><br>* `download_speed_limit`：表示 "下载限速"。<br><br>* `request_header`：表示 "客户端请求头设置"。<br><br>* `deny_access`：表示 "拒绝访问"。<br><br>* `url_auth`：表示 "URL 鉴权"。<br><br>* `cache_key`：表示 "缓存键值"。<br><br>* `compression`：表示 "智能压缩"。<br><br>* `video_drag`：表示 "视频拖拽"。<br><br>* `cache_time`：表示 "节点缓存规则"。<br><br>* `response_header`：表示 "HTTP 响应头设置"。<br><br>* `browser_cache`：表示 "浏览器缓存"。<br><br>* `http_code`：表示 "HTTP 状态码改写"。<br><br>* `custom_page`：表示 "自定义页面"。<br><br>* `origin_range`：表示 "Range 回源"。<br><br>* `origin_follow`：表示 "回源重定向跟随"。<br><br>* `origin_tcp_timeout`：表示 "回源 TCP 超时"。<br><br>* `origin_http_timeout`：表示 "回源 HTTP 超时"。<br><br>* `origin_rewrite`：表示 "回源改写"。<br><br>* `origin_sni`：表示 "回源 SNI"。<br><br>* `origin_protocol`：表示 "回源协议"。<br><br>* `origin_request_header`：表示 "HTTP 请求头设置"。<br><br>* `origin_host`：表示 "回源 Host"。<br><br><br>注意<br><br>如果匹配条件列表中有一个条件的 `Object` 是 `response_header` 或者 `http_code`，动作列表只能包含一个 [Stage 为 client_response](https://docs.byteplus.com/en/docs/18/47553#stage-%E4%B8%BA-client-response) 的动作。 |`response_header` |
|Groups |Object[] |否 |表示 `Action` 对应的 CDN 特性配置，包含 `Dimension` 参数和 `GroupParameters` 结构体。<br><br><br>* `Dimension` 参数表示配置对象。某些 CDN 特性会包含多个配置对象。<br><br>* `GroupParameters` 结构体包含与 `Dimension` 对应的配置。某些配置的不同值会产生不同的配置组合，因此 `GroupParameters` 表示一个配置组。例如，在 "客户端请求头设置" 中，您可以对请求头进行设置和删除操作。这些操作会产生不同的配置组合，定义在各自的配置组中。另外，对于 `GroupParameters` 来说，每个配置组包含一个 `Parameters` 结构体。`Parameters` 结构体是一个参数列表，每个参数表示一个具体的配置。<br><br><br>参见 [各 Stage 下 Action 的参数配置](https://docs.byteplus.com/en/docs/18/47553#%E5%90%84-stage-%E4%B8%8B-action-%E7%9A%84%E5%8F%82%E6%95%B0%E9%85%8D%E7%BD%AE) 章节的描述。 | |
|Dimension |String |否 |表示配置对象。 |`response_header` |
|GroupParameters |Object[] |否 |表示与 `Dimension` 对应的配置。 | |
|Parameters |Object[] |是 |表示一个参数列表。 | |
|Name |String |是 |表示列表中一个参数的名称。 |`action` |
|Values |String[] |是 |表示该参数的值。 | |
|Condition |Object |是 |表示 IF 表达式下的匹配条件定义。 | |
|IsGroup |Boolean |是 |该参数值必须是 `true`。 |`true` |
|Connective |String |是 |该参数值必须是 `and`。 |`and` |
|ConditionGroups |Object[] |是 |表示一个条件组列表。 | |
|IsGroup |Boolean |是 |表示每个列表项是否是条件组。该参数值必须是 `true`，表示每个列表项是一个条件组。 |`true` |
|Connective |String |是 |表示条件组之间的逻辑关系。该参数有以下取值：<br><br><br>* `and`：表示关系是 `AND`。<br><br>* `or`：表示关系是 `OR`。<br><br><br>该参数的默认值是 `and`。 |`and` |
|ConditionGroups |Object[] |是 |表示条件组中的匹配条件列表。 | |
|IsGroup |Boolean |是 |表示该匹配条件是否是条件组。该参数值必须是 `false`。规则引擎不支持条件组嵌套。 |`false` |
|Condition |Object |是 |表示列表中一个匹配条件的定义。每个匹配条件包含：<br><br><br>* `Object`：表示匹配对象。<br><br>* `Operator`：表示匹配操作符。<br><br>* `Value`：表示匹配值列表。除非 `Operator` 是 `exist` 或 `not_exist`，否则每个匹配条件中都需要指定匹配值列表。<br><br>* `IgnoreCase`：表示匹配值是否区分大小写。仅适用于匹配值是字符串的情况。<br><br>* `TimeZone`：表示时区，仅适用于 `Object` 是 `request_time` 的情况。<br><br>* `Name`：<br><br>   * 表示参数名称，适用于 `Object` 是 `query_string`、`request_header`、 `response_header` 或者 `client_cert_info` 的情况。<br><br>   * 表示时间范围的类型，适用于 `Object` 是 `request_time` 的情况。<br><br><br>关于各 Object 可搭配使用的 `Operator`，以及 `IgnoreCase` 等信息，参见下方 [各匹配对象的输入要求](https://docs.byteplus.com/en/docs/18/47553#%E5%90%84%E5%8C%B9%E9%85%8D%E5%AF%B9%E8%B1%A1%E7%9A%84%E8%BE%93%E5%85%A5%E8%A6%81%E6%B1%82) 章节的描述。 | |
|Object |String |是 |表示匹配对象。该参数有以下取值：<br><br><br>* `always`：表示所有请求。<br><br>* `path`：表示请求路径，不包含查询字符串。<br><br>* `path_and_param`：表示请求路径和查询字符串。<br><br>* `url`：表示完整的请求 URL。<br><br>* `query_string`：表示请求 URL 中的查询字符串。<br><br>* `http_referer`：表示请求中的 Referer 头部。<br><br>* `client_ip`：表示发送请求的客户端 IP 地址。<br><br>* `http_origin`：表示请求中的 Origin 头部。<br><br>* `http_ua`：表示请求中的 User\-Agent 头部。<br><br>* `request_header`：表示请求中除 Origin，Referer 和 User\-Agent 之外的某个头部。<br><br>* `client_area`：表示客户端 IP 地址来自的国家或地区。<br><br>* `http_method`：表示请求使用的方法。<br><br>* `request_time`：表示 CDN 收到用户请求的时间。<br><br>* `protocol`：表示请求使用的协议。<br><br>* `response_header`：表示源站响应中的某个头部。<br><br>* `http_code`：表示源站响应中的状态码。 |`always` |
|Operator |String |是 |表示匹配操作符。该参数有以下取值：<br><br><br>* `prefix_match`：表示匹配指定的前缀。<br><br>* `prefix_not_match`：表示不匹配指定的前缀。<br><br>* `suffix_match`：表示匹配指定的后缀。<br><br>* `suffix_not_match`：表示不匹配指定的后缀。<br><br>* `match`：表示匹配指定的对象。<br><br>* `not_match`：表示不匹配指定的对象。<br><br>* `regex_match`：表示匹配指定的正则表达式。<br><br>* `regex_not_match`：表示不匹配指定的正则表达式。<br><br>* `equal`：表示与指定的值相同。<br><br>* `not_equal`：表示与指定的值不同。<br><br>* `exist`：表示指定的对象存在。<br><br>* `not_exist`：表示指定的对象不存在。<br><br>* `belong_to`：表示属于指定的全局配置。<br><br>* `not_belong_to`：表示不属于指定的全局配置。 |`suffix_match` |
|IgnoreCase |Boolean |是 |表示 `Value` 是否区分大小写。 |`true` |
|Value |String[] |是 |表示匹配值列表。<br><br>关于匹配值的输入要求，参见下方 [各匹配对象的输入要求](https://docs.byteplus.com/en/docs/18/47553#%E5%90%84%E5%8C%B9%E9%85%8D%E5%AF%B9%E8%B1%A1%E7%9A%84%E8%BE%93%E5%85%A5%E8%A6%81%E6%B1%82) 章节的描述。 |`["png","gif"]` |
|Name |String |否 |* 当 `Object` 是 `request_header`、`response_header` 或 `query_string` 时，该参数表示您要指定的头部或查询参数。<br><br>* 当 `Object` 是 `request_time` 时，该参数有以下取值：<br><br>   * `weekday`：表示每星期中的固定几天。<br><br>   * `period`：表示一个固定时间段。<br><br>   * `everyday`：表示每日中的固定时间段。<br><br>* 当 `Object` 是 `client_cert_info` 时，该参数有以下取值：<br><br>   * `common_name`：表示证书主题中的通用名称（Common Name）。<br><br>   * `serial_number`：表示证书序列号。<br><br>   * `country_name`：表示证书主体所属国家或地区的代码。<br><br>   * `locality_name`：表示证书主体所在的城市或地区。<br><br>   * `organization_name`：表示证书主体所属组织或公司名称。<br><br>   * `organizational_unit_name`：表示证书主体所属的组织单位或部门名称。 |`myparam` |
|TimeZone |String |否 |当 `Object` 是 `request_time` 时，该参数请求时间对应的时区。当前，您只能指定时区为 UTC+08:00，对应的参数值是 `+0800`。 |`+0800` |
|ElseBlock |Object |是 |表示规则中 ELSE 表达式，包含 `Actions` 和 `SubRules` 这两个结构体。<br><br>如果用户请求不满足 `IfBlock` 中 `Condition` 下的匹配条件，CDN 先执行 `ElseBlock` 中 `Actions` 下的操作，再处理 `ElseBlock` 中 `SubRules` 下的子规则。 | |
|SubRules |Object[] |否 |表示 `ElseBlock` 表达式下的子规则列表，含义及其包含的参数与 `IfBlock` 下的 `SubRules` 结构体相同。列表中最多可以包含 10 条子规则。 | |
|IfBlock |Object |是 |表示子规则下的 IF 表达式，含义及其包含的参数与父规则的 `IfBlock` 相同。需要留意的是，子规则中无法嵌套子规则。因此，子规则中 `IfBlock` 下的 `SubRules` 结构体的值必须为空（`[]`）。 | |
|ElseBlock |Object |否 |表示子规则下的 ELSE 表达式，含义及其包含的参数与父规则的 `ElseBlock` 相同。 | |
|Actions |Object[] |否 |表示 `ElseBlock` 表达式下的 `Actions` 结构体，含义及其包含的参数与 `IfBlock` 的 `Actions` 相同。 | |
|TemplateVersion |String |否 |表示待更新的策略版本。<br><br><br>* 如果待更新的参数是 `Title` 或 `Message`，您无需指定该参数。这两个参数与策略版本无关。<br><br>* 如果待更新的参数是不是 `Title` 和 `Message`，您必须指定该参数为 `draft`。参见文档开头的描述。 |`draft` |
|Title |String |否 |表示策略的新名称，长度不能超过 100 个字符。 |`new-title` |


<span id="各-stage-下-action-的参数配置"></span>
## 各 Stage 下 Action 的参数配置

<span id="stage-为-client-request"></span>
### Stage 为 client_request


|**行为（Action）**  |**配置参数** |**示例** |
|---|---|---|
|`redirect_request` |* `source_path`：原始路径，通过正则表达式匹配。<br><br>* `status_code`：重定向状态码，取值有 `301`、`302`、`303`、`307`、`308`。<br><br>* `protocol`：重定向协议。取值有 `follow_client`、`http`、`https`。<br><br>* `target_host`：目标站点的域名或 IP 地址，端口可选。<br><br>* `target_path`：目标路径，支持指定`$n` 捕获原始路径的组。<br><br>* `target_query_action`：对用户请求 URL 中查询参数的处理方式，取值有 `include_part`、`include_all`、`exclude_part`、`exclude_all`。<br><br>* `target_query_values`：需要包含或移除的参数。适用于 `target_query_action` 是 `include_part` 或 `exclude_part` 的情况。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_269c25d2888e08f8eba903f3f8d810c1.json" name="redirect_request">redirect_request</Attachment><br> |
|`redirect_protocol` |* `status_code`：重定向状态码，取值有 `301`、`302`、`303`、`307`、`308`。<br><br>* `protocol`：重定向协议。取值有 `http`、`https`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc69f446b49ee968718afdfc8fc9c994.json" name="redirect_protocol">redirect_protocol</Attachment><br> |
|`allow_access` |* `effective_scope`：生效范围，取值有 `rule_engine`、`method_denied_rule`、`area_access_rule`、`request_block_rule`。生效范围内的访问控制规则不再拦截符合规则引擎条件的请求。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1cb30425b540afd3d3cce038f4d0fe92.json" name="allow_access.json">allow_access.json</Attachment><br> |
|`download_speed_limit` |* `limit_type`：传输速度上限。取值有 `normal`、`dynamic_limit`。<br><br>* `rate`：传输速度上限。<br><br>* `query_name`：限速参数的名称。适用于 `limit_type` 是 `dynamic_limit` 的情况。<br><br>* `dynamic_rate_unit`：限速参数所指示的速度的单位。取值有 `KB/s`、`B/s`、`MB/s`。适用于 `limit_type` 是 `dynamic_limit` 的情况。<br><br>* `rate_unit`：速度单位。取值有 `KB/s`、`B/s、MB/s`。<br><br>* `after_size`：限速规则生效前的不限速数据量。<br><br>* `after_size_unit`：数据量单位。取值有 `B`、`KB`、`MB`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30784db7f6e71524b69af14c020ecc2d.json" name="download_speed_limit.json">download_speed_limit.json</Attachment><br> |
|`request_header` |* `action`: 对客户端请求头操作，取值有 `set`、`delete`。<br><br>* `header_name`：头部名称。<br><br>* `header_value`：头部值，适用于 `action` 是 `set` 的情况。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13c911a67e9d16e54b479d9e20113613.json" name="request_header">request_header</Attachment><br> |
|`deny_access` |* `status_code`：CDN 响应状态码，范围是 100\-599。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90022a80c3c7d9204a21ccadddececca.json" name="deny_access">deny_access</Attachment><br> |
|`url_auth` |* `auth_type`：鉴权类型，取值有 `type_a`、`type_b`、`type_c`、`type_d`、`type_e`<br><br><br>**Type A 配置参数**<br><br><br>* `master_secret_key`：主密钥。<br><br>* `backup_secret_key`：备密钥。<br><br>* `sign_name`：签名参数的名称。<br><br>* `duration`：签名的有效时长，单位是秒。<br><br>* `time_format`：时间戳的格式，取值为 `dec`。<br><br>* `algorithm`：鉴权算法，取值有：`md5`、`sha256`。<br><br>* `origin_keep_auth_query`：是否在回源请求以及缓存键中均包含签名参数，取值有 `true`、`false`。<br><br>* `rewrite_m3u8`：是否启用 "M3U8 改写"，取值有 `true`、`false`。<br><br>* `keep_slice_query`：是否保留视频分片 URI 中的查询参数，取值有 `true`、`false`。<br><br>* `m3u8_keep_query`：是否在视频分片 URI 中添加用户请求 URL 中的非签名参数，取值有 `true`、`false`。<br><br>* `rewrite_m3u8_tag`：额外需要进行 URI 改写的标签列表。<br><br><br>**Type B 配置参数**<br><br><br>* `master_secret_key`、`backup_secret_key`、`duration`、`algorithm`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`、`rewrite_m3u8_tag`<br><br>* `time_format`：取值有：`dec`、`hex`、`basicFormat2m`。`basicFormat2m` 表示的格式是 YYYYMMDDHHMM。<br><br><br>**Type C 配置参数**<br><br><br>* `master_secret_key`、`backup_secret_key`、`duration`、`algorithm`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`、`rewrite_m3u8_tag`<br><br>* `time_format`：取值为 `hex`。<br><br><br>**Type D 配置参数**<br><br><br>* `master_secret_key`、`backup_secret_key`、`sign_name`、`time_name`、`duration`、`algorithm`、`origin_keep_auth_query`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`、`rewrite_m3u8_tag`<br><br>* `time_format`：取值有：`dec`、`hex`。<br><br>* `time_name`：时间戳参数的名称。<br><br><br>**Type E 配置参数**<br><br><br>* `master_secret_key`、`backup_secret_key`、`sign_name`、`time_name`、`duration`、`algorithm`、`rewrite_m3u8`、`keep_slice_query`、`m3u8_keep_query`、`rewrite_m3u8_tag`<br><br>* `time_format`：取值有：`dec`、`hex`。<br><br>* `custom_headers`：额外参与签名计算的自定义请求头，最多 50 个。<br><br>* `custom_queries`：额外参与签名计算的查询参数，最多 50 个。<br><br>* `signature_rules`：参数签名计算的对象顺序。`signature_rules` 中可以包含 `referer`、`origin`、`secret_key`、`domain`、`uri`、`ip`、`ua`、`time_name` 以及您在 `custom_headers` 和 `custom_queries` 中定义的请求头和查询参数。这里，`uri` 表示请求 URL 中的路径，不包含查询参数。`time_name` 表示时间戳。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ae398c73b502830e7d5c3bb7917a718.json" name="type-a.json">type-a.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5fe383bbfaae4c4f390346f6bf84439.json" name="type_b.json">type_b.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f8930053c49164c8dc3d8208da23e69.json" name="type_c.json">type_c.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b61a3d5d2a1cf109e90c979f86960bc8.json" name="type_d.json">type_d.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a33dba9f893d5c7f61b2db3714f94d4f.json" name="type-e.json">type-e.json</Attachment><br> |


<span id="stage-为-cache"></span>
### Stage 为 cache


|**行为（Action）**  |**配置参数** |**示例** |
|---|---|---|
|`cache_key` |`Dimension` 为 `query_string` 时，表示对请求 URL 中查询参数的处理方式。缓存键默认包含所有查询参数，有以下配置参数：<br><br><br>* `query_action`：包含的查询参数，取值有 `include_part`、`include_all`、`exclude_part`、`exclude_all`。<br><br>* `query_names`：需要包含或移除的参数。适用于 `target_query_action` 是 `include_part` 或 `exclude_part` 的情况。<br><br>* `ignore_case`：查询参数名称是否是大小写敏感的。<br><br><br>&nbsp;<br><br>`Dimension` 为 `request_header` 时，表示对请求中头部的处理方式。缓存键默认不包含任何头部，有以下配置参数：<br><br><br>* `header_names`：包含的头部列表。<br><br>* `ignore_case`：头部名称是否是大小写敏感的，取值必须为 `true`。<br><br><br>&nbsp;<br><br>`Dimension` 为 `cookie` 时，表示对请求中 Cookie 的处理方式。缓存键默认不包含任何 cookie，有以下配置参数：<br><br><br>* `cookie_action`：对用户请求中 Cookie 的处理方式，取值有 `include_part`、`include_all`、`exclude_part`、`exclude_all`。<br><br>* `cookie_names`：需要包含的 Cookie 列表，列表中是这些 Cookie 的 Key。<br><br>* `ignore_case`：Cookie key 是否是大小写敏感的。<br><br><br>&nbsp;<br><br>`Dimension` 为 `request_path` 时，表示是否改写原始路径，默认不改写原始路径，有以下配置参数：<br><br><br>* `source_path`：原始路径，通过正则表达式匹配。<br><br>* `target_path`：改写后的路径，支持指定`$n` 捕获原始路径的组。<br><br><br>&nbsp;<br><br>`Dimension` 为 `path_ignore_case` 时，表示缓存键中的路径是否区分大小写。默认是大小写不敏感，有以下配置参数：<br><br><br>* `ignore_case`：缓存键中的路径是否是大小写敏感的。<br><br><br> |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03ae9096555995f285cb21a33f24e239.json" name="cache_key">cache_key</Attachment><br> |
|`compression` |* `methods`：压缩算法，取值有 `br`、`gzip`。<br><br>* `min_file_size`：文件最小尺寸。小于该尺寸的文件不压缩。<br><br>* `min_file_size_unit`：尺寸单位。取值有 `KB`、`MB`。<br><br>* `format`：文件类型的配置，CDN 仅压缩指定类型的文件。取值有 `default`、`customize`。`default` 表示`content_types` 列表中的所有类型。<br><br>* `content_types`：指定的文件类型、适用于 `format` 是 `customize` 的情况。取值有：`text/html`、`text/plain`、`text/xml`、`text/css`、`application/javascript`、`application/x-javascript`、`application/rss+xml`、`application/json`、`image/tiff`、`text/javascript`、`image/svg+xml`、`application/xml`、`text/plain; charset=utf-8`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea52d7a5b797b0adf65c90403fa4cedd.json" name="compression">compression</Attachment><br> |
|`video_drag` |* `switch`：是否启用视频拖拽。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c85937d97bbf2841da168c5f33d0e6d.json" name="video_drag">video_drag</Attachment><br> |
|`cache_time` |* `ttl`：缓存时长，适用于 `cache_policy`为 `default` 的情况。<br><br>* `ttl_unit`：缓存时长的单位，取值有 `sec`、`min`、`hour`、`day`。适用于 `cache_policy`为 `default` 的情况。<br><br>* `cache_policy`：缓存策略，取值有 `default`、`origin_first`、`no_cache`。<br><br>* `force_cache`：是否开启 "强制缓存"。适用于 `cache_policy`为 `default` 的情况。<br><br>* `replenish`：当源站响应中既不包含 `Cache-Control` 也不包含 `Expires` 时，是否使用已配置的缓存时长。仅当 `cache_policy` 为 `origin_first` 时适用。<br><br>* `set_cookie_no_cache`：是否缓存包含 Set\-Cookie 头部的源站响应。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5b20c40df5a15b2396da1c7cd6dceab.json" name="cache_time">cache_time</Attachment><br> |


<span id="stage-为-client-response"></span>
### Stage 为 client_response


|**行为（Action）**  |**配置参数** |**配置参数** |
|---|---|---|
|`response_header` |* `action`: CDN 响应用户请求时对响应头的操作，取值有 `set`、`delete`。<br><br>* `header_name`：头部名称。<br><br>* `header_value`：头部值，适用于 `action` 是 `set` 的情况。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_19c29be2af0dd5a170d32f19d8d095ff.json" name="response_header">response_header</Attachment><br> |
|`browser_cache` |* `cache_policy`：缓存策略，取值有 `cache`、`origin_first`、`no_cache`。<br><br><br>当 `cache_policy` 为 `cache` 时，您还需要设置：<br><br><br>* `ttl`：缓存时长，最长 10 年。<br><br>* `ttl_unit`：时长单位，取值有 `sec`、`min`、`hour`、`day`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_3803a1f675d2d36d62c4011e422d043a.json" name="browser_cache.json">browser_cache.json</Attachment><br> |
|`http_code` |* `status_code`：自定义 CDN 响应状态码，取值范围为 100\-999。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_fec6c7abf0691beff86c81c0f1d2eab3.json" name="http_code.json">http_code.json</Attachment><br> |
|`custom_page` |* `page_mode`：取值必须为 `redirection`，表示页面重定向。<br><br>* `status_code`：CDN 响应状态码，取值有 `301`、`302`、`303`、`307`、`308`。<br><br>* `location`：重定向 URL。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_4db381c7252d3a785e97184575561aaa.json" name="custom_page.json">custom_page.json</Attachment><br> |


<span id="stage-为-origin-request"></span>
### Stage 为 origin_request


|**行为（Action）**  |**配置参数** |**示例** |
|---|---|---|
|`origin_range` |* `switch`：是否启用回源 Range。<br><br>* `range_type`：分片类型，取值只能为 `fixed`，表示固定分片。<br><br>* `range_size`：分片大小。<br><br>   * 如果 `unit` 是 `KB`，`range_size` 只能是 `512`。<br><br>   * 如果 `unit` 是 `MB`，`range_size` 的取值范围是 1\-40。<br><br>* `unit`：分片的单位，取值有 `KB`、`MB`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64df7cb3754d8b9bd5eac4dc2060d894.json" name="origin_range.json">origin_range.json</Attachment><br> |
|`origin_follow` |* `switch`：是否启用回源重定向跟随。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7bff59be74c35e9cbe81238f9167fa1d.json" name="origin_follow">origin_follow</Attachment><br> |
|`origin_tcp_timeout` |* `connect_timeout`：TCP 建连的超时时长，默认值是 `2`。<br><br>* `connect_timeout_unit`：超时时长的单位，取值只能是 `sec`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08d39bc3afcddaa53d1a1830e572425c.json" name="origin_tcp_timeout">origin_tcp_timeout</Attachment><br> |
|`origin_http_timeout` |* `connect_timeout`：HTTP 请求的超时时长，默认值是 `60`。<br><br>* `connect_timeout_unit`：超时时长的单位，取值只能是 `sec`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7749919155603107989f0d97cacd02ce.json" name="origin_http_timeout.json">origin_http_timeout.json</Attachment><br> |
|`origin_rewrite` |* `action`：改写类型，有以下取值：<br><br>   * `path_rewrite`：路径改写，不包含查询参数。<br><br>   * `url_rewrite`：路径改写，包含查询参数。<br><br>* `source_path`：用于匹配客户端请求 URL 中路径的正则表达式，最长 1,024 个字符。<br><br>* `target_path`：回源请求 URL 中改写后的路径，最长 1,024 个字符。支持使用 `$1` 、 `$2` 、 `$3` 等引用 `source_path` 中定义的捕获组。<br><br>* `mode`：匹配到改写规则后的处理方式。取值只能为 `break` ，表示当前规则匹配后，不再匹配后续改写规则。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10c7424a8861b203467208c34865f69f.json" name="origin_rewrite.json">origin_rewrite.json</Attachment><br> |
|`origin_sni` |* `domain`：自定义的 SNI 域名。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_502d9ab2b1b7addcc7c54fa31498cf82.json" name="origin_sni.json">origin_sni.json</Attachment><br> |
|`origin_protocol` |* `origin_protocol`：回源请求使用的协议，取值有 `follow_client`、`http`、`https`。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bdfdaaa95f0a0efe41a87f6d54ca2991.json" name="origin_protocol.json">origin_protocol.json</Attachment><br> |
|`origin_request_header` |* `action`: CDN 响应用户请求时对响应头的操作，取值有 `set`、`delete`。<br><br>* `header_name`：头部名称。<br><br>* `header_value`：头部值，适用于 `action` 是 `set` 的情况。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9879c889c26a7ceda887251af1a7e1a8.json" name="origin_request_header.json">origin_request_header.json</Attachment><br> |
|`origin_host` |* `host`：回源请求中的 Host 头部值。 |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7fcb1327bda9210a128a8361054f62d.json" name="origin_host.json">origin_host.json</Attachment><br> |


<span id="各匹配对象的输入要求"></span>
## 各匹配对象的输入要求


|**匹配对象** |**IgnoreCase** |**可指定的** **Operator** |**Name 输入要求** |**Value 输入要求** |**示例值** |
|---|---|---|---|---|---|
|`always` |不适用 |不适用 |不适用 |不适用 | |
|`path` |适用 |`equal` `not_equal` |不适用 |* 必须以 `/` 开头。<br><br>* 总数不能超过 100 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。 |`["/www/img/myimage.png", "/docs/file"]` |
|||`prefix_match` `prefix_not_match` ||* 必须以 `/` 开头。<br><br>* 总数不能超过 100 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%） |`["/www", "/docs/f"]` |
|||`suffix_match` `suffix_not_match` ||* 总数不能超过 100 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。<br><br>* 不能以句点（.）开头。 |`["png","docx"]` |
|||`regex_match` `regex_not_match` ||* 总数不能超过 50 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。 |`["^/a{1,2}(.*)g$"]` |
|||`belong_to` `not_belong_to` ||指定一个全局配置，且该全局配置必须满足以下条件：<br><br><br>* `ConfigType` 是 `common_match_list`。<br><br>* `CommonListType` 是 `exact_match` 或者 `regex_match`。 |`["MySharedList"]` |
|`path_and_param` |适用 |与 `path` 相同 |不适用 |与 `path` 相同。 | |
|`url` |适用 |`equal` `not_equal` |不适用 |* 必须以 `http://` 或者 `https://` 开头。<br><br>* 总数不能超过 100 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。 |`["https://www.example.com/www/img/myimage.png","https://www.example.com/docs/file"]` |
|||`prefix_match` `prefix_not_match` ||* 必须以 `http://` 或者 `https://` 开头。<br><br>* 总数不能超过 100 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。 |`["https://www.example.com/www", "https://www.example.com/docs/f"]` |
|||`suffix_match` `suffix_not_match` ||* 总数不能超过 100 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。 |`["png","docx"]` |
|||`regex_match` `regex_not_match` ||* 总数不能超过 50 个，总长度不能超过 300 个字符。<br><br>* 不能包含空格、百分号（%）。 |`["^/a{1,2}(.*)g$"]` |
|||`belong_to` `not_belong_to` ||指定一个全局配置，且该全局配置必须满足以下条件：<br><br><br>* `ConfigType` 是 `common_match_list`。<br><br>* `CommonListType` 是 `exact_match` 或者 `regex_match`。 |`["MySharedList"]` |
|`http_referer` |适用 |`equal` `not_equal` |不适用 |* 总数不能超过 100 个。<br><br>* 单个条目的长度不能超过 200 个字符。 |`["https://www.example.com/image.png", "a.example.com","*.exampe.net","203.0.113.8"]` |
|||`exist` `not_exist` ||不适用 | |
|||`regex_match` `regex_not_match` ||* 总数不能超过 50 个。<br><br>* 单个条目的长度不能超过 200 个字符。 |`["^/a{1,2}(.*)g$"]` |
|||`belong_to` `not_belong_to` ||指定一个全局配置，且该全局配置必须满足以下条件：<br><br><br>* `ConfigType` 是 `common_match_list`。<br><br>* `CommonListType` 是 `exact_match` 或者 `regex_match`。 |`["MySharedList"]` |
|`client_ip` |不适用 |`match` `not_match` |不适用 |* 支持 IP 地址和 CIDR 网段。<br><br>* 支持 IPv4 地址和 IPv6 地址。<br><br>* 总数不能超过 100 个。 |`["203.0.113.8","203.0.113.9"]` |
|||`belong_to` `not_belong_to` ||指定一个全局配置，且该全局配置必须满足以下条件：<br><br><br>* `ConfigType` 是 `common_match_list`。<br><br>* `CommonListType` 是 `ip_match`。 |`["MySharedList"]` |
|`http_origin` |适用 |与 `http_referer` 相同。 |不适用 |与 `http_referer` 相同。 | |
|`http_ua` |适用 |与 `http_referer` 相同。 |不适用 |与 `http_referer` 相同。 | |
|`request_header` |适用 |与 `http_referer` 相同。 |* 不能包含汉字、下划线（_）、空格、双引号（"）、冒号（:）。<br><br>* 长度不能超过 100 个字符。 |与 `http_referer` 相同。 |**Name**<br><br>`myheader`<br><br>**Value**<br><br>`["value1","value2"]` |
|`client_area` |不适用 |`match` `not_match` |不适用 |* 包含最多 30 个国家或地区的 Alpha\-3 代码。Alpha\-3 代码可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取。 |`["PNG","FSM","FSM"]` |
|`http_method` |不适用 |`equal` `not_equal` |不适用 |* 包含以下一个或者多个值：`post`、`head`、`get`、`put`、`options`、`delete`、`connect`、`patch`。 |`["post","options"]` |
|`request_time` |不适用 |`match` `not_match` |`weekday`：每一周中的某些天。 |* 包含以下一个或者多个值：`mon`、`tue`、`wed`、`thur`、`fri`、`sat`、`sun`。 |`["mon","fri"]` |
||||`period`：某个任意时间段。 |开始时间和结束时间精确到秒。 |`["2025-05-07 14:21:21", "2025-06-13 14:21:24"]` |
||||`everyday`：一天中的某个时间段。 ||`["02:02:02","06:04:04"]` |
|`protocol` |不适用 |`equal` `not_equal` |不适用 |指定 `http` 或者 `https`。 |`["http"]` |
|`client_cert_info` |适用 |`match` `not_match` |`common_name`：证书主题中的通用名称（Common Name）。 |总数不能超过 100 个，每个长度不能超过 64 个字符，支持以通配符 `*` 开头和结尾。 |`["www.example.com"]` |
||||`serial_number`：证书序列号。 ||`["03A7F2C91B4E6D8A"]` |
||||`country_name`：证书主体所属国家或地区的代码。 ||`["CN"]` |
||||`locality_name`：证书主体所在的城市或地区。 ||`["Beijing"]` |
||||`organization_name`：证书主体所属组织或公司名称。 ||`["Example Co., Ltd."]` |
||||`organizational_unit_name`：证书主体所属的组织单位或部门名称。 ||`["IT Department"]` |
|`response_header` |适用 |与 `http_referer` 相同。 |* 不能包含汉字、下划线（_）、空格、双引号（"）、冒号（:）。<br><br>* 长度不能超过 100 个字符。 |与 `http_referer` 相同。 |**Name**<br><br>`myheader`<br><br>**Value**<br><br>`["value1","value2"]` |
|`http_code` |不适用 |`match` `not_match` |不适用 |* 包含最多 30 个状态码。<br><br>* 状态码的范围是 100\-599。<br><br>* 支持指定 `2xx`、`3xx` 等。 |`["405","5xx"]` |


<span id="返回参数"></span>
## 返回参数

<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

<span id="示例一"></span>
#### 示例一

```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
    "Rule": "{\"IfBlock\":{\"SubRules\":[],\"Actions\":[{\"Action\":\"origin_tcp_timeout\",\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"30\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}],\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Condition\":{\"Object\":\"always\"}}]}]}}}"
}
```


<span id="示例二"></span>
#### 示例二

本示例重点展示 `Condition` 的配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本示例不能直接使用。您需要先处理 <code>Rule</code> 结构体中的参数配置。参见 <code>Rule</code> 参数的说明。</div>


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


<span id="示例三"></span>
#### 示例三

本示例重点展示 `Actions` 的配置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本示例不能直接使用。您需要先处理 <code>Rule</code> 结构体中的参数配置。参见 <code>Rule</code> 参数的说明。</div>


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
